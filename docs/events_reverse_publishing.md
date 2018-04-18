# Reverse Publishing with Pointslocal

> Reverse publishing is typically used to take events from Pointslocal and convert them into a print-friendly format for inclusion in a newspaper or other publication.

> The following documentation will show how to select, format and export events for print.

## Selecting events for reverse publishing
The admin and the reverse publishing templates themselves provide a number of ways to select or specify events for reverse publishing.

### Manual selection
The first is to manually select the events you want from the list in the admin.  This has some limitations in terms of total events available to be shown in browser.

https://pointslocal.github.io/docs/events_search

By checking any event you will make them available for export.  With one or more event selected, click the Export button in the utility bar and select your template.

![Selecting Events](https://raw.githubusercontent.com/pointslocal/docs/master/assets/img/events_reverse_publishing/events_revers_publishing_selection.png)

### The Queue
Events can also be added to a queue, which can be thought of as a working group of events.  By selecting any number of events and clicking the Queue button in the utility bar, you'll be redirected to your current working set.  This allows you to perform multiple searches and pick and choose events from the list.  From here you can again select those you wish to export and click the Export button as described above.

![Viewing Your Queued Events](https://raw.githubusercontent.com/pointslocal/docs/master/assets/img/events_reverse_publishing/events_revers_publishing_queue.png)

### Automatic
The template configuration itself (described below) can automatically select events for you.  

A use case: you know that you will always want to export all Arts events starting Thursday through the following Thursday without any further curation.  The template itself allows you to specify this in the API call.  


This will cause the export to go to one or more of the available output destinations (described below).

## Formatting with the template
> The following sections are advanced topics and for many use cases there will be no need to explore these areas of the admin. We recommend that you request export templates directly from Pointslocal, particularly if you do not have strong knowledge of templating, JSON and Javascript.

The way the events are formatted is very configurable.  This section will explain how to create and route a reverse publishing export.

Under Exports in the left-hand "hamburger" navigation, export configurations can be created or modified.  There are three components to an export template:

* The template itself.  This is the text representation of the output.
* The preprocessing.  This is a Javascript-based manipulation of the underlying data as returned by the API.
* The configuration.  This tells the exporter where to get the data, how to request it and what to do with the final output.  It relies on the Pointslocal API and accepts any options documented there.

### The Template
The Pointslocal reverse publishing component is capable of producing any *normal* text format.  By normal we mean anything that can be templatized in a reliable text format.  Typically this includes plain text, CMS-specific formats, XML., Word documents, etc.

The templating language used is Mustache.  You can read more about it [here](https://mustache.github.io/).  You can utilize any API key/value returned or created by preprocessing here.  An example:

```html
<h1>{{title}}</h1>
{{day}} {{start_time}}. {{venue_name}}.  {{description}}{{#url}}See: {{url}}{{/url}}
```

This would bring back the ```title``` and additional fields from the API call to be output in the template.  The ```day``` field does not exist as part of the API call and thus would have to be created in the preprocessing.  See below:

## The Preprocessing
This accepts arbitrary Javascript.  This is supplied a single top-level array:
* ```groups``` - A selection of grouped events (by category, date, neighborhood, etc)
* ```items``` - Each group then has an array of 0 or more items that belong to it.

In the above example we need to create a day of the week from the date returned by the API.  To do so we'll just invoke a little Javascript:

```javascript
// iterate the groups
for (var i=0; i<groups.length; i++) {
    // iterate each group's items
    for (j=0; j<groups[i].items.length; j++) {
        // add a new value for day of week "day"
        var dateob = new Date(groups[i].items[j].date);
        var dow = '';
        switch (dateob.getDay()) {
            case 0:
                dow = 'Sunday';
                break;
            case 1:
                dow = 'Monday';
                break;
            case 2:
                dow = 'Tuesday';
                break;
            case 3:
                dow = 'Wednesday';
                break;
            case 4:
                dow = 'Thursday';
                break;
            case 5:
                dow = 'Friday';
                break;
            case 6:
                dow = 'Saturday';
                break;                
        }
        groups[i].items[j].day = dow;
    }
    
}

```

While a trivial example, this example shows how the data can be manipulated and augmented for use in the template.

### The Configuration
Available outputs for export include:

* ```email``` - Accepts any number of recipients
* ```ftp``` - Allows authenticated or anonymous FTP uploads
* ```sftp```
* ```download``` - downloads the file directly from browser

Without any specified outputs, the output will be shown in browser.
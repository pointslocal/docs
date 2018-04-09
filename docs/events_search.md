# Searching Events

> The events search page provides several ways to locate events for edit, approval or inclusion in reverse publishing.

![Searching Events](https://raw.githubusercontent.com/pointslocal/docs/master/assets/img/events/events_search.png)



### Text Search
The text search will do an exact search for your events across the title, description, venue name and venue address fields.
<!--
### Category Search

### Neighborhood Search
-->
### Template Search
![Searching Events by Template](https://raw.githubusercontent.com/pointslocal/docs/master/assets/img/events/events_search_template.png)
A template represents a set of rules and formats around a reverse publishing export.  Some examples might include "Entertainment events in the downtown area in the next two weeks" or "Arts events anywhere this weekend."

In search, these rules can be used to approximate a result set for edit or export; they can be considered, in fact, saved searches.   If a template has been defined with parameters like the examples above, it can be used to execute a search.  Instead of selecting "Entertainment," "Downtown" and "Next Two Weeks" in the search bar each time, those will be pre-populated for you.  In addition, each additional search option can override those in the template.

These templates (and their rules) can be configured by clicking the "hamburger" icon in the top left to open the secondary navigation and then clicking "Exports."  Configuring these may require some technical knowledge of JSON and our API, documented at http://pointslocal.readthedocs.io/en/latest/api/.

<!-- ### Featured Search 

This allows you to search for events that are featured for today.
-->
### Date Search
The date search allows single day or range searches via the Start Date and End Date inputs.  Clicking either will show a WYSIWYG datepicker.

The default value for Start Date is today and the default value for End Date is +2 weeks.  

<!--
## Advanced Searches

### Source Search

### Tag Search

### User Search

-->
# Managing Feeds
New Feed Views Summary:
1. All Feeds Log: A dashboard view of all feeds and the results of their last run. Note: If a feed has been established but not yet run, the result data will be void and a grey dot will indicate that status.

2. Individual Feed Log: Accessed by drill down from the All Feeds Log. This exposes the history of the last 100 runs of the feed. This may change to a different frequency as a result of QA or experience in production (i.e.: last two weeks of runs for the feed).

3. Aggregate Feed Log: Accessed by two links. First, by clicking on the "Detail" button in top right corner of the All Feeds Log (just to left of spyglass). Second, as a bread crumb link (“Feed Log”) in the top left of a sub view.

### All Feeds Log (Event Imports)

#### View header

* Feed Info: General information about the feed and it’s health over time

* Fetch Info: Details of the last time the feed was accessed including quantity of events.

* Process Info: Information on what the system did with the data that came from the fetch.

* Data Info: State of the system as it relates to future events from that feed.

#### Columns

* Health: A subjective summary of the previous 7 days' worth of fetches and imports. Also accessible via search or sort. This can be represented by three icon states: 

    1. A smiling emoji, indicating no errors in that time period.

    2. An indifferent emoji, indicating a mix of errors and successes OR no runs in that time period.

    3. A sick emoji, indicating *only *errors in that time period.

* Featured (Feat.): Indicates and allows toggling of featured status.  Featured status for a feed can enable quick access to feeds considered to be of high value via search or sort.

* Active (Act.): Indicates and allows toggling of active status of a feed. An inactive feed will not be fetched or processed. Also accessible via search or sort.

* Name: Contains three values. 

    4. A source indicator (Facebook, Scrape, Google Calendar, iCal import and general API).

    5. The Name (often the venue name) whose name is linked to the import history for that feed

    6. An external link that resolves to the feed’s fetch destination

* Status: The result of the last fetch and process of the feed.  

    7. A green circle indicates no error encountered.

    8. A red circle indicates an error on fetch or processing was encountered.

    9. A grey circle indicates the feed has never run and has no prior status.  

* Count: The number of events found in the feed. This could include past events that will be ignored on process. 

* Started: The time (or time ago) the feed fetch process began.  If the import began within the last 24 hours, value is express in hours. Otherwise and date is shown.

* Invalid: Count of events in the feed that are missing required data. Currently, validation occurs for: title, date and time.

* Created: The number of new events (not existing in system) created on that import.

* Existed: The number of events encountered that already existed.  These are not created.

* Future(30/60/90): The total number of future events followed by the count of event in subsequent 30-day blocks.  These block counts do not overlap.  Note: block counts may or may not add up to total future events.

### Individual Feed Log (Recent history of each import for a feed)

#### View header

* Fetch Info: Details of the last time the feed was accessed including quantity of events.

* Events: A breakdown on what the import process did with encountered events from feed. The sum of all columns in the events breakdown equals the Count value under the Fetch Info.

* Venues: Indicates the count of venues created on each fetch. Normally, this will be 0.

#### Columns

* Status: The result of the fetch and process.  

    10. A green circle indicates no error encountered.

    11. A red circle indicates an error on fetch or processing was encountered.

* Count: Count of events found in the feed. 

* Started: The time (or time ago) the feed fetch process began.

* Duration: The time (in seconds, minutes or hours) it took to fetch the feed.

* Invalid: Count of events in the feed that were missing required data.

* Created: Count of new events (not existing in system) created on that import.

* Existed: Count of events encountered that already existed. 

* Duplicate: Currently hard-coded to zero. Intention: The number of events encountered that were seen as duplicate (existed as part of another feed and/or through admin users or UGC). 

* Blocked: Count of events bypassed due to having been blocked via admin.  Note: currently event blocking is a site config-based rule that has to be manually enabled by Pointslocal.  When enabled, blocking occurs on the deletion of an event from a feed in the admin.

* Updated: Currently hard-coded to zero. Intention: The number of events that had date/time information updated from the upstream feed source.

* Passed: Count of Events in the feed that had dates in the past (already occurred).

* Created: Count of new events created on that import.

### Aggregate Feed Log (Recent history of all imports)

Effectively the same view as the individual feed log, except:

* Feed Info: Shows the name and type of the feed

* Doesn't show updated count

* Doesn't show feed fetch duration 

## Glossary of Terms

* Feed - Any source of data accessible via HTTP through APIs or scraped web sites

* Import - The event and process by which a feed is read, analyzed and ingested into Pointslocal


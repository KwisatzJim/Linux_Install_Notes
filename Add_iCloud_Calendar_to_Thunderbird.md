### Add iCloud calendar to Thunderbird

A) Create an app-specific password for Thunderbird

B) Discover the URL to your iCloud calendar

iCloud calendar URLs for Thunderbird (and other iCal clients) contain three pieces of information that are unique for each calendar:

https://<server-number>-caldav.icloud.com/<user-id>/calendars/<calendar-id>/

There are several ways to find the effective values for your specific calendar but none are “consumer-ready”. What I present below is the easiest I could find. Let me know if you found something more user friendly.  
If you feel confident running scripts executing the ‘icloud-calendar-urls’ Ruby script instead is a lot more convenient.

- Open the iCloud calendar app in the browser of your choice.
- Open the browser’s developer tools aka inspector. Often hitting F12 gets you there but the below table has all the details:

| •         | • Google Chrome | • Firefox      | • Internet Explorer/Edge | • Safari |
|-----------|-----------------|----------------|--------------------------|----------|
| •	MacOS   | •	⌘+⌥+i         | •	⌘+⌥+i        | •	n/a                    | •	⌘+⌥+i  |
| •	Windows | •	ctrl+shift+i  | •	ctrl+shift+i | •	F12                    | •	n/a    |

```
•	Open the ‘Network’ tab in the devtools
```

- clear any entries that may already be there to empty the list (in Chrome: crossed-through circle icon, 2nd from left)
- filter for ‘collections’ (enter that into the text field)
- activate only the ‘XHR’ requests
- Now, on the iCloud page, click the checkmark on the left side of the calendar you want to integrate into Thunderbird.
- The inspector will record a HTTP request against URL that looks something like this https://<server-number>-calendarws.icloud.com/ca/collections/<calendar-id>?<lots-of-keys-and-values>&dsid=<user-id>&yadayada-etc. Extract server number, calendar ID and user ID and keep them somewhere handy.
- In my case the user ID is a 9-digit number and the calendar ID consists of 40+ alphanumeric characters and dashes.
- Extract the three highlighted pieces of information.

Alternatives for tech-savvy folks:

- open-source iCloud discovery client (Docker or PHP or Groovy/Java) by Daniel Mühlbachler
- poking through Info.plist files in /Users/<your-username>/Library/Calendars on the Mac. This can be simplified by running the ‘icloud-calendar-urls’ Ruby script.

C) Create calendar to Thunderbird

You’re home free! The last step is a trivial one.

In Thunderbird open the ‘Calendar’ tab, then right-click on the left side in the calendar list and select ‘New Calendar’.

In the next dialog select ‘On the Network’ and hit ‘Continue’. The calendar URL you extracted in the previous step needs to be entered in the following dialog after you select ‘CalDAV’ as your calendar format.

Again, the URL is https://<server-number>-caldav.icloud.com/<9-digit-user-id>/calendars/<calendar-id>/. The actual values for the <xxx> tokens is what you collected in step B.

Thunderbird will then ask you for a password at which point you enter the app-specific iCloud password generated in step A).

Congratulations, well done!

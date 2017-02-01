---
layout: post
title:  "It took 4 days to get TransitDB unsuspended"
categories: TransitDB, Android
---

This is a happy resolution to the [previous post](https://www.carsonlam.ca/transitdb-app-suspended/) 
about TransitDB being suspended from the Play Store due to
a spurious accusation of the app serving as an 'alternate app store'.
It took four days, but I successfully navigated the Google Play bureaucracy after a few stumbles.
The whole process has been somewhat of a Kafka-esque nightmare,
and shaken my faith in the highly automated nature of the Google Play app validation processes.

**What worked:** the only way to get through this process is through the 
[Google Play App Removal Appeal Form](https://support.google.com/googleplay/android-developer/troubleshooter/2993242).
This appeals form is the one and only shot you get.
Unfortunately, most replies are form letters, and the first reply I got apparently did not actually read my appeal message.
It was just a form letter re-stating what the app was originally accused of (Payments Policy violation),
and that this only resulted in a rejected update, not suspension.

It wasn't clear how I was supposed to respond to this: was I supposed to just reply to the email, or re-appeal?
The email had no instructions. Turns out the correct action is to just reply to the email.
There won't be any auto-acknowledgement, and a response usually arrives in a day.
I clearly restated the timeline of events and what had gone wrong, and my appeal was then accepted.
Unfortunately, the staff could provide no further insight.
They couldn't explain what had triggered the Payments Policy violation flag, 
why the app was falsely accused of being an Alternate App Store,
nor whether this was a fully-automated process that hit a false flag.

**What didn't work:** The Google Play Support live chat won't help here.
It's mainly intended for Google Play consumers, not developers, but I thought it was worth a shot.
No luck there, though: the live chat staff said they have no access to information about policy issues
(which is what app suspensions are), and they best they can do is send a note to the Policy team
in the hopes of expediting a resolution.

When I added in-app purchases to TransitDB, I received an email from a human at Google, introducing themselves as my new "Partner Manager". 
After filling out a developer survey linked in that introductory email, I received a personalized response from the same person.
I emailed this "Partner Manager" of mine twice regarding my predicament, and never heard back: no autoresponder, no bounce, nada.

**Submitting a 'clean' update to the app after suspension:**
After the app is unsuspended, it can only be republished to the Play Store following an app update.
Unfortunately, the whole procedure to get the app unsuspended did not yield and concrete steps on how to avoid getting auto-suspended again.
All I can go on is the theory that the Play Store had started flagging apps for violating the Payments Policy by searching apps 
for strings referencing PayPal or Patreon. This would mean that simply never showing PayPal/Patreon links when the app
runs on a Google Play device isn't enough: the strings must be scrubbed from the Play Store version of the app entirely.

The way to accomplish this is with Android Gradle Build Flavors.
I already use Build Flavors in TransitDB to handle slight manifest differences for distribution on
[Amazon App Store](https://www.amazon.com/Carson-Lam-TransitDB-Vancouver/dp/B00RYZVCOW/) and 
[BlackBerry World](https://appworld.blackberry.com/webstore/content/32009887/).
Scrubbing PayPal/Patreon links from the Google Play version of the app while keeping them in the 
versions distributed on the other app stores meant that I had to start using sourcesets.
Now, a different definition of the same Java class is used for each Build Flavor: 

* One that exclusively uses the Google Play Billing Services Library for in-app purchases, for distribution only on Google Play
* Another that contains only links to PayPal and Patreon, with all the strings inside (instead of in a resource XML)

This took significant refactoring to ensure that the difference between the flavors boiled down to a single Java class.
It was all worth it, as it reduces my maintenance burden, and gives me the peace of mind that the app _probably_ won't be falsely flagged again.

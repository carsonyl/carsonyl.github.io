---
layout: post
title:  "Number of bus routes serving each Vancouver bus stop throughout a day"
categories: TransitDB, Transit, TransLink
---

TransLink recently [changed their Next Bus SMS service](http://buzzer.translink.ca/2016/08/some-tweaks-to-the-next-bus-sms-service/)
to require that users include route numbers in addition to the stop code.
For instance, where previously you could simply text '[50913](http://www.transitdb.ca/stop/50913/)' to 33333,
you now must text '50913 99'.
If the stop is served by multiple routes, you can include up to two route numbers in your SMS.
**This got me wondering: how many bus stops are served by more than one route?**

The question of the number of route serving each stop is worth answering,
because the [TransitDB Android app](https://play.google.com/store/apps/details?id=ca.transitdb.mobile.android) includes a feature to text the current stop's code to 33333.
I want to update this feature to include the route numbers that are now required,
but I also want to know if I can get away with a solution that avoids prompting the user
to pick route numbers after choosing the 'Text 33333' option.
My desired solution is to include the route numbers in the text message if I know the stop is only served by up to two routes.
Otherwise, no route numbers are included, and the user has to do it themselves.

Right from the start, it's clear that a route that uses a stop for unloading only should not count towards that stop's tally of routes.
Out of TransLink's 8727 active bus stops, this only eliminates 63 stops from consideration.

Since bus schedules work on a daily basis, let's drill down to a typical weekday,
and look at the routes per stop:

Number of routes at stop | Number of stops
--- | ---
12|2
10|3
9|13
8|14
7|39
6|75
5|135
4|206
3|704
2|2184
1|5263

Tied for first place with 12 routes each are [EB W PENDER ST FS SEYMOUR ST](http://www.transitdb.ca/stop/50078/) and [NB 203 ST FS FRASER HWY](http://www.transitdb.ca/stop/57025/).
There are 8638 active stops on this typical weekday, and 7447/8638 (86%) are served by two routes or fewer.
This is a good portion just by absolute numbers, but a lot of stops are pushed over the threshold due to various special circumstances, including:

* The stop also serves NightBus
* Special routes such as School Specials make use of regular stops just a couple of times in the day
* Routes allocate odd trips to some stops, but not enough to justify saying the stop is 'served' by the route

These special cases can be worked around by limiting the scope to a smaller window of time instead of a whole day.
This also makes sense in practice, since Next Bus SMS is about providing real-time arrival predictions for the next two buses,
and if you're texting 33333 in the afternoon, it doesn't make sense to consider NightBus routes or anything outside the near term.
So, let's narrow the scope to a typical weekday, between 4pm and 4:30pm:

Number of routes at stop | Number of stops
--- | ---
9|5
8|5
7|18
6|26
5|62
4|124
3|379
2|1552
1|5795

During this 30 minute window of the peak period, 7347/7966 (92%) of stops are served by two routes or fewer.
For a sample of other extremes, a 10:30am to 11am off-peak window yields 7061/7532 (94%),
and a late night window of 11:30pm to 12am yields 4645/4815 (96%).

So it's starting to sound like my desired solution will be very good. But wait:
all stops are not equally likely to be chosen for texting 33333.
In practice, it appears that roughly 1 in 5 usages of this feature in the app are
for stops that have more than 2 routes according to the criteria above.

I implemented this solution and pushed it out in an app update on Sunday,
thinking that the problem with this solution would fly under the radar.
Within 12 hours of the update, someone had noticed and sent me feedback pointing it out.

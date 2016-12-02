---
layout: post
title:  "I've read about those unexpected app suspensions—and then it happened to me"
categories: TransitDB, Android
---

I publish TransitDB on the [Play Store](https://play.google.com/store/apps/details?id=ca.transitdb.mobile.android), [Amazon App Store](https://www.amazon.com/Carson-Lam-TransitDB-Vancouver/dp/B00RYZVCOW/), and [BlackBerry App World](https://appworld.blackberry.com/webstore/content/32009887/).

The following story all happened within a span of about 3 hours, by my estimate.

Today I submitted an update to the Play Store. Just some transit schedule changes. Went to private alpha, and then to 10% staged rollout. At that point, it was rejected for violating the Payments Policy.

> **Policy Issue:** Payments
>
> Alternative payment mechanisms to Google Play’s in-app billing service are only permitted if the products purchased are to be used outside of the app. For example:
> * For physical goods or services, such as movie tickets, or a publication where the price also includes a hard copy subscription; or 
> * For digital goods that may be downloaded to devices and used outside of the app, such as songs that can be played on other music players.
>
> Donations to 527 designated tax exempt organizations are also permitted.

This sounded like it took issue with me offering in-app donation options via Patreon and PayPal in addition to Google IAP. I had those alternate options ever since I added donation options into the app about a year ago, and it had survived many app updates without comment until this point. In any case, I added a check to hide those options when it detects the presence of `com.android.vending`, and submitted that as a new update.

I go through the private alpha and 10% staged rollout process again. This time, the app was suspended for violating the Alternative Stores provision:

> **4.5 Alternative Stores.** You may not use the Store to distribute or make available any Product which has a purpose that facilitates the distribution of software applications and games for use on Android devices outside of the Store.

Needless to say, this was a fairly shocking and serious allegation, and certainly some kind of false positive. Everything the app does is totally above-board, and I can't imagine what could have tripped this flag. I do make an effort to not do anything shady or contrary to the policies.

I've submitted an appeal. Appeal decisions are final, so I hope I haven't screwed up my case. Their confirmation email says that they could take up the 72 hours to respond. It's frustrating.

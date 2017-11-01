---
layout: post
title:  "Be careful when using java.util.Calendar to get month names"
categories: Android
---

`java.util.Calendar` operates in 'lenient' mode by default.
This means that setting invalid date values will silently yield a reconciled value on retrieval.
The example given in the documentation is that setting January 32 yields February 1.

When working with Calendar instances for the purpose of getting back a month name,
this silent lenient mode can bite you. For instance:

```java
Calendar month = Calendar.getInstance();
month.set(Calendar.MONTH, Calendar.NOVEMBER);
return String.format(Locale.getDefault(), "%tB", month);
// or return month.getDisplayName(Calendar.MONTH, Calendar.LONG, Locale.getDefault())
```

The code snippet above tries to get the English name for `Calendar.NOVEMBER`.
When this code is run between October 1 through 30, this returns "November", as expected.
But on October 31, something spooky happens: it unexpectedly returns "December". 👻

This is because November 31 is an invalid date, and automatically gets reconciled to December 1.
There's two possible solutions to this:

* Set the day of month to 1 prior to setting the month. Or at the same time using `Calendar.set(year, month, day)`.
* Avoid making a `Calendar` instance in the first place, by using `DateFormatSymbols.getInstance(Locale.getDefault()).getMonths()[month]`.

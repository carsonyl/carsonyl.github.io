---
layout: post
title:  "The versioning relationship between pytz and the IANA Time Zone Database"
categories: Python
---

[pytz](https://pypi.python.org/pypi/pytz) is a Python library that provides the world timezone database.
pytz tracks the [IANA Time Zone Database](http://www.iana.org/time-zones), though its version numbers don't exactly match.
For instance, pytz 2016.6.1 corresponds to the 2016f IANA Time Zone Database release.
How does this work?

The IANA Time Zone Database's versioning follows the pattern of _yearX_,
where _X_ is a letter incremented for every update in that year.
Thus, 2016a is the first release of the year, and 2016f is the sixth.

pytz's versioning is similar, but follows the [Semantic Versioning](http://semver.org/) convention of _major.minor.patch_
by tagging versions as _year.num[.patch]_, where _num_ is _X_ above, but converted to a number starting at 1.
Alternatively, `num = ord(X) - ord('a') + 1`. Though IANA's versioning increases consecutively,
pytz does not necessarily have a release for every IANA database version, so there can be gaps.

pytz was originally versioned exactly the same as the IANA database,
but, in order to be compatible with pip, switched to the current scheme starting with 2013f / 2016.6.

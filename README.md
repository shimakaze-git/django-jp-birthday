# django-jp-birthday

![https://pypi.python.org/pypi/django_jp_birthday](https://img.shields.io/pypi/v/django_jp_birthday.svg)
[![image](https://img.shields.io/pypi/pyversions/django-jp-birthday.svg)](https://pypi.org/project/django-jp-birthday)
![https://img.shields.io:/pypi/djversions/django-jp-birthday](https://img.shields.io:/pypi/djversions/django-jp-birthday)
![https://django-jp-birthday.readthedocs.io/en/latest/?version=latest](https://readthedocs.org/projects/django-jp-birthday/badge/?version=latest)
[![Updates](https://pyup.io/repos/github/shimakaze-git/django-jp-birthday/shield.svg)](https://pyup.io/repos/github/shimakaze-git/django-jp-birthday/)
[![Python 3](https://pyup.io/repos/github/shimakaze-git/django-jp-birthday/python-3-shield.svg)](https://pyup.io/repos/github/shimakaze-git/django-jp-birthday/)
[![Total alerts](https://img.shields.io/lgtm/alerts/g/shimakaze-git/django-jp-birthday.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/shimakaze-git/django-jp-birthday/alerts/)
![https://img.shields.io/github/repo-size/shimakaze-git/django-jp-birthday](https://img.shields.io/github/repo-size/shimakaze-git/django-jp-birthday)
![https://img.shields.io/github/languages/code-size/shimakaze-git/django-jp-birthday](https://img.shields.io/github/languages/code-size/shimakaze-git/django-jp-birthday)
![https://codecov.io/gh/shimakaze-git/django-jp-birthday/branch/master/graph/badge.svg](https://codecov.io/gh/shimakaze-git/django-jp-birthday/branch/master/graph/badge.svg)
![https://img.shields.io/github/license/shimakaze-git/django-jp-birthday.svg](https://img.shields.io/github/license/shimakaze-git/django-jp-birthday.svg)
[![image](https://img.shields.io/pypi/dm/django-jp-birthday)](https://img.shields.io/pypi/dm/django-jp-birthday)
[![.github/workflows/test.yml](https://github.com/shimakaze-git/django-jp-birthday/actions/workflows/test.yml/badge.svg)](https://github.com/shimakaze-git/django-jp-birthday/actions/workflows/test.yml)

django-jp-birthday is a django's model for use Japanese birthdays and ages.

Based library is [https://github.com/bashu/django-birthday](https://github.com/bashu/django-birthday) .

Authored by [shimakaze_soft](https://github.com/shimakaze-git) and some great

[contributors](https://github.com/shimakaze-git/django-jp-birthday/CONTRIBUTING.rst)

# Features

- Converting Birthdays to Japanese Style
- Get all birthdays from specified Japanese calendar
- Calculate age based on birthday
- Get the zodiac
- Get all birthdays from specified zodiac
- Years of the Japanese era

-----

- Get all user profiles within the next 30 days
- Get all user profiles which have their birthday today
- order the user profiles according to their birthday

# Installation

- [pypi](https://pypi.org/project/django-jp-birthday/)

```Bash
$ pip install django-jp-birthday

$ python steup.py install
```

# Usage

django-jp-birthday provides a `jp_birthday.models.BirthdayModel` model type which is a subclass of django.db.models.Model and thus has the same characteristics as that.

`jp_birthday.managers.JpBirthdayManager` is used as a manager for `jp_birthday.models.BirthdayModel` and provides various methods.

```Python
from jp_birthday.models import BirthdayModel

class ModelsTest(BirthdayModel):

    class Meta:
        app_label = 'jp_birthday'
        ordering = ('pk',)
```

## Converting Birthdays to Japanese Style

```Python
# id: 1
# ["2001-01-01"]

m = ModelTest.objects.filter(id=1).first()
birthday = m.get_jp_era_birthday()
# h-13-1-1

birthday = m.get_jp_era_birthday(True)
# {'era': 'heisei', 'era_short': 'h', 'era_jp': 'へいせい', 'era_kanji': '平成', 'year': 13, 'month': 1, 'day': 1}
```

## Get all birthdays from specified Japanese calendar

```Python
# ["2001-01-01", "2000-01-02", "2002-12-31", "1980-03-01"]

birthdays = ModelTest.objects.get_jp_era_birthdays("heisei")
# ["2001-01-01", "2000-01-02", "2002-12-31"]

birthdays = ModelTest.objects.get_jp_era_birthdays("へいせい")
# ["2001-01-01", "2000-01-02", "2002-12-31"]
```

## Calculate age based on birthday

```Python
# id: 1
# ["1995-01-05"]

m = ModelTest.objects.filter(id=1).first()
birthday = m.get_age()
# 27
```

## Get the zodiac

```Python
# ["子", "丑", "寅", "卯", "辰", "巳", "午", "未", "申", "酉", "戌", "亥"]

# id: 1
# ["1995-01-05"]

m = ModelTest.objects.filter(id=1).first()
birthday = m.get_zodiac()
# 亥
```

## Get all birthdays from specified zodiac

```Python
# ["2001-01-01", "2000-01-02", "2002-12-31", "1980-03-01", "1995-02-01", "1995-12-01"]

birthdays = ModelTest.objects.get_zodiac_birthdays("亥")
# ["1995-02-01", "1995-12-01"]
```

## Years of the Japanese era

```Python
# id: 1
# ["1995-01-05"]

m = ModelTest.objects.filter(id=1).first()
birthday = m.get_jp_era_years()
# 31
```

## Get all user profiles within the next 30 days

```Python
# ["2001-01-01", "2000-01-02", "2002-12-31"]

jan1 = date(year=2010, month=1, day=1)
birthdays = ModelsTest.objects.get_upcoming_birthdays(after=jan1)
# ["2001-01-01", "2000-01-02"]
```

## Get all user profiles which have their birthday today

```Python
# ["2001-01-01", "2000-01-02", "2002-12-31", "1990-03-01", "1990-01-01"]

jan1 = date(year=2010, month=1, day=1)
birthdays = ModelsTest.objects.get_birthdays(jan1)

# ["2001-01-01", "1990-01-01"]
```

## Order the user profiles according to their birthday

```Python
# ["2001-01-01", "2000-01-02", "2002-12-31", "1990-03-01"]

jan1 = date(year=2010, month=1, day=1)
birthdays = ModelsTest.objects.order_by_birthday()
# ["2001-01-01", "2000-01-02", "1990-03-01", "2002-12-31"]
```

# Docs

- Documentation: https://django-jp-birthday.readthedocs.io.

# License

`django-jp-birthday` is released under the MIT license.

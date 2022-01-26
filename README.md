# django-jp-birthday

![https://pypi.python.org/pypi/django_jp_birthday](https://img.shields.io/pypi/v/django_jp_birthday.svg)

![https://img.shields.io/pypi/v/django_jp_birthday.svg](https://pypi.python.org/pypi/django_jp_birthday)

![https://readthedocs.org/projects/django-jp-birthday/badge/?version=latest](https://django-jp-birthday.readthedocs.io/en/latest/?version=latest)

![https://pyup.io/repos/github/shimakaze-git/django_jp_birthday/shield.svg](https://pyup.io/repos/github/shimakaze-git/django_jp_birthday/)

![https://img.shields.io/github/repo-size/shimakaze-git/django-jp-birthday](https://img.shields.io/github/repo-size/shimakaze-git/django-jp-birthday)
![https://img.shields.io/github/languages/code-size/shimakaze-git/django-jp-birthday](https://img.shields.io/github/languages/code-size/shimakaze-git/django-jp-birthday)
![https://codecov.io/gh/shimakaze-git/django-jp-birthday/branch/master/graph/badge.svg](https://codecov.io/gh/shimakaze-git/django-jp-birthday/branch/master/graph/badge.svg)
![https://img.shields.io/github/license/shimakaze-git/django-jp-birthday.svg](https://img.shields.io/github/license/shimakaze-git/django-jp-birthday.svg)

Django model for Japanese birthday.

- Free software: MIT license
- Documentation: https://django-jp-birthday.readthedocs.io.

# Features

- TODO

# Credits

This package was created with [Cookiecutter](https://github.com/audreyr/cookiecutter) and the [audreyr/cookiecutter-pypackage](https://github.com/audreyr/cookiecutter-pypackage) project template.

# Main

django-jp-birthday is a helper library to work with birthdays and ages in models.

Authored by `shimakaze_soft <https://github.com/shimakaze-git>`_,  and some great

`contributors <https://github.com/shimakaze-git/django-jp-birthday/contributors>`_.

# Installation

```Bash
$ pip install django-jp-birthday
$ python steup.py install
```


# Usage

```Python
from jp_birthday.models import BirthdayModel

class ModelsTest(BirthdayModel):

    class Meta:
        app_label = 'jp_birthday'
        ordering = ('pk',)
```

Get all user profiles within the next 30 days:

```Python
ModelsTest.objects.get_upcoming_birthdays()
```

Get all user profiles which have their birthday today:

```Python
ModelsTest.objects.get_birthdays()
```

Or order the user profiles according to their birthday:

```Python
ModelsTest.objects.order_by_birthday()
```

# Docs

django-jp-birthday [`docs`](https://github.com/shimakaze-git/django-jp-birthday#usage)

# License

`django-jp-birthday` is released under the MIT license.

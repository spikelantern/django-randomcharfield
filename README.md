# django-randomcharfield

## What's this?

This is a custom Django model field written as an alternative to UUIDs.

It works by base64-encoding 20 bytes (160 bits) from `urandom`, as recommended by Neil Madden's fantastic blog post, ["Moving away from UUIDs"](https://neilmadden.blog/2018/08/30/moving-away-from-uuids/)

## Installation

Use any package manager of choice. If using pip, install with this command:

```
pip install django-randomcharfield
```

## Usage

Add this to your model definition as follows:

```python
from django.db import models
from randomcharfield import (
    RandomCharField, generate_random_field,
)


class SomeModel(models.Model):
    uid = RandomCharField(default=generate_random_field)
```

Note that this doesn't make any assumptions about your current database state. That means you are responsible for creating the database index for this field, adding a uniqueness constraint, or making it a primary key.

If you have existing rows in your table and want to add a uniqueness constraint, you may want to set this field as nullable (i.e. passing in `null=True`) and to devise a plan to populate this. A good guide for such a plan is one written in the official Django documentation to deal with the same situation for `UUIDField`: https://docs.djangoproject.com/en/3.0/howto/writing-migrations/#migrations-that-add-unique-fields

## Notes

This isn't a lot of code, so you should probably be just copying the field to your project if you want customisations, rather than proposing changes.

## License

MIT

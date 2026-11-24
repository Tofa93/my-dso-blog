---
title: Development
sidebar_label: Development
sidebar_position: 2
description: Implementing product tags and improving the review form in Django.
---

# Development

## Product tags

I introduced a `Tag` model with a name and automatically managed `created_at` and `updated_at` timestamps. Products can have any number of tags, but tags are optional:

```python
class Tag(models.Model):
    name = models.CharField(max_length=50)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.name

# Field added to Product:
tags = models.ManyToManyField(Tag, blank=True)
```

I created and applied the database migration:

```bash
cd src
python manage.py makemigrations products
python manage.py migrate
```

## Product page and admin

In `products/templates/product.html`, I added a section below the rating summary and above the Buy button. Django's `{% for %}` and `{% empty %}` template tags display the assigned tags or **“no tags available”** when there are none.

I also registered the `Tag` model in Django Admin and added `list_filter = ("tags",)` to `ProductAdmin` so products can be filtered by tag.

## Review form

After a successful review, the form must clear the selected stars and comment. A one-time session flag resets the form after the redirect while preserving the existing behavior of pre-filling a user's review on regular page visits.

## Verification

- **45 Django tests passed** after adjusting the review form.
- Black, Flake8, and isort checks passed.
- Tags were tested both on the product page and in Django Admin.

```bash
cd src
python manage.py test
```

**Key learning:** A new feature should not break previously tested behavior. The existing review-form test helped reveal and fix a regression.

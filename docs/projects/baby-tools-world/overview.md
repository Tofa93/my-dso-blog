---
title: Baby Tools World
sidebar_label: Overview
sidebar_position: 1
description: A Django shop project featuring product tags, automated testing, and Docker deployment.
tags:
  - django
  - python
  - docker
---

# Baby Tools World

Baby Tools World is a small Django-based shop application that I extended as part of my DevSecOps training. The goal was to add **product tags**, improve the review form, and deploy the application in a Docker container on a Linux virtual server.

## Tech stack

| Area | Technology |
| --- | --- |
| Backend | Python 3.12, Django |
| Database | SQLite |
| Frontend | Django Templates, Bootstrap |
| Quality checks | Django tests, Black, Flake8, isort |
| Deployment | Docker, Linux, SSH, Gunicorn |

## Project documentation

- [Development](./development.md) — models, templates, Django Admin, and review form.
- [Deployment](./deployment.md) — Docker setup, configuration, and persistent data.

**Source code:** [Baby Tools World on GitHub](https://github.com/Tofa93/baby-tools-world/tree/add-product-tags)

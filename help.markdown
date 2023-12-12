---
layout: default
title: Getting Help
permalink: /help/
---

### Online Help
1. Piazza, CampusWire, ...

### Drop-In Office Hours

{% for person in site.people -%}
| [{{person.name}}](mailto:{{person.email}}) ({{person.role}}) | {{person.office_hours}} |
{% endfor %}

- If our regular office hours don't match your schedule, please contact us on Piazza to make an appointment at a mutually available time.

### CS Tutoring Center

The [Computer Science Tutoring Center](https://tutoringcenter.cs.usfca.edu/) is a great resource to get help from other students.

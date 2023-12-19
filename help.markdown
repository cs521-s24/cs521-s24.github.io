---
layout: default
title: Getting Help
permalink: /help/
---

### Online Help
1. All registered students have received an invitation to our CampusWire forum
1. To get help, please **post a question** to CampusWire. We will use unresolved questions as a to-do list.
1. Please post to the class feed so everyone benefits from seeing the questions and answers.
1. Feel free to answer each others' questions so CW is a valuable forum for all. 
1. For questions about your grade or personal circumstances, please post your question to **Instructors & TAs**. 
1. Please do not use Direct Messages or email to ask questions about course material. It's too hard to keep track of those.

### Drop-In Office Hours

{% for person in site.people -%}
| [{{person.name}}](mailto:{{person.email}}) ({{person.role}}) | {{person.office_hours}} |
{% endfor %}

If our regular office hours don't match your schedule, please contact us on CampusWire to make an appointment at a mutually available time.

### CS Tutoring Center

The [Computer Science Tutoring Center](https://tutoringcenter.cs.usfca.edu/) is a great resource to get help from other students.

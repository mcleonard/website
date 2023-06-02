---
layout: post
title:  "My new Python library, Synthwave"
date:   2023-06-02 14:00:00 -0700
categories: Python data
---

As I write this I'm searching for a new job. At my previous place, my favorite projects were data engineering work. There's something about getting a request from the marketing team for some data, figuring out where to get it from, formatting it, and delivering the records to them. I like helping people and I get to do it with data and code!

So, I'm putting time into improving my data engineering skillz. All the courses and other content I'm finding online don't go beyond the basics though. They cover Python, SQL, data modeling, Spark, etc., things I already pretty much know. But I need more experience, as much as I can get.

The big looming problem here is data. How do I get experience building data pipelines with verification and quality checks and data warehousing and all the tools if I'm working solo without a source of data? All of this, all of the skills and technology and tools require a data source, preferably something exactly what you'd see from a real product.

To handle this, I built [Synthwave](https://mcleonard.github.io/synthwave/html/index.html), a Python library that generates a stream of synthetic data. I made it so the data is equivalent to what you would get from services like Segment, RudderStack, and Amplitude. I also focused on making it simple and intuitive to define the data fields and structures you need.

First you define your events in a file, say `events.py`:

```python
from synthwave import Event, field

class AccountCreated(Event):
   user_id = field.UUID()

   properties = field.Object(
      first_name=field.GivenName(),
      last_name=field.FamilyName(),
      age=field.Integer(13, 95),
      email_address=field.EmailAddress(),
      location=field.Location() | field.Null(0.2),
   )
```

Then you start Synthwave by pointing to the event file in your terminal:  
`python -m synthwave -e events.py -o stdout`

This will generate a stream of event data like:

```
{
   'event': 'account_created',
   'event_id': '24a4f6ae-06dc-4df9-b67d-faac490ce890',
   'timestamp': '2023-05-25T15:22:55.419+00:00',
   'user_id': 'b18a2f0e-7257-41c0-8f1c-9c63c275b342',
   'properties': {
      'first_name': 'Parron',
      'last_name': 'Akori',
      'age': 95,
      'email_address': 'cleon@anache.net',
      'location': None
   }
}
```

The events can be sent to the terminal, a file, or to a URL with a POST request. Read [the documentation](https://mcleonard.github.io/synthwave/html/index.html) to learn more about using Synthwave.

This is a good start as a simple way to generate data with the fields and structure you need for testing, prototyping, or learning. I'm planning on adding more fields as well as a way to generate multiple streams of data in parallel.
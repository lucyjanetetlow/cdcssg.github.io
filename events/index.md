---
title: Events
sitemap:
  priority: 0.8
description: Details of the Cri du Chat Syndrome Support Group events
keywords: conference meetup
---

<a href='calendar.ics' class='btn btn-primary pull-right'>
  <i class='fa fa-calendar'></i>
  Add to your calendar
</a>

The group supports a number of regional and national events.

## Regional Meetups

Regional meetups are a great way to meet families near you, especially for new families for whom the family weekends can be very daunting! We want to support more and more regional meetups, and will pay the costs, but we need people with local knowledge to organise them. If you'd like to make one happen for families near you, read our [guide to running a meetup](meetups.html).

## Family Weekends

Our support group has been holding family weekends since the early 1990s. They are the only national event in the UK that is held specifically for the families, carers and professionals interested in Cri du Chat Syndrome. With a mixture of social and informational activities, they are always popular!

## Upcoming Events
{% assign events = site.events | sort: "end" %}
<ul class="thumbnails events">
  {% for event in events %}
    {% if event.end >= site.time %}
      {% include event_thumbnail.html %}
    {% endif %}
  {% endfor %}
</ul>

## Past Events
{% assign events = site.events | sort: "end" | reverse %}
<ul class="thumbnails events">
  {% for event in events %}
    {% if event.end < site.time %}
      {% include event_thumbnail.html %}
    {% endif %}
  {% endfor %}
</ul>


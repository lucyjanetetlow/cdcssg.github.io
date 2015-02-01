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

## Regional Meetups

blah

## Family Weekends

Our support group has been holding family weekends since the early 1990s and is the only event in the UK that is held specifically for the families, carers and professionals interested in Cri du Chat Syndrome.

## Upcoming Events
{% assign events = site.events | sort: "end" %}
<div class="row">
  <div class="col-sm-6 col-md-4">
    {% for event in events %}
      {% if event.end >= site.time %}
        {% include event_thumbnail.html %}
      {% endif %}
    {% endfor %}
  </div>
</div>

## Past Events
{% assign events = site.events | sort: "end" | reverse %}
<div class="row">
  <div class="col-sm-6 col-md-4">  
    {% for event in events %}
      {% if event.end < site.time %}
        {% include event_thumbnail.html %}
      {% endif %}
    {% endfor %}
  </div>
</div>


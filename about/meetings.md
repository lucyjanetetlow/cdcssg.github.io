---
title: Meetings
description: Cri du Chat Syndrome Support group committee meeting details and minutes
---

## Upcoming Meetings
{% assign meetings = site.meetings | sort: "date" %}
<ul class="thumbnails meetings">
  {% for meeting in meetings %}
    {% if meeting.date >= site.time %}
      {% include meeting_thumbnail.html %}
    {% endif %}
  {% endfor %}
</ul>

## Past Meetings
{% assign meetings = site.meetings | sort: "date" | reverse %}
<ul class="thumbnails meetings">
  {% for meeting in meetings %}
    {% if meeting.date < site.time %}
      {% include meeting_thumbnail.html %}
    {% endif %}
  {% endfor %}
</ul>


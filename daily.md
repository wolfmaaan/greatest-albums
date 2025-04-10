---
layout: default
title: Album of the Day
---

{% assign all_albums = site.data.albums %}
{% assign album_count = all_albums | size %}
{% assign today_string = site.time | date: "%Y%m%d" %}
{% assign index = today_string | modulo: album_count %}
{% assign daily_album = all_albums[index] %}

<div class="album-of-the-day" style="border: 1px solid #ccc; padding: 1rem; border-radius: 0.5rem;">
  <h2>Album of the Day</h2>
  <p><strong>{{ daily_album.title }}</strong> by {{ daily_album.artist }}</p>
  {% if daily_album.cover %}
    <img src="{{ daily_album.cover }}" alt="Album cover for {{ daily_album.title }}" style="max-width: 100%; height: auto;">
  {% endif %}
  {% if daily_album.url %}
    <p><a href="{{ daily_album.url }}">More about this album →</a></p>
  {% endif %}
</div>

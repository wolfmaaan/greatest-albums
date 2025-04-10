---
layout: default
title: Greatest Albums of All Time - Album of the Day
---

{% assign all_albums = site.data.albums %}
{% assign album_count = all_albums | size %}
{% assign today_string = site.time | date: "%Y%m%d" %}
{% assign index = today_string | modulo: album_count %}
{% assign daily_album = all_albums[index] %}

<div class="album-of-the-day" style="border: 1px solid #ccc; padding: 1rem; border-radius: 0.5rem; text-align: center;">
  <h2>Album of the Day</h2>
  <p><strong>{{ daily_album.title }}</strong> by {{ daily_album.artist }}</p>
  {% if daily_album.cover %}
    <img src="{{ daily_album.cover }}" alt="Album cover for {{ daily_album.title }}" style="max-width: 100%; height: auto; margin: 1rem auto; display: block;">
  {% endif %}
  {% if daily_album.link %}
    <p><a href="{{ daily_album.link }}" target="_blank">More about this album :information_source:</a></p>
  {% endif %}
  {% if daily_album.youtube %}
    <p><a href="{{ daily_album.youtube }}" target="_blank">Listen on YouTube :tv:</a></p>
  {% endif %}
</div>

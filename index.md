---
layout: default
title: Greatest Albums of All Time
---

<h1>🎶 Greatest Albums of All Time</h1>
<p>A curated list of the most iconic albums in music history. Click each title to learn more.</p>

<div class="album-list">
  {% for album in site.data.albums %}
    <div class="album">
      <img src="{{ album.cover }}" alt="{{ album.title }} cover" class="album-cover">
      <h2><a href="{{ album.link }}" target="_blank">{{ album.title }}</a></h2>
      <p><strong>Artist:</strong> {{ album.artist }}</p>
      <p><strong>Year:</strong> {{ album.year }}</p>
    </div>
  {% endfor %}
</div>

<style>
.album-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1.5rem;
}
.album {
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 10px;
  text-align: center;
  background-color: #fafafa;
}
 
  width: 100%;
}
  height: auto;
  border-radius: 8px;
</style>

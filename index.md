---
layout: default
title: Greatest Albums of All Time
---

<h1>🎶 Greatest Albums of All Time</h1>
<p class="intro">A curated list of the most iconic albums in music history. Click each title to learn more.</p>

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
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap');

body {
  font-family: 'Inter', sans-serif;
  background-color: #f9f9fb;
  color: #1f2937;
  margin: 0;
  padding: 2rem;
}

h1 {
  font-size: 2.25rem;
  margin-bottom: 0.5rem;
  color: #111827;
}

.intro {
  font-size: 1.1rem;
  color: #4b5563;
  margin-bottom: 2rem;
}

.album-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 2rem;
}

.album {
  background: #ffffff;
  border: 1px solid #e5e7eb;
  border-radius: 12px;
  padding: 1rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.album:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 12px rgba(0, 0, 0, 0.08);
}

.album-cover {
  width: 100%;
  height: auto;
  border-radius: 8px;
  margin-bottom: 1rem;
}

.album h2 {
  font-size: 1.25rem;
  margin: 0.5rem 0;
  color: #2563eb;
}

.album h2 a {
  text-decoration: none;
}

.album h2 a:hover {
  text-decoration: underline;
}
</style>
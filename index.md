---
layout: default
title: Greatest Albums of All Time
---

<h1>Greatest Albums of All Time</h1>
<p>A community curated list of the most iconic albums in music history. Only the best of the best. Nostalgia, sentiment, connection, experience, aesthetic pleasure. It all plays a part. There are no rules. Cardiacs taught us that.</p>

{% assign album_count = site.data.albums | size %}
<p>Total albums submitted: {{ album_count }}</p>

<input type="text" id="searchInput" placeholder="Search albums..." onkeyup="filterAlbums()">
<select id="sortSelect" onchange="sortAlbums()">
  <option value="title">Sort by Title</option>
  <option value="artist">Sort by Artist</option>
  <option value="year">Sort by Year</option>
</select>

<div class="album-list">
  {% for album in site.data.albums %}
    <div class="album">
      <img src="{{ album.cover }}" alt="{{ album.title }} cover" class="album-cover">
      <h2 class="title"><a href="{{ album.link }}" target="_blank">{{ album.title }}</a></h2>
      <p class="artist"><strong>Artist:</strong> {{ album.artist }}</p>
      <p class="year"><strong>Year:</strong> {{ album.year }}</p>
    </div>
  {% endfor %}
</div>

<style>
.album-list {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 1.5rem;
  margin-top: 1rem;
}
.album {
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 10px;
  text-align: center;
  background-color: #fafafa;
}
.album-cover {
  width: 100%;
  height: auto;
  border-radius: 8px;
}
input, select {
  margin: 1rem 0.5rem 1rem 0;
  padding: 0.5rem;
}
</style>

<script>
function filterAlbums() {
  let input = document.getElementById('searchInput').value.toLowerCase();
  let albums = document.querySelectorAll('.album');
  albums.forEach(album => {
    const text = album.textContent.toLowerCase();
    album.style.display = text.includes(input) ? '' : 'none';
  });
}

function sortAlbums() {
  const criteria = document.getElementById('sortSelect').value;
  const container = document.querySelector('.album-list');
  const albums = Array.from(container.children);

  albums.sort((a, b) => {
    let aVal = a.querySelector(`.${criteria}`).textContent.toLowerCase();
    let bVal = b.querySelector(`.${criteria}`).textContent.toLowerCase();
    return aVal.localeCompare(bVal);
  });

  albums.forEach(album => container.appendChild(album));
}
</script>

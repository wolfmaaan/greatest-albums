---
layout: default
title: Album of the Day
---

{% assign all_albums = site.data.albums %}

<div class="album-of-the-day" style="border: 1px solid #ccc; padding: 1rem; border-radius: 0.5rem; text-align: center;">
  <h2>Album of the Day</h2>
  <p><strong id="title"></strong> by <span id="artist"></span></p>
  <img id="cover" hidden src="" alt="Album cover" style="max-width: 100%; height: auto; margin: 1rem auto; display: block;">
  <p><a hidden id="link" target="_blank">More about this album</a></p>
  <p><a hidden id="review" href="" target="_blank">Read a review</a></p>
  <p><a hidden id="youtube" href="" target="_blank">Listen on YouTube</a></p>
</div>

<script>
  function show(id) {
    document.getElementById(id).hidden = false;
  }

  function set(id, field, value) {
    if (value) {
      document.getElementById(id)[field] = value;
      show(id);
    }
  }

  function setLink(id, link) {
    set(id, 'href', link);
  }

  function setImage(id, src) {
    set(id, 'src', src);
  }

  function setText(id, text) {
    set(id, 'innerHTML', text);
  }

  async function setHash(album) {
    const msgUint8 = new TextEncoder().encode(`${album.title}-${album.artist}`);
    const hashBuffer = await crypto.subtle.digest('SHA-256', msgUint8);
    const hashArray = Array.from(new Uint8Array(hashBuffer))                    
    const hashHex = hashArray.map(b => b.toString(16).padStart(2, '0')).join('')
    album.hash = hashHex;
  }

  async function pickDailyAlbum() {
    let allAlbums = {{ all_albums | jsonify }};
    const albumCount = allAlbums.length;

    const date = new Date();
    const dateNumber = Math.floor(date.getTime() / 1000 / 86400);
    const index = dateNumber % albumCount;
    await Promise.all(allAlbums.map(x => setHash(x)));
    allAlbums.sort((a, b) => a.hash < b.hash ? 1 : -1);

    const dailyAlbum = allAlbums[index];

    return dailyAlbum;
  }

  window.onload = async function() {
    const dailyAlbum = await pickDailyAlbum();

    setText('title', dailyAlbum.title);
    setText('artist', dailyAlbum.artist);
    setImage('cover', dailyAlbum.cover);
    setLink('link', dailyAlbum.link);
    setLink('review', dailyAlbum.review);
    setLink('youtube', dailyAlbum.youtube);
  }
</script>

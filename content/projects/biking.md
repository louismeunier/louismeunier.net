---
title: "🚲 biking"
# date: 2020-11-26
description: An interactive map and analyzer of my bike rides.
weight: 1

---


<div class="image-wrapper">
<img src="/images/bike.png" alt="Preview of my biking website" height="400px" />
</div>


<div class="links">
<a class="fake-button" href="https://github.com/louismeunier/biking">
<button class="btn btn-info">source code</button>
</a>

<a class="fake-button" href="https://bike.louismeunier.net">
<button class="btn btn-info">live site</button>
</a>
</div>

An interactive map and analyzer of my bike rides. Data is automatically updated every time I enter a ride into Strava. The map is created with [Leaflet](https://leafletjs.com/), the site is made with [Svelte](https://svelte.dev/), and the data is automatically synced to [Firesbase](https://firebase.google.com/) from [Strava's API](https://developers.strava.com/).

<iframe class="website-preview" src="https://bike.louismeunier.net" width="100%" height="550px"></iframe>
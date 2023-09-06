<template>
  <div class="playlist-data-container">
    <p class="playlist-data-label">Playlist Data:</p>
    <pre>{{ playlists }}</pre>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Playlists',
  data() {
    return {
      playlists: []
    }
  },
  created() {
    const spotifyAccessToken = localStorage.getItem('SPOTIFY_ACCESS_TOKEN')
    if (spotifyAccessToken) {
      return axios.get('https://api.spotify.com/v1/me/playlists', { headers: { Authorization: `Bearer ${spotifyAccessToken}` } } )
        .then(playlists => {
          this.playlists = playlists.data.items
        })
    }
    else {
      return this.$router.push('/')
    }
  }
}
</script>

<style scoped>
.playlist-data-container {
  border: 1px solid black;
  padding-left: 25px;
  padding-right: 25px;
  width: fit-content;
}

.playlist-data-label {
  font-size: 25px;
}
</style>
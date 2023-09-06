<template>
  <div>
    <h3>Home</h3>
    <button @click="loginToSpotify">Login to Spotify</button>
  </div>
</template>

<script>
export default {
  name: 'Home',
  methods: {
    loginToSpotify() {
      const codeVerifier = this.generateRandomString(128)
      return this.generateCodeChallenge(codeVerifier)
        .then(codeChallenge => {
          const state = this.generateRandomString(16)
          const scope = 'playlist-read-private playlist-read-collaborative playlist-modify-private playlist-modify-public'

          localStorage.setItem('code_verifier', codeVerifier)

          const args = new URLSearchParams({
            response_type: 'code',
            client_id: process.env.VUE_APP_CLIENT_ID,
            scope: scope,
            redirect_uri: process.env.VUE_APP_REDIRECT_URI,
            state: state,
            code_challenge_method: 'S256',
            code_challenge: codeChallenge
          })

          window.location = 'https://accounts.spotify.com/authorize?' + args
        })
    },
    generateRandomString(length) {
      let text = ''
      const possible = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789'

      for (let i = 0; i < length; i++) {
        text += possible.charAt(Math.floor(Math.random() * possible.length))
      }
      return text
    },
    generateCodeChallenge(codeVerifier) {
      const encoder = new TextEncoder()
      const data = encoder.encode(codeVerifier)
      return window.crypto.subtle.digest('SHA-256', data)
        .then(digest => this.base64encode(digest))
    },
    base64encode(string) {
      return btoa(String.fromCharCode.apply(null, new Uint8Array(string)))
        .replace(/\+/g, '-')
        .replace(/\//g, '_')
        .replace(/=+$/, '')
    }
  }
}
</script>

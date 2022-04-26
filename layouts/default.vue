<template>

  <v-app dark>

    <v-main>

      <v-container>

        <Nuxt />

      </v-container>

    </v-main>

    <v-footer v-if="this.discord_loaded" elevation="10" app>

      <div :class="'status-icon status-' + this.discord.discord_status" />

      <span>

        {{

          this.discord.discord_status === 'dnd'

          ? 'Do not disturb' :

          this.discord.discord_status.charAt(0).toUpperCase() + this.discord.discord_status.slice(1)

        }}

      </span>

      <div class="spotify-status">

        <v-icon size="20">mdi-headphones</v-icon>

        <a v-if="this.discord.listening_to_spotify" :href="'https://open.spotify.com/track/' + this.discord.spotify.track_id" class="spotify-link">

            Listening to <b>{{this.discord.spotify.song}}</b> by <b>{{this.discord.spotify.artist}}</b>

        </a>

        <span v-else>

          Not listening to anything

        </span>

      </div>

    </v-footer>

  </v-app>

</template>

<script>

import axios from 'axios'

export default {

  data: () => ({

    discord: null,

    discord_loaded: false

  }),

  head: () => ({

    title: 'Kappug.dev'

  }),

  created() {

    this.gS()

    setInterval(this.gS, 5000)

  },

  methods: {

    gS() {

      axios.get('https://api.lanyard.rest/v1/users/715541337549570114')

        .then(r => {this.discord = r.data.data;this.discord_loaded = true})

    }

  }

}

</script>

<style scoped>

.status-icon {

  width: .75rem;

  height: .75rem;

  border-radius: 50%;

  margin-right: 6px;

}

.status-online {

  background-color: #3ba55d;

}

.status-idle {

  background-color: #faa81a;

}

.status-dnd {

  background-color: #ed4245;

}

.status-offline {

  background-color: #6d7985;

}

.spotify-status {

  right: 16px;

  max-width: 65%;

  margin-bottom: auto;

  position: absolute;

}

.spotify-link {

  color: white;

  text-decoration: none;

}

.spotify-link:hover {

  text-decoration: underline;

}

.v-footer {

  min-height: 6vh

}

</style>

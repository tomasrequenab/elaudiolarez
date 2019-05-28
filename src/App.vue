<template lang="pug">
#app
  h1 El Audio Larez

  select(v-model="selectedCountry")
    option(v-for="country in countries" :value="country.value") {{ country.name }}

  spinner(v-show="loading")

  ul
    artist(v-for="artist in artists" :artist="artist" :key="artists.indexOf(artist)")
</template>

<script>
import getArtists from './api/requests'

import Artist from './components/Artist'
import Spinner from './components/Spinner'

export default {
  name: "app",
  components: {
    Artist,
    Spinner
  },
  data() {
    return {
      countries: [
        { name:"Venezuela", value:"venezuela" },
        { name:"Francia", value:"france" },
        { name:"España", value:"spain" },
      ],
      selectedCountry: 'venezuela',
      loading: true,
      artists: []
    }
  },
  methods: {
    fetch: function() {
      const self = this
      this.loading = true
      this.artists = []
      getArtists(this.selectedCountry)
        .then(function(artists) {
          self.loading = false
          self.artists = artists
        })
    }
  },
  mounted () {
    this.fetch()
  },
  watch: {
    selectedCountry() {
      this.fetch()
    }
  }
}
</script>

<style lang="stylus">
#app
  font-family "Avenir", Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #212121
  margin-top 60px

h1,
h2
  font-weight normal

ul
  list-style-type none
  padding 0

li
  display inline-block
  margin 0 10px

a
  color blue
</style>

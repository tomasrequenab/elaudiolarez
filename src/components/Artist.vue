<template lang="pug">
li
  h2: a(:href="artist.url" target="_blank") {{ artist.name }}
  img(:src="artist.image[2]['#text']")
</template>

<script>

export default {
  name: "artist",
  props: {
    artist: {
      type: Object,
      required: true
    }
  }
}
</script>

<style lang="stylus">
li
  margin 10px
</style>

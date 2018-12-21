<template>
  <div id="app">
    <h1>Player</h1>
    <Search />
    <Controller :currentTrack="currentTrack" />
    <Playlist
      :list="list"
      @changeTrack="changeTrack"
      />
  </div>
</template>

<script>
  import Search from './Search.vue';
  import Controller from './Controller.vue';
  import Playlist from './Playlist.vue';
  import axios from 'axios';

  export default {
    components: {
      Search,
      Controller,
      Playlist,
    },
    data: () => {
      return {
        list: [],
        currentTrack: { creator: '', title: '', location: '' },
      }
    },
    mounted: function() {
      axios.get('http://vip.aersia.net/roster.xml')
        .then((response) => {
          const parser = new DOMParser();
          const doc = parser.parseFromString(response.data, 'application/xml');
          [].slice.call(doc.getElementsByTagName('track')).forEach((track) => {
            this.list.push({
              creator: track.childNodes[1].innerHTML,
              title: track.childNodes[3].innerHTML,
              location: track.childNodes[5].innerHTML,
            });
          });
        });
    },
    methods: {
      changeTrack(currentTrack) {
        this.currentTrack = currentTrack;
      },
    },
  }
</script>

<!-- CSS libraries -->
<style src="normalize.css/normalize.css"></style>

<!-- Global CSS -->
<style lang="scss">
@import './variables.scss';

#app {
  max-width: 400px;
  margin: 0 auto;
  line-height: 1.4;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  color: $vue-blue;
}
</style>

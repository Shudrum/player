<template>
  <div id="playlist">
    <Track
      v-for="track in list"
      :key="track.id"
      :track="track"
      @play="$emit('changeTrack', $event)"
    />
  </div>
</template>

<script>
  import Track from './Track.vue';

  export default {
    components: {
      Track,
    },
    props:
    [
      'list',
    ],
  };
</script>

<style lang="scss">
</style>

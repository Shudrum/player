<template>
  <div @click="$emit('play', track)">
    {{ track.creator }} - {{ track.title }}
  </div>
</template>

<script>
  export default {
    props: [
      'track',
    ],
  };
</script>

<style lang="scss">
</style>
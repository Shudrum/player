<template>
  <div>
    <div>{{ currentTrack.title }}</div>
    <audio
      :src="currentTrack.location"
      ref="audioObject"
    />
    <button @click="playAudio">Play</button>
    <button @click="pauseAudio">Pause</button>
    <div id="progress">
      <div :style="styleObject"></div>
    </div>
  </div>
</template>

<script>
  export default {
    props: [
      'currentTrack',
      'value',
    ],
    data: function() {
      return { progress: 0, interval: null };
    },
    watch: {
      currentTrack: function() {
        this.playAudio();
      }
    },
    computed: {
      styleObject() {
        return {
          width: `${this.progress * 100}%`,
        };
      },
    },
    methods: {
      playAudio() {
        console.log(this.$refs.audioObject);
        this.$refs.audioObject.play();
      },
      pauseAudio() {
        this.$refs.audioObject.pause();
      },
    },
    mounted() {
      this.interval = setInterval(() => {
        this.progress = (this.$refs.audioObject.currentTime / this.$refs.audioObject.duration);
      }, 100);
      
    },
    beforeDestroy() {
      clearInterval(this.interval);
    },
  };
</script>

<style lang="scss">
#progress {
  height: 10px;
  > div {
    height: 100%;
    background-color: aquamarine;
  }
}
</style>
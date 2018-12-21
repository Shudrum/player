<template>
  <form>
        <input 
          type="search"
          name="search"
          v-on:change="handleChange"
        />
        <input type="submit" />
      </form>
</template>

<script>
  export default {
    props: [
      
    ],
    data: () => {
      return { value: '' };
    },
    methods: {
      handleChange(e) {
        value: e.target.value
      },
    },
  };
</script>
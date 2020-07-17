<template>
  <div class="home">
    <form action="">
      <label for="">
        Search:
        <input v-model="tag" type="text">
      </label>
      <button type="submit" class="go-button" @click.prevent="search">Search</button>
    </form>
  </div>
</template>

<script>

export default {
  name: 'Home',
  data() {
    return {
      tag: '',
    };
  },
  methods: {
    search() {
      // eslint-disable-next-line no-console
      console.log('Searching for: ', this.tag);
    },
  },
};
</script>

<template>
  <div class="home">
    <form action="">
      <label for="">
        Search:
        <input v-model="tag" type="text">
      </label>
      <button type="submit" class="go-button" @click.prevent="search">Search</button>
    </form>
    <p v-if="loading">Loading...</p>
    <ul v-else>
      <li v-for="image in images" :key="image.id">{{image}}</li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios';
import config from '../../config';

export default {
  name: 'Home',
  data() {
    return {
      loading: false,
      tag: '',
      images: [],
    };
  },
  methods: {
    search() {
      this.loading = true;
      this.fetchImages().then((response) => {
        this.images = response.data.photos.photo;
        this.loading = false;
      });
    },
    fetchImages() {
      return axios({
        method: 'get',
        url: 'https://flickr.com/service/rest/',
        params: {
          method: 'flickr.photos.search',
          api_key: config.api_key,
          tags: this.tag,
          extras: 'url_n,owner_name,date_taken,views',
          page: 1,
          format: 'json',
          nojsoncallback: 1,
          per_page: 35,
        },
      });
    },
  },
};
</script>

<template>
  <div>
    <div class="wrapper" id="page">
      <site-header />
      <p v-if="loading" class="text-centered">
        Loading...
      </p>
      <div v-else class="masonry">
        <image-card v-for="image in cleanImages" :key="image.id" :image="image" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import config from '../../config';
import SiteHeader from '../components/SiteHeader.vue';
import ImageCard from '../components/ImageCard.vue';

export default {
  name: 'home',
  components: {
    SiteHeader,
    ImageCard,
  },
  data() {
    return {
      loading: false,
      images: [],
    };
  },
  methods: {
    loadImages() {
      this.loading = true;
      this.fetchImages()
        .then((response) => {
          this.images = response.data.photoset.photo;
          this.loading = false;
        })
        .catch((error) => {
          console.log('An error ocurred: ', error);
        });
    },
    fetchImages() {
      return axios({
        method: 'get',
        url: 'https://api.flickr.com/services/rest',
        params: {
          method: 'flickr.photosets.getPhotos',
          api_key: config.api_key,
          photoset_id: config.photoset,
          extras: 'url_n, url_o, owner_name, date_taken, views',
          page: 1,
          format: 'json',
          nojsoncallback: 1,
          per_page: 30,
        },
      });
    },
  },
  beforeMount() {
    this.loadImages();
  },
  computed: {
    cleanImages() {
      return this.images.filter((image) => image.url_n);
    },
  },
};
</script>

<style lang="scss">
.text-centered {
  text-align: center;
}
.wrapper {
  margin: 0 auto;
  max-width: 1200px;
  @media only screen and (max-width: 799px) {
    max-width: 100%;
    margin: 0 1.5rem;
  }
}
.masonry {
  margin: 1.5em auto;
  max-width: 1200px;
  column-gap: 1.5em;
}

@media only screen and (min-width: 1024px) {
  .masonry {
    column-count: 3;
  }
}

/* Masonry on medium-sized screens */
@media only screen and (max-width: 1023px) and (min-width: 768px) {
  .masonry {
    column-count: 2;
  }
}

/* Masonry on small screens */
@media only screen and (max-width: 767px) and (min-width: 540px) {
  .masonry {
    column-count: 1;
  }
}
</style>

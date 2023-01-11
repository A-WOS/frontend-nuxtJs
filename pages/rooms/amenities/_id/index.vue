<template>
  <main class="container my-5">
    <div class="row">
      <div class="col-12 text-center my-3">
        <h2 class="mb-3 display-4 text-uppercase">{{ amenity.name }}</h2>
      </div>
      <div class="col-md-6">
        <div class="recipe-details">
          <h4>Description</h4>
          <p>{{ amenity.description }}</p>
        </div>
      </div>
      <div>
        <nuxt-link class="btn btn-outline btn-large btn-info" to="/rooms/amenities">뒤로가기</nuxt-link>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "index",
  head() {
    return {
      title: "View Amenity"
    };
  },
  async asyncData({ $axios, params }) {
    try {
      console.log(params)
      let amenity = await $axios.$get(`/rooms/amenities/${params.id}`);
      return { amenity };
    } catch (e) {
      return { amenity: [] };
    }
  },
  data() {
    return {
      amenity: {
        name: "",
        description: "",
      }
    };
  }
};
</script>

<style scoped>
</style>

<template>
  <main class="container mt-5">
    <div class="row">
      <div class="col-12 text-right mb-4">
        <div class="d-flex justify-content-between">
          <h3>Amenities</h3>
          <nuxt-link to="/rooms/amenities/add" class="btn btn-info">Add Amenity</nuxt-link>
        </div>
      </div>
      <template v-for="amenity in amenities">
        <div :key="amenity.pk" class="col-lg-3 col-md-4 col-sm-6 mb-4">
          <amenity-card :onDelete="deleteAmenity" :amenity="amenity"></amenity-card>
        </div>
      </template>
    </div>
  </main>
</template>

<script>
import AmenityCard from "@/components/AmenityCard.vue";

export default {
  head() {
    return {
      title: "Amenity list"
    };
  },
  components: {
    AmenityCard
  },
  async asyncData({$axios, params}) {
    try {
      let amenities = await $axios.$get('/rooms/amenities');
      console.log("params: ", params)
      return {amenities};
    } catch (e) {
      return {amenities: []};
    }
  },
  data() {
    return {
      amenities: []
    };
  },
  methods: {
    async deleteAmenity(amenity_pk) {
      try {
        console.log(amenity_pk);
        await this.$axios.$delete(`/rooms/amenities/${amenity_pk}`); // delete amenity
        // await this.$axios
          // .delete(`/rooms/amenities/${amenity_pk}`); // delete amenity
          // .then(() => {
          //   alert("삭제가 완료되었습니다.");
          //   this.$router.push("/rooms/amenities");// 삭제 후 이동
          // })

        let newAmenities = await this.$axios.$get("/rooms/amenities"); // get new list of amenities
        console.log(newAmenities)
        this.amenities = newAmenities; // update list of amenities
      } catch (e) {
        console.log(e);
      }
    }
  }
};
</script>

<style scoped>
</style>

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
        <div :key="amenity.id" class="col-lg-3 col-md-4 col-sm-6 mb-4">
          <amenity-card :onDelete="deleteAmenity" :amenity="amenity"></amenity-card>
        </div>
      </template>
    </div>
  </main>
</template>

<script>
import AmenityCard from "@/components/AmenityCard.vue";

const sampleData = [
  {
    id: 1,
    name: "Shower",
    description: "two shower booths",
  },
  {
    id: 2,
    name: "kitchen",
    description: "cook",
  },
  {
    id: 3,
    name: "amazing rooms",
    description: "Three rooms"
  }
];

export default {
  head() {
    return {
      title: "Amenity list"
    };
  },
  components: {
    AmenityCard
  },
  asyncData(context) {
    let data = sampleData;
    return {
      amenities: data
    };
  },
  data() {
    return {
      amenities: []
    };
  },
  methods: {
    deleteAmenity(amenity_id) {
      console.log(deleted `${amenity.id}`)
    }
  }
};
</script>

<style scoped>
</style>

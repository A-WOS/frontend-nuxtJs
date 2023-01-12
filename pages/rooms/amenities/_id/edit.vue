<template>
  <main class="container my-5">
    <div class="row">
      <div class="col-12 text-center my-3">
        <h2 class="mb-3 display-4 text-uppercase">{{ amenity.name }}</h2>
      </div>
      <div class="col-md-4">
        <form @submit.prevent="submitAmenity">
          <div class="form-group">
            <label for>편의시설명</label>
            <input type="text" class="form-control" v-model="amenity.name">
          </div>
          <div class="form-group">
            <label for>상세 설명</label>
            <input type="text" v-model="amenity.description" class="form-control" name="Description">
          </div>
          <button type="submit" class="btn btn-success">저장</button>
        </form>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "edit",
  head(){
      return {
        title: "Edit Amenity"
      }
    },
  async asyncData({ $axios, params }) {
    try {
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
      },
    };
  },
  methods: {
    async submitAmenity() {
      let editedAmenity = this.amenity;

      const config = {
        headers: { "content-type": "multipart/form-data" }
      };
      let formData = new FormData();
      for (let data in editedAmenity) {
        formData.append(data, editedAmenity[data]);
        console.log("data: ", data)
        console.log("editedAmenity[data]: ", editedAmenity[data])
      }
      console.log("editedAmenity: ", editedAmenity);
      try {
        let response = await this.$axios.$put(`/rooms/amenities/${editedAmenity.pk}`, formData, config);
        console.log("response: ", response);
        await this.$router.push(`/rooms/amenities/`);
      } catch (e) {
        console.log(e);
      }
    }
  }

}
</script>

<style scoped>

</style>

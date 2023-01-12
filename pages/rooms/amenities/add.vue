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
            <input v-model="amenity.description" type="text" class="form-control">
          </div>
          <button type="submit" class="btn btn-primary">확인</button>
        </form>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: "add",
  head() {
    return {
      title: "Add Amenity"
    };
  },
  data() {
    return {
      amenity: {
        name: "",
        description: ""
      },
    };
  },
  methods: {
    async submitAmenity() {
      const config = {
        headers: {"content-type": "multipart/form-data"}
      };
      let formData = new FormData();
      for (let data in this.amenity) {
        formData.append(data, this.amenity[data]);
      }
      try {
        await this.$axios.$post("/rooms/amenities/", formData, config);
        await this.$router.push("/rooms/amenities/");
      } catch (e) {
        console.log(e);
      }
    }
  }
};
</script>

<style scoped>

</style>

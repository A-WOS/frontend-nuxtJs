<template>
  <div class="card amenity-card">
    <div class="card-body">
      <h5 class="card-title">Name: {{ amenity.name }}</h5>
      <div class="action-buttons">
        <nuxt-link :to="`/rooms/amenities/${amenity.pk}/`" class="btn btn-sm btn-success">View</nuxt-link>
        <nuxt-link :to="`/rooms/amenities/${amenity.pk}/edit/`" class="btn btn-sm btn-primary">편집</nuxt-link>
        <button @click="onDelete(amenity.pk)" class="btn btn-sm btn-danger">삭제</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["amenity", "onDelete"],
  name: "AmenityCard"
};
</script>

<style>
.amenity-card {
  box-shadow: 0 1rem 1.5rem rgba(0, 0, 0, .6);
}
</style>

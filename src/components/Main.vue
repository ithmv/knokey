<template>
  <main>
    <div class="container">
      <Card v-for="(apartment, index) in apartments" 
      :key="index" 
      :name="apartment.name"
      :sum="apartment.sum"
      :address="apartment.address"
      :freeRooms="apartment.freeRooms"
      :allRooms="apartment.allRooms"
      :roomClass="apartment.roomClass"
      :distanceFromCenter="apartment.distanceFromCenter"
      :images="apartment.images"
      :latitude="apartment.coords.split(',')[0]" 
      :longitude="apartment.coords.split(',')[1]"
      :placeholderImage="'https://www.borisbecker.ae/assets/uploads/media-uploader/noimage1688562406.jpg'"
      />
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Card from './Card.vue';

import jsonData from './apartments.json';

interface Apartment {
  name: string;
  sum: number;
  address: string;
  freeRooms: number;
  allRooms: number;
  roomClass: string;
  distanceFromCenter: string;
  images: { path: string }[];
  coords: string;
}

export default defineComponent({
  components: {
    Card,
  },
  data() {
    return {
      apartments: jsonData as Apartment[],
    };
  },
});
</script>

<style lang="scss" scoped>
  main {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    padding-right: 16px;
  }
</style>
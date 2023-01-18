<template>
  <navbar/>
  <card-weather/>
</template>

<script>
import CardWeather from '../components/CardWeather.vue';
import Navbar from '../components/Navbar.vue';
export default {
  components: {
    CardWeather,
    Navbar
  },
    name: "Home",
}
</script>

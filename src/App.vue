<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <div class="ui fixed menu vue-color">
    <div class="">
      <a href="" class="header item">Influencer´s</a>
    </div>
  </div>
  <div class="">
    <card />
  </div>
</template>

<script>
import axios from 'axios'
import Swal from 'sweetalert2'
import Card from './components/Card.vue'

export default {
  name: 'App',
  components: {
    Card,
  },
  data() {
    return {
      
    }
  },
  methods: {
    
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

<script>
import Navbar from './components/Navbar.vue'
import Footer from './components/Footer.vue'
import {mapWritableState, mapActions} from 'pinia'
import {useIndexStore} from '@/stores/index'

export default {
  components: {
    Navbar,
    Footer
  },
  computed: {
    ...mapWritableState(useIndexStore, ['isLogin'])
  },
  methods: {
    ...mapActions(useIndexStore, ['fetchNews', 'fetchTable'])
  },
  created() {
    if(localStorage.getItem('access_token')) {
      this.isLogin = true
      this.fetchNews()
      this.fetchTable()
    }
  }
}
</script>

<template>
<Navbar
v-if="isLogin"
/>
<router-view/>
<Footer
v-if="isLogin"
/>
</template>

<style>
.work-sans {
    font-family: "Work Sans", sans-serif;
  }

  #menu-toggle:checked + #menu {
    display: block;
  }

  .hover\:grow {
    transition: all 0.3s;
    transform: scale(1);
  }

  .hover\:grow:hover {
    transform: scale(1.02);
  }

  .carousel-open:checked + .carousel-item {
    position: static;
    opacity: 100;
  }

  .carousel-item {
    -webkit-transition: opacity 0.6s ease-out;
    transition: opacity 0.6s ease-out;
  }

  #carousel-1:checked ~ .control-1,
  #carousel-2:checked ~ .control-2,
  #carousel-3:checked ~ .control-3 {
    display: block;
  }

  .carousel-indicators {
    list-style: none;
    margin: 0;
    padding: 0;
    position: absolute;
    bottom: 2%;
    left: 0;
    right: 0;
    text-align: center;
    z-index: 10;
  }

  #carousel-1:checked
    ~ .control-1
    ~ .carousel-indicators
    li:nth-child(1)
    .carousel-bullet,
  #carousel-2:checked
    ~ .control-2
    ~ .carousel-indicators
    li:nth-child(2)
    .carousel-bullet,
  #carousel-3:checked
    ~ .control-3
    ~ .carousel-indicators
    li:nth-child(3)
    .carousel-bullet {
    color: #000;
  }
</style>

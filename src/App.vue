<template>
  <div id="app">
    <img src="./assets/logo.png">
    <block></block>
    <Carousel :items="items" :init="0" v-on:change="change"></Carousel>
    <router-view/>
  </div>
</template>

<script>
import Block from './components/Block'
import Carousel from './components/Carousel'
export default {
  name: 'App',
  components: {
    Block,
    Carousel
  },
  data () {
    return {
      items: ['1111', '2222', '3333']
    }
  },
  methods: {
    change (val) {
      console.log('carousel changed to: ' + val)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

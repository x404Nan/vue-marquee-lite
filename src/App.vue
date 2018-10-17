<template>
  <div id="app">
    <vue-marquee-lite
      className="paomadeng"
      :data="list"
      :space="0"
      />
  </div>
</template>

<script>
import Vue from 'vue';
import Marquee from './packages/marquee';

Vue.use(Marquee);
export default {
  name: 'app',
  data() {
    return {
      list: ['aaaaaaaaaaaaaaaaaaaaaa', 'bbbbbbbbbbbbbbbbbb', 'cccccccccccccc'],
    };
  },
  // components: {
  //   Marquee,
  // },
};
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

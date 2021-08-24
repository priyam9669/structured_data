<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import Vue from 'vue'
import HelloWorld from './components/HelloWorld.vue'

export default Vue.extend({
  name: 'App',
  components: {
    HelloWorld
  },
  data:()=>({
     
  }),
  async created(){
      //alert();
      this.fetch_data()
    },
    methods:{
      async fetch_data(){
      fetch('https://api.16biticon.com/auth/getJsonLdData')
      .then(response => (response).text())
      .then(structuredDataText => {
        console.log(JSON.parse(structuredDataText).json_ld)
        const script = document.createElement('script');
        script.setAttribute('type', 'application/ld+json');
        script.textContent = JSON.parse(structuredDataText).json_ld;
        document.head.appendChild(script);
      });
      }
    }

});
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

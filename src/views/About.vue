<template>
  <div class="about">
    <h1>This is an about page</h1>
    <button @click="getCurTrack">refresh</button>
    <h1>{{this.cur}}</h1>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return{
      token: '',
      cur: ""
    }
  },
  mounted(){
    // const hash = this.$route.hash;
    // const a = "access_token";
    // console.log(a)
    // console.log(this.$route.fullPath)
    this.token = this.getUrlVars(this.$route.fullPath)["access_token"];
    console.log(this.token)
    this.getCurTrack();
    // console.log(this.$route)
  },
  methods: {
    getCurTrack(){
      const self = this;
      const config = {
        headers: {
          'Access-Control-Allow-Origin': '*',
            Authorization: `Bearer ` + self.token
        }
      };
      axios.get("https://api.spotify.com/v1/me/player", config).then(function(response){console.log(response); self.cur = response.data.item.name})
    },
    getUrlVars(url) {
      var hash;
      var myJson = {};
      var hashes = url.slice(url.indexOf('#') + 1).split('&');
      for (var i = 0; i < hashes.length; i++) {
          hash = hashes[i].split('=');
          myJson[hash[0]] = hash[1];
          // If you want to get in native datatypes
          // myJson[hash[0]] = JSON.parse(hash[1]); 
      }
      console.log(myJson)
      return myJson;
    }

  }
}
</script>

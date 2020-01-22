<template>
  <div class="about">
    <!-- <h1>Your current Track</h1>
    <h1>--</h1> -->
    <h1>{{this.cur.name}}</h1>
    <h2>By</h2>
    <h1>{{this.cur.artists[0].name}}</h1>
    <button @click="getCurTrack">refresh</button>
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
          Authorization: `Bearer ` + self.token
        }
      };
      axios.get("https://api.spotify.com/v1/me/player", config).then(function(response){console.log(response); self.cur = response.data.item})
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

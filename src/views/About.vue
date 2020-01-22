<template>
  <div class="about">
    <h1>This is an about page</h1>
    <button @click="getCurTrack">refresh</button>
    <h1>{{this.cur.name}}</h1>
    <h2>By</h2>
    <h1 v-for="item in cur.artists" :key=item>{{item.name}}</h1>
    <h2><i>Available Devices</i></h2>
    <h3 v-for="index in devices" :key=index>{{ index.name }}  : <i>{{index.is_active}}</i></h3>
    <button @click="pause">Pause</button>
    <button @click="play">Play</button>
    <!-- <h2>{{this.devices[1].name}}</h2> -->
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return{
      token: '',
      cur: "",
      devices: ""
    }
  },
  mounted(){
    // const hash = this.$route.hash;
    // const a = "access_token";
    // console.log(a)
    // console.log(this.$route.fullPath)
    this.token = this.getUrlVars(this.$route.fullPath)["access_token"];
    console.log(this.token)
    this.getDevices();
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
      axios.get("https://api.spotify.com/v1/me/player", config).then(function(response){console.log(response); self.cur = response.data.item; console.log(self.devices)})
    },
    pause(){
      let f = this.getActivePlayerId()
      const data = {
        id: f
      };
      console.log(data)
      const self = this;
      const config = {
        headers: {
          'Access-Control-Allow-Origin': '*',
            Authorization: `Bearer ` + self.token
        }
      };
    axios.put("https://api.spotify.com/v1/me/player/pause", data, config).then(function(response){console.log(response)})
    },
    play(){
      let f = this.getActivePlayerId()
      const data = {
        id: f
      };
      console.log(data)
      const self = this;
      const config = {
        headers: {
          'Access-Control-Allow-Origin': '*',
            Authorization: `Bearer ` + self.token
        }
      };
    axios.put("https://api.spotify.com/v1/me/player/play", data, config).then(function(response){console.log(response)})
    },
    getDevices(){
      const self = this;
      const config = {
        headers: {
          'Access-Control-Allow-Origin': '*',
            Authorization: `Bearer ` + self.token
        }
      };
      axios.get("https://api.spotify.com/v1/me/player/devices", config).then(function(response){console.log(response); self.devices = response.data.devices})
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
    },
    getActivePlayerId(){
      let i = 0;
      for(i; i < this.devices.length; i++){
        if(this.devices[i].is_active == true){
          console.log(this.devices[i].id)
          return this.devices[i].id;
        }
      }
    }

  }
}
</script>

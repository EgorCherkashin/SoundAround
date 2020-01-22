<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h1>{{this.info}}</h1>
    <button @click="getToken">Get Track</button>
  </div>
</template>

<script>
// import axios from 'axios'
export default {
  name: 'home',
  data() {
    return {
      info: "Hey"
    }
  },
  methods: {
    getToken(){
      // window.location = "https://accounts.spotify.com/authorize?client_id=66d7aef40b0440bc93a4584d58a60039&response_type=code&redirect_uri=http://localhost:8080/about&scope=user-read-currently-playing"
      window.location = "https://accounts.spotify.com/authorize?response_type=token&redirect_uri=http://localhost:8080/about&client_id=66d7aef40b0440bc93a4584d58a60039&scope=user-read-playback-state%20user-modify-playback-state&state=13m02"
    }
  }
}
</script>

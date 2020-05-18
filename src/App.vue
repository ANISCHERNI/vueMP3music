<template>
  <div id="app">
    <header>
      <h1>ANIS MUSIC</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">
          {{ current.title }} <span>{{ current.artist }}</span>
        </h2>

        <div class="controls">
          <button class="prev" @click="prev">prev</button>
          <button class="play" v-if="!isplaying" @click="play">play</button>
          <button class="pause" v-else @click="pause">pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>

 <section class="playlist">
   <h3>The play liste</h3>
   <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src==current.src) ? 'song playing' :'song  '" >

{{song.title}}-{{song.artist}}

   </button>
  </section>

    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      current: {},
      index: 0,
      isplaying: false,

      songs: [
        {
          title: "G.G.A KHALUNI",
          artist: "G.G.A & NOURDO",
          src: require("./assets/G-G-A-NORDO.mp3"),
        },
        {
          title: "El 3ajla Dour",
          artist: "sanfara",
          src: require("./assets/Sanfara-El 3ajla-Edour.mp3"),
        },
      ],
      player: new Audio(),
    };
  },
  methods: {
    play(song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
    
      this.player.play();
      this.isplaying = true;
    },
    pause() {
      this.player.pause();
      this.isplaying = false;
    },
next(){
  this.index++;
if(this.index>this.songs.length -1){

  this.index=0;

}
this.current=this.songs[this.index];
this.play(this.current);

},
prev(){
  this.index--;
if(this.index > 0){

  this.index=this.songs.length -1;

}
this.current=this.songs[this.index];
this.play(this.current);

},

  },

  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
   // this.player.play();
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: sans-serif;
}
header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
  background-color: black;
  color: aliceblue;
}

main{
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}
.song-title {
  color: #53565A;
  font-size: 32px;
  font-weight: 700;
  text-emphasis: none;
  text-align: center;
}
.song-title span{
  font-weight: 400;
  font-style: italic;
}

.controls{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}

button{
appearance: none;
background: none;
border: none;
outline:none;
cursor: pointer;

}
.play{
  font-size: 20px;
font-weight: 700;
padding: 15px 25px;
margin: 0px 15px;
border-radius: 8px;
color: #FFF;
background-color: #cc2e5d;

}
button :hover{
  opacity: 0.8;
}
.next, .prev{
font-size: 16px;
font-weight: 700;
padding: 10px 20px;
margin: 0px 15px;
border-radius: 6px;
color: #fff;
background-color: #ff5858;
}

.playlist{
  padding: 0px 30px ;

}
.playlist h3 {


  color: #212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}
.playlist .song {
display: block;
width: 100%;
padding: 15px;
  font-size: 22px;
  font-weight: 700;
  margin-bottom: 30px;
 cursor: pointer;
}
.playlist .song:hover{
color: #ff5858;
}

.playlist .song .playing{
color: #fff;
background-image: linear-gradient(to right, #cc2e5d ,#ff5858);
}

</style>

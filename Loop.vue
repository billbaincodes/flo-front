<template>
  <view class="container">
    <text
      :v-if="loaded"
      class="text-container"
      v-for="todo in todos"
      :key="todo.text"
    >{{ todo.text }}</text>
    <text
      :v-if="loaded"
      class="text-container"
      v-for="song in playlist.slo"
      :key="song.URL"
    >{{ song.URL }}</text>
    <text class="text-container" v-for="song in playlist.med" :key="song.URL">{{ song.URL }}</text>
    <text class="text-container" v-for="song in playlist.fast" :key="song.URL">{{ song.URL }}</text>

    <song
      :v-if="loaded"
      class="text-container"
      v-for="song in playlist.slo"
      :key="song.URL"
      :item="song"
    ></song>

    <button title="log" :onPress="log">log</button>
  </view>
</template>


<script>
import song from "./Song";

export default {
  components: { song },
  data: function() {
    return {
      loaded: false,
      todos: [
        { text: "Learn JavaScript" },
        { text: "Learn Vue" },
        { text: "Build something awesome" }
      ],
      playlist: { failure: "you" }
    };
  },

  mounted: function() {
    // console.log("mounted");
    this.playlistFetch();
  },
  methods: {
    playlistFetch: function() {
      console.log("mounted");
      fetch("https://flo-back.herokuapp.com/playlist/user/1")
        .then(function(response) {
          return response.json();
        })
        .then(result => this.songSorter(result));
    },
    songSorter: function(result) {
      console.log(result);
      let array = result.playlist;
      let answer = { slo: [], med: [], fast: [] };

      for (let i = 0; i < array.length; i++) {
        if (array[i].slo === true) {
          answer.slo.push(array[i]);
        } else if (array[i].med === true) {
          answer.med.push(array[i]);
        } else {
          answer.fast.push(array[i]);
        }
      }
      this.$data.playlist = answer;
      this.loaded = true;
      console.log(this.playlist);
    },
    log: function() {
      console.log(this.$data.playlist);
    }
  }
};
</script>

<style>
.container {
  background-color: white;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.text-container {
  color: blue;
  padding: 2;
}
</style>
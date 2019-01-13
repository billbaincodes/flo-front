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
    <!-- <text class="text-container" v-for="song in playlist.med" :key="song.id">{{ song.URL }}</text>
    <text class="text-container" v-for="song in playlist.fast" :key="song.id">{{ song.URL }}</text>-->
    <button title="log" :onPress="log">log</button>
  </view>
</template>


<script>
export default {
  data: function() {
    return {
      loaded: false,
      todos: [
        { text: "Learn JavaScript" },
        { text: "Learn Vue" },
        { text: "Build something awesome" }
      ],
      playlist: {}
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
        .then(function(result) {
          //Sort songs into individual playlists
          let array = result.playlist;
          let answer = { slo: [], med: [], fast: [] };

          for (let i = 0; i < array.length; i++) {
            console.log();

            if (array[i].slo === true) {
              answer.slo.push(array[i]);
            } else if (array[i].med === true) {
              answer.med.push(array[i]);
            } else {
              answer.fast.push(array[i]);
            }
          }
          this.playlist = answer;
          this.loaded = true;
          console.log(this.playlist);
        });
    },
    log: function() {
      console.log(this);
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
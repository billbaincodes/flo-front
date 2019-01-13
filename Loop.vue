<template>
  <view class="container">
    <text
      :v-if="loaded"
      class="text-container"
      v-for="todo in todos"
      :key="todo.text"
    >{{ todo.text }}</text>

    <text class="text-container" v-for="song in playlist.slo" :key="song.id">{{ song.URL }}</text>
    <text class="text-container" v-for="song in playlist.med" :key="song.id">{{ song.URL }}</text>
    <text class="text-container" v-for="song in playlist.fast" :key="song.id">{{ song.URL }}</text>
  </view>
</template>


<script>
export default {
  data() {
    return {
      loaded: true,
      todos: [
        { text: "Learn JavaScript" },
        { text: "Learn Vue" },
        { text: "Build something awesome" }
      ],
      playlist: {
        slo: [
          {
            id: 1,
            URL: "http://song.com/walk-like-an-egyptian",
            slo: true,
            med: false,
            fast: false
          },
          {
            id: 2,
            URL: "http://song.com/i-walk-the-line",
            slo: true,
            med: false,
            fast: false
          }
        ],
        med: [
          {
            id: 3,
            URL: "http://song.com/i-ran",
            slo: false,
            med: true,
            fast: false
          },
          {
            id: 4,
            URL: "http://song.com/running-with-the-devil",
            slo: false,
            med: true,
            fast: false
          }
        ],
        fast: [
          {
            id: 5,
            URL: "http://song.com/born-to-run",
            slo: false,
            med: false,
            fast: true
          },
          {
            id: 6,
            URL: "http://song.com/too-fast-for-love",
            slo: false,
            med: false,
            fast: true
          }
        ]
      }
    };
  },

  mounted: function() {
    // console.log("mounted");
    // this.playlistFetch();
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
          let playlist = { slo: [], med: [], fast: [] };

          for (let i = 0; i < array.length; i++) {
            console.log();

            if (array[i].slo === true) {
              playlist.slo.push({ URL: array[i].URL });
            } else if (array[i].med === true) {
              playlist.med.push(array[i]);
            } else {
              playlist.fast.push(array[i]);
            }
          }
          this.playlist = playlist;
          this.loaded = true;
          console.log(this.playlist, this.loaded);
        });
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
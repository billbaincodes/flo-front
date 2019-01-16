<template>
  <nb-container class="body">
    <nb-header class="hider"/>
    <nb-content>
      <nb-list>
        <nb-list-item class="divider" :on-press="navSlo" itemDivider>
          <nb-text class="divider-text" :style="{color: 'cyan'}">Calm</nb-text>
          <image :style="{height: 18, width: 18}" :source="require('./assets/icon-menu.png')">
        </nb-list-item>
        <song
          :v-if="loaded"
          class="text-container"
          v-for="song in playlist.slo"
          :key="song.URL"
          :item="song"
        />
        <view v-if="!loaded" :style="{flex: 1, justifyContent: 'center'}">
          <activity-indicator size="large" color="cyan"/>
        </view>
        <nb-list-item class="divider" :on-press="navMed" itemDivider>
          <nb-text class="divider-text" :style="{color: 'cyan'}">Moderate</nb-text>
          <image :style="{height: 18, width: 18}" :source="require('./assets/icon-menu.png')">
        </nb-list-item>
        <song
          :v-if="loaded"
          class="text-container"
          v-for="song in playlist.med"
          :key="song.URL"
          :item="song"
        ></song>
        <view v-if="!loaded" :style="{flex: 1, justifyContent: 'center'}">
          <activity-indicator size="large" color="cyan"/>
        </view>
        <nb-list-item class="divider" :on-press="navFast" itemDivider>
          <nb-text class="divider-text" :style="{color: 'cyan'}">Intense</nb-text>
          <image :style="{height: 18, width: 18}" :source="require('./assets/icon-menu.png')">
        </nb-list-item>
        <song
          :v-if="loaded"
          class="text-container"
          v-for="song in playlist.fast"
          :key="song.URL"
          :item="song"
        ></song>
        <view v-if="!loaded" :style="{flex: 1, justifyContent: 'center'}">
          <activity-indicator size="large" color="cyan"/>
        </view>
      </nb-list>
    </nb-content>
  </nb-container>
</template>

<script>
import trash from "./assets/pic-profile.png";
import song from "./Song.vue";

export default {
  components: { song },
  data: function() {
    return {
      playlist: { failure: "you" },
      loaded: false
    };
  },
  props: {
    navigation: {
      type: Object
    }
  },
  mounted: function() {
    this.playlistFetch();
  },
  methods: {
    navSlo: function() {
      this.navigation.navigate("addsong", { list: "slo" });
    },
    navMed: function() {
      this.navigation.navigate("addsong", { list: "med" });
    },
    navFast: function() {
      this.navigation.navigate("addsong", { list: "fast" });
    },
    playlistFetch: function() {
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
    }
  }
};
</script>

<style>
.body {
  background-color: rgb(43, 43, 43);
  border-top-width: 4;
  border-bottom-width: 4;
  border-color: cyan;
}
.hider {
  display: none;
}
.container {
  background-color: rgb(43, 43, 43);
  align-items: center;
  justify-content: center;
  flex: 1;
  border-top-width: 4px;
  border-color: cyan;
}
.text-color-primary {
  color: cyan;
}
.text-input {
  color: white;
  background-color: rgb(43, 43, 43);
  border-color: white;
  border-width: 1;
  width: 225;
}
.header {
  color: cyan;
  font-size: 60;
}
.divider {
  display: flex;
  justify-content: space-between;
  background-color: rgb(43, 43, 43);
}
.divider:first-child {
  border-top-width: 4px;
  border-color: cyan;
}

.divider-text {
  font-weight: bold;
  font-size: 20;
}
</style>
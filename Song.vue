<template>
  <nb-list-item :onPress="deleteSong" class="divider">
    <nb-text class="song-text">"{{item.title}}" - {{item.artist}}</nb-text>
  </nb-list-item>
</template>

<script>
import { Alert } from "react-native";
export default {
  props: {
    item: {
      Type: Object
    }
  },
  methods: {
    deleteSong: function() {
      const songTitle = this.$props.item.title
      Alert.alert(
        "Confirm",
        `Delete ${songTitle}?`,
        [
          { text: "Cancel", onPress: () => console.log("Cancel Pressed") },
          { text: "OK", onPress: this.deleteSongFetch }
        ],
        { cancelable: true }
      );
    },

    deleteSongFetch: function() {
      let songID = this.$props.item.id;

      fetch(`https://flo-back.herokuapp.com/song/${songID}`, {
        method: "DELETE"
      });

      fetch(`https://flo-back.herokuapp.com/playlist/${songID}`, {
        method: "DELETE"
      });
    }
  }
};
</script>

<style>
.divider {
  display: flex;
  justify-content: space-between;
  background-color: rgb(43, 43, 43);
  border-bottom-width: 1;
  border-color: rgb(207, 207, 207);
  margin-right: 14;
}
.song-text {
  color: white;
}
</style>
<template>
  <view class="container">
    <nb-form>
      <nb-item :style="{marginRight: 14}" stackedLabel>
        <nb-label :style="{color: 'white'}">Title</nb-label>
        <nb-input v-model="title" :style="{color: 'rgb(190, 190, 190)'}"/>
      </nb-item>
      <nb-item :style="{marginRight: 14}" stackedLabel>
        <nb-label :style="{color: 'white'}">Artist</nb-label>
        <nb-input v-model="artist" :style="{color: 'rgb(190, 190, 190)'}"/>
      </nb-item>
      <nb-item :style="{marginRight: 14}" stackedLabel>
        <nb-label :style="{color: 'white'}">URL</nb-label>
        <nb-input v-model="URL" :style="{color: 'rgb(190, 190, 190)'}"/>
      </nb-item>
    </nb-form>
    <view class="lower">
      <touchable-opacity
        :onPress="pickImage"
        class="login"
        :style="{backgroundColor: 'rgb(60, 60, 60)', height: 40, width: 130}"
      >
        <text class="text-color-primary">Device Storage</text>
      </touchable-opacity>
      <touchable-opacity
        :onPress="addSong"
        class="login"
        :style="{backgroundColor: 'rgb(60, 60, 60)', height: 40, width: 130}"
      >
        <text class="text-color-primary">Save</text>
      </touchable-opacity>
    </view>
  </view>
</template>

<script>
export default {
  data: function() {
    return {
      title: false,
      artist: false,
      URL: false,
      newSongID: undefined
    };
  },
  props: {
    navigation: {
      type: Object
    }
  },
  methods: {
    pickImage: function() {
      Expo.ImagePicker.launchImageLibraryAsync({
        allowsEditing: true,
        aspect: [1, 1]
      });
    },
    addSong: function() {
      let songTitle = this.$data.title
      let songArtist = this.$data.artist
      let songURL = this.$data.URL
      let payload = {
        title: songTitle,
        artist: songArtist,
        URL: songURL
      }

      if (!payload.title || !payload.artist || !payload.URL) {
        alert("Bogus info");
      } else {
        this.addSongFetch(payload);
        this.navigation.goBack();
      }
    },
    addSongFetch: function(payload) {
      fetch("https://flo-back.herokuapp.com/song", {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify(payload)
      })
        .then(response => response.json())
        .then(body => (this.$data.newSongID = body.addedSong.id))
        .then(this.addSongToListFetch);
    },
    addSongToListFetch: function() {
      console.log('I was called')
        let currentList = this.$props.navigation.state.params.list
        let payload = {
          slo: false,
          med: false,
          fast: false,
          users_id: 1,
          song_id: this.$data.newSongID
        }

        if (currentList === 'slo') {
          payload.slo = true
        } else if (currentList === 'med') {
          payload.med = true
        } else {
          payload.fast = true
        }

        fetch("https://flo-back.herokuapp.com/playlist", {
          method: "POST",
          headers: {
            "Content-Type": "application/json"
          },
          body: JSON.stringify(payload)
        })
          .then(response => response.json());
    },
    logger: function() {
      console.log(this.$props.navigation.state.params.list);
    }
  }
};
</script>

<style>
.lower {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-evenly;
}

.container {
  background-color: rgb(43, 43, 43);
  flex: 1;
  border-top-width: 4;
  border-bottom-width: 4;
  border-color: cyan;
}

.text-color-primary {
  color: white;
  font-size: 18;
}

.login {
  margin-top: 50;
  align-items: center;
  justify-content: center;
}
</style>
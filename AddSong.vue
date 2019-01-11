<template>
  <nb-container>
    <nb-header class="hider" hasTabs/>
    <nb-tabs  class="color">
      <nb-tab :style="{backgroundColor: 'black'}"  heading="Local Storage">
        <view :style="{backgroundColor: 'black'}" class="local-container">
          <nb-content padder>
            <nb-button :style="{backgroundColor: 'rgb(43, 43, 43)'}" class="add-song-local" block light>
              <text :style="{color: 'white'}">Access Local Storage</text>
            </nb-button>
          </nb-content>
        </view>
      </nb-tab>
      <nb-tab :style="{backgroundColor: 'black'}" heading="Cloud Storage">
        <nb-form>
          <nb-item floatingLabel>
            <nb-label :style="{color: 'white'}">Title</nb-label>
            <nb-input :style="{color: 'white'}"/>
          </nb-item>
          <nb-item floatingLabel last>
            <nb-label :style="{color: 'white'}">Artist</nb-label>
            <nb-input :style="{color: 'white'}"/>
          </nb-item>
          <nb-item floatingLabel last>
            <nb-label :style="{color: 'white'}">URL</nb-label>
            <nb-input :style="{color: 'white'}"/>
          </nb-item>
        </nb-form>
        <view class="cloud-container">
          <nb-content padder>
            <nb-button :style="{backgroundColor: 'rgb(43, 43, 43)'}" :onPress="submitSong" class="add-song" block light>
              <text :style="{color: 'white'}">Add Song!</text>
            </nb-button>
          </nb-content>
        </view>
      </nb-tab>
    </nb-tabs>
  </nb-container>
</template>

<script>
export default {
  props: {
    navigation: {
      type: Object
    }
  },
  methods: {
    submitSong: function() {
      console.log("song added");
      this.navigation.goBack()
    }
  }
};
</script>


<style>
.tabs {
  background-color: black;
  /* color: cyan; */
}
.hider {
  display: none;
}
.cloud-container {
  align-items: center;
  justify-content: center;
  flex: 1;
  margin-bottom: 175px;
}
.add-song {
  width: 100;
  margin-top: 100;
}

.add-song-local {
  width: 300;
  /* background-color: gray; */
}

.local-container {
    background-color: white;
  align-items: center;
  justify-content: center;
  flex: 1;
  margin-top: 100px;
}
</style>
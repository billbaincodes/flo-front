<template>
  <nb-container>
    <nb-header class="hider" hasTabs/>
    <nb-tabs class="color">
      <nb-tab heading="Local Storage">
        <view class="local-container">
          <nb-content padder>
            <nb-button class="add-song-local" block light>
              <text>Access Local Storage</text>
            </nb-button>
          </nb-content>
        </view>
      </nb-tab>
      <nb-tab heading="Cloud Storage">
        <nb-form>
          <nb-item floatingLabel>
            <nb-label>Title</nb-label>
            <nb-input/>
          </nb-item>
          <nb-item floatingLabel last>
            <nb-label>Artist</nb-label>
            <nb-input/>
          </nb-item>
          <nb-item floatingLabel last>
            <nb-label>URL</nb-label>
            <nb-input/>
          </nb-item>
        </nb-form>
        <view class="cloud-container">
          <nb-content padder>
            <nb-button :onPress="submitSong" class="add-song" block light>
              <text>Add Song!</text>
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
  background-color: white;
  align-items: center;
  justify-content: center;
  flex: 1;
  margin-bottom: 175px;
}
.add-song {
  width: 100;
  /* background-color: gray; */
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
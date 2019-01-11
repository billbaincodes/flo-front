<template>
  <view class="container">
    <text class="header">Your Profile:</text>
    <image
      :style="{width: 200, height: 200, borderRadius: 100}"
      :source="{uri: 'https://static1.squarespace.com/static/549dd0cee4b029881efa814b/5b101ad2758d46ee70365c19/5c05b5c621c67cd401736b1e/1543878094686/dc-headshot-photographer-52.JPG?format=300w'}"
    />

    <view :style="{backgroundColor: 'rgb(43, 43, 43)', width: 300}">
      <text class="profile-text">Name: Donnie Denver</text>
      <text class="profile-text">Email: donnie@gmail.com</text>
    </view>

    <nb-button
    title="nb-button"
      :style="{backgroundColor: 'rgb(43, 43, 43)', width: 125}"
      class="add-song-local"
      block
      light
    >
      <text :style="{color: 'white'}">Edit Profile</text>
    </nb-button>
  </view>
</template>

<script>
export default {
  props: {
    navigation: {
      type: Object
    }
  },
  methods: {
    navMusic: function() {
      this.navigation.navigate("music");
    }
  }
};
</script>

<style>
.container {
  background-color: black;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.text-color-primary {
  color: cyan;
}

.header {
  color: cyan;
  font-size: 40;
}
.profile {
  align-items: flex-start;
  justify-content: flex-start;
  margin-top: 40px;
}
.profile-text {
  color: white;
  font-size: 20;
}
</style>
<template>
  <view class="container">
    <text class="header">Your Profile:</text>
    <image
      :style="{width: 50, height: 50}"
      :source="{uri: './assets/pic-profile.png'}"
    />
    <text class="text-color-primary">Name:</text>
    <text class="text-color-primary">Donny Denver</text>
    <text class="text-color-primary">Email:</text>
    <text class="text-color-primary">DD@gmail.com</text>

  </view>
</template>

<script>
// import profilePic from "./assets/pic-profile.png"

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
.text-input {
  color: white;
  background-color: rgb(66, 66, 66);
  border-color: white;
  border-width: 1;
  width: 225;
}
.header {
  color: cyan;
  font-size: 60;
}
</style>
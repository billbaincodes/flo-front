<template>
  <view class="container">
    <text class="header">flô:</text>
    <text class="text-color-primary">Email:</text>
    <text-input class="text-input"/>
    <text class="text-color-primary">Password:</text>
    <text-input class="text-input"/>
    <touchable-opacity :on-press="navMusic">
      <text class="text-color-primary">Log In</text>
    </touchable-opacity>
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
      this.navigation.navigate("main");
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
  font-size: 75;
}
</style>

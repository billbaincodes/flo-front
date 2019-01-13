<template>
  <view class="container">
    <text class="header">flô</text>
        <KeyboardAvoidingView

      behavior="padding"
    >
    <text class="text-color-primary">Email:</text>
    <text-input :style="{padding: 6}" class="text-input"/>
    <text class="text-color-primary">Password:</text>
    <text-input :style="{padding: 6}" class="text-input"/>

    <touchable-opacity class="login" :style="{backgroundColor: 'rgb(43, 43, 43)', height: 50, width: 100}" :on-press="navMusic">
      <text class="text-color-primary">Log In</text>
    </touchable-opacity>
            </KeyboardAvoidingView>
  </view>
</template>

<script>
import {KeyboardAvoidingView} from 'react-native'

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
  font-size: 24;
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
  font-size: 80;
}
.login {
  margin: 60;
  align-items: center;
  justify-content: center;
}
</style>

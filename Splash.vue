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

  <view class="buttons">
    <touchable-opacity class="login" :style="{backgroundColor: 'rgb(43, 43, 43)', height: 50, width: 100, borderWidth: 2, borderColor: 'white'}" :on-press="navMusic">
      <text class="text-color-primary">Log In</text>
    </touchable-opacity>
        <touchable-opacity class="login" :style="{backgroundColor: 'rgb(43, 43, 43)', height: 50, width: 100, borderWidth: 2, borderColor: 'white'}" :on-press="navMusic">
      <text class="text-color-primary">Sign Up</text>
    </touchable-opacity>
    </view>
            </KeyboardAvoidingView>
  </view>
</template>

<script>
import {KeyboardAvoidingView} from 'react-native'

export default {
  props: {
    navigation: {
      type: Object,
    }
  },
  methods: {
    navMusic: function() {
      this.navigation.navigate("main", {title: 'Main'});
    }
  }
};
</script>

<style>
.container {
  background-color: rgb(43, 43, 43);
  align-items: center;
  justify-content: center;
  flex: 1;
  border-top-width: 4px;
  border-color: cyan;
}
.text-color-primary {
  color: white;
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
  margin-top: 60;
  margin-right: 10;
  align-items: center;
  justify-content: center;
}

.buttons {
  display: flex;
  flex-direction: row;
  align-items: center;
}
</style>

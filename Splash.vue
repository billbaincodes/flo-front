<template>
  <view class="container">
    <text class="header">flô</text>
        <KeyboardAvoidingView
        behavior="padding"
    >
      <nb-form>
          <nb-item :style="{width: 200, marginRight: 10}" floatingLabel>
            <nb-label :style="{color: 'white'}">Email</nb-label>
            <nb-input :style="{color: 'white'}"/>
          </nb-item>
          <nb-item :style="{width: 200, marginRight: 10}" floatingLabel>
            <nb-label :style="{color: 'white'}">Password</nb-label>
            <nb-input secureTextEntry :style="{color: 'white'}"/>
          </nb-item>
        </nb-form>

  <view class="buttons">
    <touchable-opacity class="login" :style="{backgroundColor: 'rgb(43, 43, 43)', height: 40, width: 90, borderWidth: 1, borderColor: 'white'}" :on-press="navMain">
      <text class="text-color-primary">Log In</text>
    </touchable-opacity>
        <touchable-opacity class="login" :style="{backgroundColor: 'rgb(43, 43, 43)', height: 40, width: 90, borderWidth: 1, borderColor: 'white'}" :on-press="navMain">
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
    navMain: function() {
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
  border-bottom-width: 4px;
  border-color: cyan;
}
.text-color-primary {
  color: white;
  font-size: 18;
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
  margin-top: 50;
  align-items: center;
  justify-content: center;

}

.buttons {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;
  margin-bottom: 50;
}
</style>

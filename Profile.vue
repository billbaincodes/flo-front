<template>
  <view class="container">
    <image
      :style="{width: 200, height: 200, borderRadius: 200, margin: 25}"
      :source="{uri: 'https://static1.squarespace.com/static/549dd0cee4b029881efa814b/5b101ad2758d46ee70365c19/5c05b5c621c67cd401736b1e/1543878094686/dc-headshot-photographer-52.JPG?format=300w'}"
    />
    <text :style="{fontSize: 32, color: 'white'}">Donnie Denver</text>
    <text class="profile-text">donnie@gmail.com</text>
    <view :style="{marginTop: 40}" class="blob">
      <text :style="{borderTopWidth: 0, borderLeftWidth: 0}" class="profile-blob">Runs</text>
      <text :style="{borderTopWidth: 0}" class="profile-blob">Songs</text>
      <text :style="{borderTopWidth: 0, borderRightWidth: 0}" class="profile-blob">Playlists</text>
    </view>
    <view class="blob">
      <text
        :style="{borderBottomWidth: 0, borderLeftWidth: 0, paddingTop: 8, color: 'rgb(180, 180, 180)'}"
        class="profile-blob"
      >17</text>
      <text
        :style="{borderBottomWidth: 0, paddingTop: 8, color: 'rgb(180, 180, 180)'}"
        class="profile-blob"
      >9</text>
      <text
        :style="{borderBottomWidth: 0, borderRightWidth: 0, paddingTop: 8, color: 'rgb(180, 180, 180)'}"
        class="profile-blob"
      >3</text>
    </view>
    <touchable-opacity
      :onPress="navEdit"
      class="login"
      :style="{backgroundColor: 'rgb(60, 60, 60)', height: 40, width:110}"
    >
      <text :style="{fontSize: 18, color: 'white'}">Edit Profile</text>
    </touchable-opacity>
  </view>
</template>

<script>
import { Ionicons } from "@expo/vector-icons";

export default {
  data: function() {
    return {
      loaded: false
    };
  },
  props: {
    navigation: {
      type: Object
    }
  },
  methods: {
    navEdit: function() {
      this.navigation.navigate("editProfile");
    }
  }
};
</script>

<style>
.blob {
  display: flex;
  flex-direction: row;
}
.profile-blob {
  width: 100;
  height: 40;
  font-size: 18;
  border-width: 0.5;
  border-color: white;
  color: white;
  justify-content: flex-start;
  text-align: center;
  margin: auto;
}

.lower {
  height: 30%;
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
}

.login {
  margin-top: 40;
  margin-bottom: 40;
  align-items: center;
  justify-content: center;
}

.container {
  background-color: rgb(43, 43, 43);
  align-items: center;
  justify-content: center;
  flex: 1;
  border-top-width: 3px;
  border-bottom-width: 3px;
  border-color: cyan;
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
  color: rgb(180, 180, 180);
  font-size: 20;
}
</style>
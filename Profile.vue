<template>
  <view class="container">
    <image
      :style="{width: 220, height: 220, borderRadius: 200, margin: 25}"
      :source="{uri: 'https://static1.squarespace.com/static/549dd0cee4b029881efa814b/5b101ad2758d46ee70365c19/5c05b5c621c67cd401736b1e/1543878094686/dc-headshot-photographer-52.JPG?format=300w'}"
    />
    <text :style="{fontSize: 36, color: 'white'}" >Donnie Denver</text>
    <text class="profile-text">donnie@gmail.com</text>
</template>

<script>
import {Ionicons} from '@expo/vector-icons'

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
    navMusic: function() {
      this.navigation.navigate("music");
    }
  },
  async created() {
    await Expo.Font.loadAsync({
      'Ionicons': require('./node_modules/@expo/vector-icons/fonts/Ionicons.ttf'),
    });

    this.loaded = true
  }
};
</script>

<style>
.lower {
  height: 30%;
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
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
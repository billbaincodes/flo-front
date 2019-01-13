<template>
  <app-navigation class="app-nav"></app-navigation>
</template>

<script>
//disable warnings for demo
console.disableYellowBox = true;

import Vue from "vue-native-core";
import { VueNativeBase } from "native-base";

// registering all native-base components to the global scope of the Vue
Vue.use(VueNativeBase);

import { StackNavigator } from "vue-native-router";
import Splash from './Splash.vue'
import Speedometer from './Speedometer.vue'
import Music from "./Music.vue"
import Main from './Main.vue'
import Profile from './Profile.vue'
import AddSong from "./AddSong.vue"
import Grow from "./Grow.vue"
import Loop from "./Loop.vue"

const AppNavigation = StackNavigator(
  {
    splash: Splash,
    speedometer: Speedometer,
    music: Music,
    profile: Profile,
    main: Main,
    addsong: AddSong,
    grow: Grow,
    loop: Loop
  },
  {
    initialRouteName: 'loop',
  }
);
export default {
  components: { AppNavigation }
}
</script>

<style>
.container {
  background-color: white;
  align-items: center;
  justify-content: center;
  flex: 1;
}

.text-color-primary {
  color: blue;
}

.nav {
  background-color: black
}

.app-nav {
  background-color: black;
}
</style>

<template>
  <app-navigation class=""></app-navigation>
</template>

<script>
import { StackNavigator } from "vue-native-router";
import Splash from './Splash.vue'
import Main from './Main.vue'
const AppNavigation = StackNavigator(
  {
    Splash: Splash,
    Main: Main,
  },
  {
    initialRouteName: 'Splash',
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
  background-color: blue
}
</style>

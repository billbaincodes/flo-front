<template>
  <app-navigation class="app-nav"></app-navigation>
</template>

<script>
//CAUTION: DISABLES WARNINGS FOR SCREEN CAP
console.disableYellowBox = true;

import Vue from "vue-native-core";
import { VueNativeBase } from "native-base";

// registering all native-base components to the global scope of the Vue
Vue.use(VueNativeBase);

import { StackNavigator } from "vue-native-router";
import Splash from "./Splash.vue";
import Speedometer from "./Speedometer.vue";
import Music from "./Music.vue";
import Main from "./Main.vue";
import Profile from "./Profile.vue";
import AddSong from "./AddSong.vue";
import Loop from "./Loop.vue";
import Color from "./Color.vue";
import EditProfile from "./EditProfile.vue";

const AppNavigation = StackNavigator(
  {
    splash: Splash,
    speedometer: Speedometer,
    music: {
      screen: Music,
      navigationOptions: {
        title: "Music",
        headerStyle: {
          backgroundColor: "rgb(0,0,0)"
        },
        headerTintColor: "#fff",
        headerTitleStyle: {
          fontWeight: "bold"
        }
      }
    },
    profile: {
      screen: Profile,
      navigationOptions: {
        title: "Profile",
        headerStyle: {
          backgroundColor: "rgb(0,0,0)"
        },
        headerTintColor: "#fff",
        headerTitleStyle: {
          fontWeight: "bold"
        }
      }
    },
    addsong: {
      screen: AddSong,
      navigationOptions: {
        title: "Add Song",
        headerStyle: {
          backgroundColor: "rgb(0,0,0)"
        },
        headerTintColor: "#fff",
        headerTitleStyle: {
          fontWeight: "bold"
        }
      }
    },
    loop: Loop,
    color: Color,
    editProfile: {
      screen: EditProfile,
      navigationOptions: {
        title: "Edit Profile",
        headerStyle: {
          backgroundColor: "rgb(0,0,0)"
        },
        headerTintColor: "#fff",
        headerTitleStyle: {
          fontWeight: "bold"
        }
      }
    },
    main: {
      screen: Main,
      navigationOptions: {
        title: "flô",
        headerStyle: {
          backgroundColor: "rgb(0,0,0)"
        },
        headerTintColor: "#fff",
        headerTitleStyle: {
          fontWeight: "bold"
        }
      }
    }
  },
  {
    initialRouteName: "splash",
    cardStyle: {
      backgroundColor: "rgba(0,0,0,0)"
    },
    navigationOptions: {
      title: "Welcome",
      headerStyle: {
        backgroundColor: "rgb(0,0,0)"
      },
      headerTintColor: "#fff",
      headerTitleStyle: {
        fontWeight: "bold"
      }
    }
  }
);
import { Ionicons } from "@expo/vector-icons";

export default {
  components: { AppNavigation }
};
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
  background-color: black;
}

.app-nav {
  background-color: black;
}
</style>

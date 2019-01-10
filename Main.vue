<template>
  <view class="container">
    <animated:view
      class="speedometer"
      :style="{
        height: growth,
        width: growth ,
        borderRadius:growth,
      }"
    >
      <text class="speedometer-text">{{speed}}</text>
    </animated:view>

    <text class="text-color-primary">playlist : {{zone}}</text>

    <touchable-opacity :on-press="speed0">
      <text class="text-color-primary">Speed 0</text>
    </touchable-opacity>
    <touchable-opacity :on-press="speed1">
      <text class="text-color-primary">Speed 1</text>
    </touchable-opacity>
    <touchable-opacity :on-press="speed2">
      <text class="text-color-primary">Speed 2</text>
    </touchable-opacity>

    <touchable-opacity :on-press="startRun" class="flo-button">
      <text v-if="run" class="text-color-primary">run</text>
      <text v-else class="text-color-primary">run</text>
    </touchable-opacity>
    <view class="nav">
      <text class="nav-text" :on-press="navProfile">Go to your Profile</text>
      <text class="nav-text" :on-press="navMusic">Go to your Music</text>
    </view>
  </view>
</template>

<script>
import { Animated, Easing } from "react-native";
import chopin from "./assets/audio-chopin.mp3";
import sexInAPan from "./assets/audio-sexInAPan.mp3";

const soundObject = new Expo.Audio.Sound();

export default {
  props: {
    navigation: {
      type: Object
    }
  },
  data() {
    return {
      growth: 0,
      speed: 0,
      run: false,
      zone: "calm",
      slow: chopin,
      fast: sexInAPan
    };
  },
  created: function() {
    this.growth = new Animated.Value(0);
  },
  watch: {
    speed: function() {
      this.playMusic();
    }
  },
  methods: {
    navProfile: function() {
      this.navigation.navigate("profile");
    },
    navMusic: function() {
      this.navigation.navigate("music");
    },
    playMusic: async function() {
      if (this.speed == 0) {
        soundObject.pauseAsync();
        soundObject.unloadAsync();
        this.zone = "calm";
      } else if (this.speed === 1) {
        soundObject.pauseAsync();
        soundObject.unloadAsync();
        await soundObject.loadAsync(this.slow);
        await soundObject.playAsync();
        this.zone = "moderate";
      } else if (this.speed === 2) {
        soundObject.pauseAsync();
        soundObject.unloadAsync();
        await soundObject.loadAsync(this.fast);
        await soundObject.playAsync();
        this.zone = "intense";
      }
    },
    speed0: function() {
      this.speed = 0;
    },
    speed1: function() {
      this.speed = 1;
    },
    speed2: function() {
      this.speed = 2;
    },
    startRun: function() {
      this.run = !this.run;

      if (this.run === true) {
        this.growth.setValue(0);

        Animated.timing(this.growth, {
          toValue: 200,
          duration: 200,
          easing: Easing.linear
        }).start(() => {
          // this.animateGrowth();
        });
      } else {
        this.growth.setValue(200);

        Animated.timing(this.growth, {
          toValue: 0,
          duration: 200,
          easing: Easing.linear
        }).start(() => {
          // this.animateGrowth();
        });
      }
    },
    animateGrowth: function() {
      this.growth.setValue(0);

      Animated.timing(this.growth, {
        toValue: 200,
        duration: 200,
        easing: Easing.linear
      }).start(() => {
        // this.animateGrowth();
      });
    },
    animateShrink: function() {
      this.growth.setValue(200);

      Animated.timing(this.growth, {
        toValue: 0,
        duration: 200,
        easing: Easing.linear
      }).start(() => {
        // this.animateGrowth();
      });
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

.speedometer {
  height: 200;
  width: 200;
  background-color: rgb(43, 43, 43);
  border-radius: 100;
  align-items: center;
  justify-content: center;
}

.speedometer-text {
  font-size: 75;
  color: cyan;
  margin: auto;
}

.nav {
  display: flex;
  flex-direction: row;
}

.nav-text {
  color: white;
  padding: 20;
}

.flo-button {
  background-color: rgb(43, 43, 43);
  width: 200;
  height: 50;
  border-radius: 50;
  align-items: center;
  justify-content: center;
  /* font-size: 30; */
}

.growth-animated-view {
  background-color: "rgb(0, 138, 231)";
  align-self: center;
}
</style>
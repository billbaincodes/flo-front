<template>
  <view class="container">
    <view class="spacer"></view>
    <animated:view
      class="speedometer"
      :style="{
        height: 200,
        width: 200 ,
        borderRadius:growth,
        borderWidth: 2,
        opacity: opacity
      }"
    >
      <view class="speedometer-container">
        <animated:view :style="{
          opacity: opacity,
      }">
          <text class="speedometer-text">
            {{speedDisplay}}
            <animated:text :style="{fontSize: 20, color: 'white', opacity: opacity}">m/s</animated:text>
          </text>
        </animated:view>
      </view>
    </animated:view>
    <animated:view :style="{opacity: opacity}">
      <text :style="{fontSize: 40}" class="text-color-primary">{{zone}}</text>
    </animated:view>

    <!-- <touchable-opacity :on-press="speed0">
      <text class="text-color-primary">Speed 0</text>
    </touchable-opacity>
    <touchable-opacity :on-press="speed1">
      <text class="text-color-primary">Speed 1</text>
    </touchable-opacity>
    <touchable-opacity :on-press="speed2">
      <text class="text-color-primary">Speed 2</text>
    </touchable-opacity>-->
    <touchable-opacity :on-press="startRun" class="flo-button">
      <text v-if="!run" :style="{fontSize: 22, color: 'white'}" class="text-color-primary">run</text>
      <text v-else class="text-color-primary">stop</text>
    </touchable-opacity>


  <view class="buttons">
    <touchable-opacity class="login" :style="{backgroundColor: 'rgb(60, 60, 60)', height: 40, width: 90}" :on-press="navProfile">
      <text class="text-color-primary">Profile</text>
    </touchable-opacity>
        <touchable-opacity class="login" :style="{backgroundColor: 'rgb(60, 60, 60)', height: 40, width: 90}" :on-press="navMusic">
      <text class="text-color-primary">Music</text>
    </touchable-opacity>
    </view>


  </view>
</template>

<script>
import { Animated, Easing } from "react-native";
import teardrop from "./assets/audio-teardrop.mp3"
import bornToRun from "./assets/audio-borntorun.mp3"
import throughTheFireAndFlames from "./assets/audio-throughthefireandflames.mp3"

const soundObject = new Expo.Audio.Sound();


export default {
  navigationOptions: {
      title: 'candy'
  },
  props: {
    navigation: {
      type: Object
    },

  },
  data() {
    return {
      growth: 200,
      bWidth: 0,
      opacity: 0,
      speed: 0,
      speedDisplay: 0,
      run: false,
      zone: 'still',
      slow: teardrop,
      med: bornToRun,
      fast: throughTheFireAndFlames
    };
  },
  created: function() {
    this.growth = new Animated.Value(0);
    this.opacity = new Animated.Value(0);
    this.bWidth = new Animated.Value(0);
  },
  mounted() {
    // Simulate speed increase to trigger music
    // this.speedSimulator();
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
      if (this.speed < 1) {
        soundObject.pauseAsync();
        soundObject.unloadAsync();
        this.zone = null;
      } else if (this.speed >= 1 && this.speed < 3) {
        soundObject.pauseAsync();
        soundObject.unloadAsync();
        await soundObject.loadAsync(this.slow);
        await soundObject.playAsync();
        this.zone = "calm";
      } else if (this.speed >=3 && this.speed < 6) {
        soundObject.pauseAsync();
        soundObject.unloadAsync();
        await soundObject.loadAsync(this.med);
        await soundObject.playAsync();
        this.zone = "moderate";
      } else if (this.speed >= 6) {
        soundObject.pauseAsync();
        soundObject.unloadAsync();
        await soundObject.loadAsync(this.fast);
        await soundObject.playAsync();
        this.zone = "intense";
      }
    },
    speedSimulator: function() {
      setTimeout(() => {
        this.speedDisplay = 0.4;
      }, 5000);
      setTimeout(() => {
        this.speedDisplay = 0.7;
      }, 5300);
      setTimeout(() => {
        this.speedDisplay = 1;
      }, 5500);
      setTimeout(() => {
        this.speed = 1
      }, 5500);
      setTimeout(() => {
        this.speedDisplay = 1.8;
      }, 12000);
      setTimeout(() => {
        this.speedDisplay = 2.1;
      }, 12020);
      setTimeout(() => {
        this.speedDisplay = 2.7;
      }, 12120);
      setTimeout(() => {
        this.speedDisplay = 3;
      }, 12500);
      setTimeout(() => {
        this.speed = 3
      }, 12500);
        setTimeout(() => {
        this.speedDisplay = 4.1;
      }, 19000);
      setTimeout(() => {
        this.speedDisplay = 5.2;
      }, 19200);
      setTimeout(() => {
        this.speedDisplay = 6.0
      }, 19500);
      setTimeout(() => {
        this.speed = 6
      }, 19500);
    },
    speed0: function() {
      this.speed = 0;
      this.speedDisplay = 0
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
        //Growing animation
        this.speed = 0

        soundObject.playAsync();
        this.growth.setValue(200);
        this.opacity.setValue(0);

        Animated.timing(this.growth, {
          toValue: 200,
          duration: 600,
          easing: Easing.linear
        }).start(() => {
          // this.animateGrowth();
        });
        Animated.timing(this.opacity, {
          toValue: 1,
          duration: 1200,
          easing: Easing.linear
        }).start(() => {
          // this.animateGrowth();
        });
        Animated.timing(this.bWidth, {
          toValue: 2,
          duration: 600,
          easing: Easing.linear
        }).start(() => {
          // this.animateGrowth();
        });
      } else {
        //Shrinking animation
        this.speed0

        this.growth.setValue(200);
        Animated.timing(this.growth, {
          toValue: 200,
          duration: 600,
          easing: Easing.linear
        }).start(() => {
          // this.animateGrowth();
        });
        Animated.timing(this.opacity, {
          toValue: 0,
          duration: 600,
          easing: Easing.linear
        }).start(() => {
          // this.animateGrowth();
        });
        Animated.timing(this.bWidth, {
          toValue: 2,
          duration: 600,
          easing: Easing.linear
        }).start(() => {
          // this.animateGrowth();
        });
        soundObject.pauseAsync();

      }
    }
  }
};
</script>

<style>
.container {
  background-color: rgb(43, 43, 43);
  align-items: center;
  justify-content: space-between;
  flex: 1;
  border-top-width: 4px;
  border-bottom-width: 4px;
  border-color: cyan;
}
.text-color-primary {
  color: white;
  font-size: 18;
}

.speedometer {
  height: 200;
  width: 200;
  background-color: rgb(43, 43, 43);
  border-radius: 100;
  align-items: center;
  justify-content: center;
  border-color: cyan;
  border-width: 0;
}

.speedometer-text {
  font-size: 75;
  color: white;
  margin: auto;
}

.nav {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  text-align: center;
}

.nav-text {
  color: white;
  border-width: 1;
  border-color: white;
  margin-top: 40;
  margin-bottom: 40;
  font-size: 18;
  height: 40;
  width: 90;
}

.flo-button {
  background-color: rgb(43, 43, 43);
  width: 200;
  height: 50;
  border-radius: 25;
  align-items: center;
  justify-content: center;
  border-width: 2;
  border-color: cyan;
  /* background-color: cyan; */
  /* font-size: 30; */
}

.growth-animated-view {
  background-color: "rgb(0, 138, 231)";
  align-self: center;
}
.spacer {
  height: 50;
  width: 1;
}
.speedometer-container {
  display: flex;
  flex-direction: row;
  align-items: flex-end;
}

.buttons {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-evenly;
  margin-bottom: 50;
  width: 100%;
}

.login {
  margin-top: 30;
  align-items: center;
  justify-content: center;
}
</style>
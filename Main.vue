<template>
  <view class="container">
    <view class="spacer"></view>
    <animated:view
      class="speedometer"
      :style="{
        height: growth,
        width: growth ,
        borderRadius:growth,
        borderWidth: bWidth,
      }"
    >
      <view class="speedometer-container">
        <animated:view :style="{
          opacity: opacity,
      }">
          <text class="speedometer-text">
            {{speed}}
            <text v-if="run" :style="{fontSize: 20, color: 'cyan'}">m/s</text>
          </text>
        </animated:view>
      </view>
    </animated:view>
    <animated:view :style="{opacity: opacity}">
      <text class="text-color-primary">zone : {{zone}}</text>
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
      <text v-if="!run" class="text-color-primary">run</text>
      <text v-else class="text-color-primary">stop</text>
    </touchable-opacity>
    <view class="nav">
      <text class="nav-text" :on-press="navProfile">Go to your Profile</text>
      <text class="nav-text" :on-press="navMusic">Go to your Music</text>
    </view>
    <button :onPress="logger" title="test">log this</button>
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
      bWidth: 0,
      opacity: 0,
      speed: 0,
      run: false,
      zone: null,
      slow: chopin,
      fast: sexInAPan
    };
  },
  created: function() {
    this.growth = new Animated.Value(0);
    this.opacity = new Animated.Value(0);
    this.bWidth = new Animated.Value(0);
  },
  mounted() {
    // simulate speed increase to trigger music
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
      if (this.speed == 0) {
        soundObject.pauseAsync();
        soundObject.unloadAsync();
        this.zone = null;
      } else if (this.speed === 1) {
        soundObject.pauseAsync();
        soundObject.unloadAsync();
        await soundObject.loadAsync(this.slow);
        await soundObject.playAsync();
        this.zone = "calm";
      } else if (this.speed === 2) {
        soundObject.pauseAsync();
        soundObject.unloadAsync();
        await soundObject.loadAsync(this.fast);
        await soundObject.playAsync();
        this.zone = "moderate";
      }
    },
    speedSimulator: function() {
      setTimeout(() => {
        this.speed = 1;
      }, 5000);
      setTimeout(() => {
        this.speed = 2;
      }, 8000);
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
        //Growing animation
        soundObject.playAsync();
        this.growth.setValue(0);
        this.opacity.setValue(0);

        this.speed = 0;
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
          toValue: 2.5,
          duration: 600,
          easing: Easing.linear
        }).start(() => {
          // this.animateGrowth();
        });
      } else {
        //Shrinking animation
        this.speed = undefined;
        this.growth.setValue(200);
        Animated.timing(this.growth, {
          toValue: 0,
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
          toValue: 0,
          duration: 600,
          easing: Easing.linear
        }).start(() => {
          // this.animateGrowth();
        });
        soundObject.pauseAsync();
      }
    },
    logger: function() {
      this.$props.navigation.setParams({ title: "title" });
      console.log(this.$props.navigation);
    }
  }
};
</script>

<style>
.container {
  background-color: black;
  align-items: center;
  justify-content: space-between;
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
  border-color: cyan;
  border-width: 0;
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
.spacer {
  height: 50;
  width: 1;
}
.speedometer-container {
  display: flex;
  flex-direction: row;
  align-items: flex-end;
}
</style>
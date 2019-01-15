<template>
  <view class="container">
    <animated:view
      class="growth-animated-view"
      :style="{
        width: growth,
        height: growth
      }"
    />
    <animated:view class="color" :style="{
        backgroundColor: interpolateColor
      }"/>
    <button title="grow it" :onPress="animateGrowth">Grow it</button>
    <button title="shrink it" :onPress="animateShrink">shrink it</button>
    <button title="color it" :onPress="colorStart">color it</button>

  </view>
</template>

<script>
import { Animated, Easing } from "react-native";

this.interpolateColor = this.animatedColorValue.interpolate({
  inputRange: [0, 150],
  outputRange: ["rgb(128,0,128)", "rgb(51, 250, 170)"]
});

export default {
  data: function() {
    return {
      growth: 0,
      interpolateColor: 0
    };
  },
  created: function() {
    this.growth = new Animated.Value(0);
    this.color = new Animated.Value(0);
  },
  methods: {
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
    },
    colorStart: function() {
      animated.timing(this.animatedColorValue, {
        toValue: 150,
        duration: 1000
      }).start(() => {
        // this.colorStart();
      });
    }
  }
};
</script>

<style>
.growth-animated-view {
  background-color: "rgb(0, 138, 231)";
  align-self: center;
}

.container {
  justify-content: center;
  flex: 1;
}

.color {
  width: 50px;
  height: 50px;
}
</style>
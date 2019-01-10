<template>
  <view class="container" >
    <animated:view
      class="growth-animated-view"
      :style="{
        height: growth,
        width: growth ,
        borderRadius:growth,
      }"
    />
    <button title="grow it" :onPress="animateGrowth">Grow it</button>
        <button title="shrink it" :onPress="animateShrink">shrink it</button>

  </view>
</template>

<script>
import { Animated, Easing } from "react-native";

export default {
  data: function() {
    return {
      growth: 0
    };
  },
  created: function() {
    this.growth = new Animated.Value(0);
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
</style>
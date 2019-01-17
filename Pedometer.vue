<template>
  <view class="container">
    <text class="header">pedometer</text>
    <text>{{steps}}</text>
    <text>{{speed}}</text>
  </view>
</template  >

<script>  

export default {
  data: function() {
    return {
      steps: undefined,
      time: undefined,
      speed: undefined
    };
  },
  props: {
    navigation: {
      type: Object,
    }
  },
  mounted: function() {
    Expo.Pedometer.watchStepCount(this.pedometerTest)
  },
  methods: {
    navMain: function() {
      this.navigation.navigate("main", {title: 'Main'});
    },
    pedometerTest: function(info) {
      console.log(info)

      if (this.time === undefined) {
        this.time = Date.now()
        this.steps = info.steps
      } else {
        timechange = Date.now() - this.time
        this.steps = this.steps - info.steps
        this.speed = (this.steps * 28.5)/this.time
      }
    }
  }
};
</script>

<style>
.container {
  background-color: rgb(43, 43, 43);
  align-items: center;
  justify-content: center;
  flex: 1;
  border-top-width: 4px;
  border-bottom-width: 4px;
  border-color: cyan;
}
.text-color-primary {
  color: white;
  font-size: 18;
}
.text-input {
  color: white;
  background-color: rgb(66, 66, 66);
  border-color: white;
  border-width: 1;
  width: 225;
}
.header {
  color: cyan;
  font-size: 40;
}
.login {
  margin-top: 50;
  align-items: center;
  justify-content: center;
}

.buttons {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;
  margin-bottom: 50;
}
</style>

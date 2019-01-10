<template>
  <view class="container">
    <text>Location:</text>
    <text v-if="location.coords">{{location.coords.latitude}}</text>
    <text v-if="location.coords">{{location.coords.longitude}}</text>
    <text v-if="location.coords">{{location.coords.speed}}</text>

    <touchable-opacity :on-press="getLocation">
      <text>get location</text>
    </touchable-opacity>
  </view>
</template>

<script>
import { Constants, Location, Permissions } from "expo";

export default {
  beforeMount() {
    window.setInterval(this.getLocation, 500)
  },
  data() {
    return {
      location: {},
      errorMessage: ""
    };
  },
  methods: {
    getLocation: function() {
      Permissions.askAsync(Permissions.LOCATION)
        .then(status => {
          if (status !== "granted") {
            errorMessage = "Permission to access location was denied";
          }
          Location.getCurrentPositionAsync({ accuracy: 6 }).then(location1 => {
            location = location1;
            this.location = location;
            console.log(location.coords)
          });
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
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
</style>

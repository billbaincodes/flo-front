<template>
  <view class="container">
    <text>Location:</text>
    <text v-if="location.coords">Speed: {{speed}}</text>
    <text v-if="location.coords">Lat1: {{lat1}}</text>
    <text v-if="location.coords">Lon1: {{lon1}}</text>
    <text v-if="location.coords">Time1: {{time1}}</text>
    <text v-if="location.coords">Lat2: {{lat2}}</text>
    <text v-if="location.coords">Lon2: {{lon2}}</text>
    <text v-if="location.coords">Time2: {{time2}}</text>
    <text v-if="location.coords">LatDelta: {{latDelta}}</text>
    <text v-if="location.coords">LonDelta: {{lonDelta}}</text>
    <text v-if="location.coords">TimeDelta: {{timeDelta}}</text>

    <touchable-opacity :on-press="getLocation">
      <text>get location</text>
    </touchable-opacity>
  </view>
</template>

<script>
import { Constants, Location, Permissions } from "expo";

export default {
  beforeMount() {
    window.setInterval(this.getLocation, 200);
  },
  data() {
    return {
      location: {},
      errorMessage: "",
      speed: null,
      lat1: null,
      lon1: null,
      time1: null,
      lat2: null,
      lon2: null,
      time2: null,
      latDelta: null,
      lonDelta: null,
      timeDelta: null
    };
  },
  methods: {
    getLocation: function() {
      Permissions.askAsync(Permissions.LOCATION)
        .then(status => {
          if (status !== "granted") {
            errorMessage = "Permission to access location was denied";
          }
          Location.getCurrentPositionAsync({ accuracy: 6 }, obj => {
            console.log(obj);
          }).then(location1 => {
            console.log(location1);
            location = location1;
            this.location = location;

            if (this.lat1 == null) {
              this.lat1 = location.coords.latitude;
              this.lon1 = location.coords.longitude;
              this.time1 = location.timestamp;
            } else {
              this.lat2 = this.lat1;
              this.lon2 = this.lon1;
              this.time2 = this.time1;

              this.lat1 = location.coords.latitude;
              this.lon1 = location.coords.longitude;
              this.time1 = location.timestamp;
            }
            this.getChange()
            console.log(location);
          });
        })
        .catch(err => {
          console.log(err);
        });
    },
    getChange: function() {
      let timeDelta = this.time1 - this.time2;
      let latDelta = this.lat1 - this.lat2;
      let lonDelta = this.lon1 - this.lon2;

      this.latDelta = Math.abs(latDelta);
      this.lonDelta = Math.abs(lonDelta);
      this.timeDelta = timeDelta;

      let speed = (this.latDelta + this.lonDelta) / this.timeDelta;

      this.speed = speed;
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

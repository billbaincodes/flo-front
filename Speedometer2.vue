<template>
  <view>
  </view>
</template>


<script>
organizeDroppedObj = objs => {
  var toBeOrganized;
  if (this.state.organizedDroppedObjs === []) {
    toBeOrganized = this.state.droppedObjs;
  } else {
    toBeOrganized = objs;
  }

  navigator.geolocation.watchPosition(
    position => {
      let userLat = position.coords.latitude;
      let userLong = position.coords.longitude;
      let calcDistance = 0;
      for (let i = 0; i < toBeOrganized.length; i++) {
        calcDistance = latLongToDistanceAway(
          userLat,
          userLong,
          toBeOrganized[i].latitude,
          toBeOrganized[i].longitude
        );
        toBeOrganized[i].distance = calcDistance;
      }
      let organized = selectionSort(toBeOrganized);
      console.log("organized", organized);
      this.setState({
        organizedDroppedObjs: organized
      });
    },
    error => this.setState({ navError: true }),
    {
      enableHighAccuracy: true,
      distanceFilter: 1,
      timeout: 10000,
      maximumAge: 10000
    }
  );

  return "done";

  function selectionSort(array) {
    for (var i = 0; i < array.length; i++) {
      var min = i;
      for (var j = i + 1; j < array.length; j++) {
        if (array[j].distance < array[min].distance) {
          min = j;
        }
      }
      var temp = array[i];
      array[i] = array[min];
      array[min] = temp;
    }
    return array;
  }

  function latLongToDistanceAway(lat1, long1, lat2, long2) {
    var radiusEarth = 6371e3;

    //convert degrees to radians
    var lat1r = (lat1 * Math.PI) / 180;
    var lat2r = (lat2 * Math.PI) / 180;

    //difference lat and difference long in radians
    var dlat = ((lat2 - lat1) * Math.PI) / 180;
    var dlong = ((long2 - long1) * Math.PI) / 180;

    var a =
      Math.sin(dlat / 2) * Math.sin(dlat / 2) +
      Math.cos(lat1r) *
        Math.cos(lat2r) *
        Math.sin(dlong / 2) *
        Math.sin(dlong / 2);
    var c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
    return radiusEarth * c;
  }
};
</script>

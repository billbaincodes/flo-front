<template>
  <view class="container">
    <nb-form>
      <nb-item :style="{marginRight: 14}" stackedLabel>
        <nb-label :style="{color: 'white'}">First</nb-label>
        <nb-input v-model="first" defaultValue="Donnie" :style="{color: 'rgb(190, 190, 190)'}"/>
      </nb-item>
      <nb-item :style="{marginRight: 14}" stackedLabel>
        <nb-label :style="{color: 'white'}">Last</nb-label>
        <nb-input v-model="last" defaultValue="Denver" :style="{color: 'rgb(190, 190, 190)'}"/>
      </nb-item>
      <nb-item :style="{marginRight: 14}" stackedLabel>
        <nb-label :style="{color: 'white'}">Email</nb-label>
        <nb-input v-model="email" defaultValue="donnie@gmail.com" :style="{color: 'rgb(190, 190, 190)'}"/>
      </nb-item>
      <nb-item :style="{marginRight: 14}" stackedLabel>
        <nb-label :style="{color: 'white'}">Password</nb-label>
        <nb-input v-model="pass" secureTextEntry :style="{color: 'rgb(190, 190, 190)'}"/>
      </nb-item>
      <nb-item :style="{marginRight: 14}" stackedLabel>
        <nb-label :style="{color: 'white'}">Confirm Password</nb-label>
        <nb-input secureTextEntry :style="{color: 'rgb(190, 190, 190)'}"/>
      </nb-item>
    </nb-form>
    <view class="lower">
      <touchable-opacity
        :onPress="pickImage"
        class="login"
        :style="{backgroundColor: 'rgb(60, 60, 60)', height: 40, width: 130}"
      >
        <text class="text-color-primary">Upload Photo</text>
      </touchable-opacity>
      <touchable-opacity
        :onPress="submitChanges"
        class="login"
        :style="{backgroundColor: 'rgb(60, 60, 60)', height: 40, width: 130}"
      >
        <text class="text-color-primary">Save</text>
      </touchable-opacity>
    </view>
  </view>
</template>

<script>
export default {
  data: function() {
    return {
      first: false,
      last: false,
      email: false,
      pass: false,
      avatarURL: false
    };
  },
  props: {
    navigation: {
      type: Object
    }
  },
  methods: {
    pickImage: function() {
      Expo.ImagePicker.launchImageLibraryAsync({
        allowsEditing: true,
        aspect: [1, 1]
      });
    },
    submitChanges: function() {
      console.log("butz");
      let updates = this.$data;

      let payload = {};

      for (key in updates) {
        if (updates[key]) {
          payload[key] = updates[key];
        } else {
        }
      }

      this.editFetch(payload);
      this.navigation.goBack();
    },
    editFetch: function(payload) {
      fetch("https://flo-back.herokuapp.com/users/1", {
        method: "PUT",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify(payload)
      });
    }
  }
};
</script>

<style>
.lower {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-evenly;
}

.container {
  background-color: rgb(43, 43, 43);
  flex: 1;
  border-top-width: 3;
  border-color: cyan;
}

.text-color-primary {
  color: white;
  font-size: 18;
}

.login {
  margin-top: 50;
  align-items: center;
  justify-content: center;
}
</style>
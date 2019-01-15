<template>       
  <view class="container">
    <nb-form>
      <nb-item :style="{marginRight: 14}" floatingLabel>
        <nb-label :style="{color: 'white'}">First</nb-label>
        <nb-input value='Donny' :style="{color: 'white'}"/>
      </nb-item>
      <nb-item :style="{marginRight: 14}" floatingLabel >
        <nb-label :style="{color: 'white'}">Last</nb-label>
        <nb-input value='Denver' :style="{color: 'white'}"/>
      </nb-item>
      <nb-item :style="{marginRight: 14}" floatingLabel >
        <nb-label :style="{color: 'white'}">Email</nb-label>
        <nb-input value='donnie@gmail.com' :style="{color: 'white'}"/>
      </nb-item>
      <nb-item :style="{marginRight: 14}" floatingLabel >
        <nb-label :style="{color: 'white'}">Password</nb-label>
        <nb-input value='pass1234' secureTextEntry :style="{color: 'white'}"/>
      </nb-item>
    </nb-form>
    <view>
      <touchable-opacity :onPress="pickImage" class="login" :style="{backgroundColor: 'rgb(43, 43, 43)', height: 40, width: 90, borderWidth: 1, borderColor: 'rgb(180, 180, 180)'}">
        <text class="text-color-primary">Upload Profile Photo</text>
      </touchable-opacity>
      <touchable-opacity :onPress="submitChanges" class="login" :style="{backgroundColor: 'rgb(43, 43, 43)', height: 40, width: 90, borderWidth: 1, borderColor: 'rgb(180, 180, 180)'}">
        <text class="text-color-primary">Save</text>
      </touchable-opacity>
    </view>
  </view>
</template>

<script>

export default {
  props: {
    navigation: {
      type: Object
    }
  },
  methods: {
    pickImage : function() {
      Expo.ImagePicker.launchImageLibraryAsync({
      allowsEditing: true,
      aspect: [1, 1],
    });
    },
    submitChanges : function() {
      this.navigation.goBack()
    }

  }
}

</script>

<style>

.container {
  background-color: rgb(43, 43, 43);
  flex: 1; 
}

.login {
  margin-top: 50;
  align-items: center;
  justify-content: center;
}

</style>
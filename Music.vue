<template>
  <nb-container>
    <nb-header class="hider"/>
    <nb-content>
      <nb-list>
        <nb-list-item class="divider" :on-press="navAdd" itemDivider>
          <nb-text class="divider-text">Slow</nb-text>
          <nb-text class="divider-text" >+</nb-text>
        </nb-list-item>
        <nb-list-item class="divider">
          <nb-text>Walk Like an Egyptian - The Bangles</nb-text>
          <text>-</text>
        </nb-list-item>
        <nb-list-item class="divider" itemDivider>
          <nb-text class="divider-text">Medium</nb-text>
          <nb-text class="divider-text">+</nb-text>
        </nb-list-item>
        <nb-list-item class="divider">
          <nb-text>Born to Run - Bruce Springsteen</nb-text>
          <text>-</text>
        </nb-list-item>
        <nb-list-item class="divider" itemDivider>
          <nb-text class="divider-text">Fast</nb-text>
          <nb-text class="divider-text">+</nb-text>
        </nb-list-item>
        <nb-list-item class="divider">
          <nb-text>Through the Fire and the Flames - Dragonforce</nb-text>
          <nb-text>-</nb-text>
        </nb-list-item>
      </nb-list>
    </nb-content>
  </nb-container>
</template>

<script>
import trash from "./assets/pic-profile.png";

export default {
  props: {
    navigation: {
      type: Object
    }
  },
  methods: {
    navAdd: function() {
      this.navigation.navigate("addsong");
    }
  }
};
</script>

<style>
.hider {
  display: none;
}
.container {
  background-color: black;
  align-items: center;
  justify-content: center;
  flex: 1;
}
.text-color-primary {
  color: cyan;
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
  font-size: 60;
}
.divider {
  display: flex;
  justify-content: space-between;
}
.divider-text {
  font-weight: bold;
  font-size: 20;
}
</style>
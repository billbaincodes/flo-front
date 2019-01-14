<template>
  <nb-container class="body">
    <nb-header class="hider"/>
    <nb-content>
      <nb-list>
        <nb-list-item class="divider" :on-press="navAdd" itemDivider>
          <nb-text class="divider-text" :style="{color: 'cyan'}">Calm</nb-text>
          <image :style="{height: 18, width: 18}" :source="require('./assets/icon-menu.png')">
        </nb-list-item>
        <nb-list-item class="divider">
          <nb-text :style="{color: 'white'}">"Walk Like an Egyptian" - The Bangles</nb-text>
        </nb-list-item>
        <nb-list-item class="divider" :on-press="navAdd" itemDivider>
          <nb-text class="divider-text" :style="{color: 'cyan'}">Moderate</nb-text>
          <image :style="{height: 18, width: 18}" :source="require('./assets/icon-menu.png')">
        </nb-list-item>
        <nb-list-item class="divider">
          <nb-text :style="{color: 'white'}">"Born to Run" - Bruce Springsteen</nb-text>
        </nb-list-item>
        <nb-list-item class="divider">
          <nb-text :style="{color: 'white'}">"I Ran" - A Flock of Seagulls</nb-text>
        </nb-list-item>
        <nb-list-item class="divider" :on-press="navAdd" itemDivider>
          <nb-text class="divider-text" :style="{color: 'cyan'}">Intense</nb-text>
          <image :style="{height: 18, width: 18}" :source="require('./assets/icon-menu.png')">
        </nb-list-item>
        <nb-list-item class="divider">
          <nb-text :style="{color: 'white'}">"Through the Fire and the Flames" - Dragonforce</nb-text>
          <nb-text>-</nb-text>
        </nb-list-item>
      </nb-list>
    </nb-content>
  </nb-container>
</template>

<script>
import trash from "./assets/pic-profile.png";

export default {
  data: function() {
    return {
      playlist: {
        slo: [],
        med: [],
        fast: []
      }
    };
  },
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
.body {
  background-color: rgb(43, 43, 43);
  border-top-width: 4;
  border-bottom-width: 4;
  border-color: cyan;
}
.hider {
  display: none;
}
.container {
  background-color: rgb(43, 43, 43);
  align-items: center;
  justify-content: center;
  flex: 1;
  border-top-width: 4px;
  border-color: cyan;
}
.text-color-primary {
  color: cyan;
}
.text-input {
  color: white;
  background-color: rgb(43, 43, 43);
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
  background-color: rgb(43, 43, 43);
}
.divider:first-child {
  border-top-width: 4px;
  border-color: cyan;
}

.divider-text {
  font-weight: bold;
  font-size: 20;
}
</style>
<template>
  <nb-list-item class="divider">
    <nb-text class="song-text">{{item.title}}</nb-text>
  </nb-list-item>
</template>

<script>
export default {
  props: {
    item: {
      Type: Object
    }
  }
};
</script>

<style>
.divider {
  display: flex;
  justify-content: space-between;
  background-color: rgb(43, 43, 43);
}
.song-text {
  color: white;
}
</style>
<template>
<view class="container">
  <text class="text-container" v-for="todo in todos" :key="todo.text">
    {{ todo.text }}
  </text>
</view>
</template>

<script>
export default {
  data: function() {
    return {
      todos: [
        { text: "Learn JavaScript" },
        { text: "Learn Vue" },
        { text: "Build something awesome" }
      ]
    };
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
.text-container {
  color: blue;
  padding: 2;
}
</style>
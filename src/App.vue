<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <task-list />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import TaskList from './components/TaskList.vue';
import TaskItem from './components/TaskItem.vue';

Vue.component('task-list', TaskList);
Vue.component('task', TaskItem);

export default Vue.extend({
  name: 'app',
  components: {},
});
</script>

<style>
#app {
  text-align: center;
  margin-top: 60px;
}
</style>

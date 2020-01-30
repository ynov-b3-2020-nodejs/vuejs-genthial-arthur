<template>
  <main class="task-list">
    <h1>Vue Todolist</h1>
    <div class="add">
      <input type="text" v-model="newTaskText" />
      <button type="button" v-on:click="addTask()">Add task</button>
    </div>
    <div class="list">
      <h2>To Do</h2>
      <task
        v-for="task in nonCompletedTasks"
        :key="task.id"
        :task="task"
        v-bind:done.sync="task.done"
      />
    </div>

    <div class="list">
      <h2>Done</h2>
      <task
        v-for="task in completedTasks"
        :key="task.id"
        :task="task"
        v-bind:done.sync="task.done"
      />
    </div>
  </main>
</template>

<script lang="ts">
import {
  createComponent,
  ref,
  Ref,
  reactive,
  watch,
  computed,
} from '@vue/composition-api';
import TaskItem from 'Task.vue';
import { Task } from '../task';

export default createComponent({
  setup() {
    const { taskList, nonCompletedTasks, completedTasks } = useTaskList();
    const { newTaskText, addTask } = useAddTask(taskList);

    return {
      taskList,
      newTaskText,
      addTask,
      nonCompletedTasks,
      completedTasks,
    };
  },
});


function useTaskList() {

  const taskList = ref<Task[]>([]);


  const nonCompletedTasks = computed(() =>
    taskList.value.filter((task) => task.done === false)
  );
  const completedTasks = computed(() =>
    taskList.value.filter((task) => task.done === true)
  );

  return { taskList, nonCompletedTasks, completedTasks };
}

function useAddTask(taskList: Ref<Task[]>) {
  const newTaskText = ref('');

  function addTask() {

    const newId = Math.round(Math.random() * 100);

    taskList.value.push(
      reactive({ taskText: newTaskText.value, id: newId, done: false })
    );
    newTaskText.value = '';
  }

  return { newTaskText, addTask };
}
</script>

<style scoped>
.task-list .add {
  display: flex;
  flex-direction: row;
  justify-content: center;
  padding: 1em;
}


</style>

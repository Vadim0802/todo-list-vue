<template>
  <div class="control-panel">
    <form v-on:submit.prevent="addTask">
      <div class="mb-3">
        <h2 class="display-4">Заметка</h2>
        <input type="text" class="form-control" name="task-name" required>
      </div>
      <button type="submit" class="btn btn-primary">Добавить</button>
    </form>
  </div>
  <h3 class="display-6">Число заметок: {{tasks.length}}</h3>
  <br>
  <div class="container-xxl">
    <ul class="list-group" v-if="tasks.length !== 0">
      <li
          class="list-group-item"
          v-for="(task, index) in tasks"
          v-bind:key="task"
      >
        <samp>{{ task }}</samp>
        <button class="btn btn-danger" v-on:click="removeTask(index)">Удалить</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    addTask(event) {
      const formData = new FormData(event.target);
      const nameTask = formData.get('task-name');

      if (!this.tasks.includes(nameTask)) {
        this.tasks.push(nameTask);
      }
    },
    removeTask(index) {
      this.tasks = this.tasks.filter((_, idx) => index !== idx);
    },
  },
};
</script>

<style>
  .list-group-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .control-panel {
    width: 400px;
  }
</style>

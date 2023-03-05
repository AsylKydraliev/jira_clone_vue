<template>
  <div class="container mt-5">
    <div class="col-5">
      <div class="d-flex gap-2">
        <b-form-input
            v-model="newTask"
            placeholder="New task"
            @keyup.enter="add"
        />
        <b-button variant="primary" class="ml-3 col-2" @click="add">Add</b-button>
      </div>
    </div>

    <div class="row mt-3">
      <div class="col-md-3">
        <div class="p-2 alert alert-secondary">
          <h3>Todos</h3>
          <draggable class="list-group kanban-column" :list="todos" group="todos">
            <div class="list-group-item" v-for="todo in todos" :key="todo.name">
              {{ todo.name }}
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 alert alert-primary">
          <h3>In progress</h3>
          <draggable class="list-group kanban-column" :list="inProgress" group="todos">
            <div class="list-group-item" v-for="todo in inProgress" :key="todo.name">
              {{ todo.name }}
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 alert alert-warning">
          <h3>On tested</h3>
          <draggable class="list-group kanban-column" :list="onTested" group="todos">
            <div class="list-group-item" v-for="todo in onTested" :key="todo.name">
              {{ todo.name }}
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-md-3">
        <div class="p-2 alert alert-success">
          <h3>Done</h3>
          <draggable class="list-group kanban-column" :list="done" group="todos">
            <div class="list-group-item" v-for="todo in done" :key="todo.name">
              {{ todo.name }}
            </div>
          </draggable>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { VueDraggableNext } from "vue-draggable-next";

export default {
  name: 'App',

  components: {
    draggable: VueDraggableNext
  },

  data() {
    return {
      newTask: '',
      todos: [
        {name: "Code Sign Up Page"},
        {name: "Test dashboard"},
        {name: "Style registration"},
        {name: "Help with design"}
      ],
      inProgress: [],
      onTested: [],
      done: [],
    }
  },

  methods: {
    add() {
      if (this.newTask) {
        this.todos.push({name: this.newTask});
        this.newTask = "";
      }
    }
  }
}
</script>

<style>
.kanban-column {
  min-height: 500px;
}
</style>

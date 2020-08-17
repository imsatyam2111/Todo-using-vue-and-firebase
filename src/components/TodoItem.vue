<template>
  <div class="container-fluid todos mt-4 mx-auto">
    <!-- Get Todo Items -->
    <div
      class="row todo-item font-weight-bold text-left px-2 py-3"
      v-for="currentTodo in todos"
      :key="currentTodo.id"
    >
      <div class="col-sm todo-details">
        <div>
          <!-- Checkbox -->
          <span v-if="isEditing !== currentTodo.id">
            <input
              class="checkbox mr-2"
              type="checkbox"
              v-bind:checked="currentTodo.completed"
              v-on:change="markComplete(currentTodo)"
            />
            <span v-bind:class="{ 'is-complete': currentTodo.completed }">
              {{ currentTodo.title }}
            </span>
          </span>

          <!-- Edit:input box -->
          <span v-if="isEditing == currentTodo.id">
            <input
              class="pl-2 py-1 border-rounded mr-1 w-50"
              type="text"
              v-model="newTitle"
              v-on:keyup.enter="update(currentTodo)"
            />
            <!-- todo update button -->
            <button
              class="update-btn btn btn-info"
              v-on:click="update(currentTodo)"
            >
              Update
            </button>
          </span>
        </div>
      </div>

      <!-- Todo Controls -->
      <div class="col-sm todo-controls">
        <div class="float-right todo-buttons">
          <!-- Edit Button -->
          <span v-show="isEditing !== currentTodo.id">
            <button class="button mr-2 edit" @click="edit(currentTodo)">
              <i class="far fa-edit"></i>
            </button>
          </span>
          <!-- Delete button -->
          <button
            v-if="isEditing !== currentTodo.id"
            class="button del"
            @click="deleteTodo(currentTodo.id)"
          >
            <i class="fas fa-trash"></i>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import db from "./firebaseInit";

export default {
  components: {},
  props: ["todos"],
  data() {
    return {
      newTitle: "",
      isEditing: 0
    };
  },
  methods: {
    markComplete: function(currentTodo) {
      db.collection("todos")
        .doc(currentTodo.id)
        .update({ completed: !currentTodo.completed });
      currentTodo.completed = !currentTodo.completed;
    },
    deleteTodo: function(id) {
      // alert(id)
      if (confirm("Are you sure?")) {
        db.collection("todos")
          .doc(id)
          .delete();
      }
    },
    edit: function(currentTodo) {
      this.isEditing = currentTodo.id;
      this.newTitle = currentTodo.title;
    },
    update: function(currentTodo) {
      this.isEditing = false;
      db.collection("todos")
        .doc(currentTodo.id)
        .update({ title: this.newTitle });
    }
  }
};
</script>

<style scoped>
.todo-item {
  font: 1.2em;
  font-family: sans-serif;
  border-bottom: 1px solid #aaa;
}
.is-complete {
  text-decoration: line-through;
  color: #444;
}
/* .update-btn {
  background-color: #2bb62b;
  color: #eee;
  border: none;
  height: 30px;
} */
.update-btn:hover {
  background-color: #0c8b0c;
}
.button {
  background: transparent;
  border: none;
  width: 50px;
}
.button:focus {
  outline: none;
}
.del:hover {
  color: red;
  transform: scale(1.2);
}
.edit:hover {
  transform: scale(1.1);
}
@media (max-width: 576px) {
  .todo-buttons {
    float: left !important;
    margin-top: 10px;
    margin-left: 30%;
  }
  .todo-controls {
    text-align: center;
  }
}
</style>

<template>
  <div id="todoApp" class="container rounded-lg mt-5 px-5 pt-5 pb-5">
    <h1 class="text-dark text-center pb-5">A Very Amazing Todo</h1>

    <form v-on:submit.prevent="addTodo">
      <div id="form-group" class="mx-auto">
        <input
          v-model="title"
          class="todo-text my-1 d-block form-control"
          type="text"
          name="title"
          placeholder="Write a Todo Here"
        />
        <button class="add-btn btn-primary form-control" type="submit">
          <i class="fas fa-plus"></i>
        </button>
      </div>
    </form>

    <div class="todo-container">
      <TodoItem v-bind:todos="todos" />
    </div>
  </div>
</template>

<script>
import TodoItem from "@/components/TodoItem.vue";
import db from "./firebaseInit";

export default {
  name: "App",
  components: {
    TodoItem
  },
  data() {
    return {
      todos: [],
      title: "",
      id: 4
    };
  },
  created() {
    db.collection("todos").onSnapshot(snapshot => {
      snapshot.docChanges().forEach(change => {
        if (change.type == "added") {
          this.todos.push({
            id: change.doc.id,
            title: change.doc.data().title,
            completed: change.doc.data().completed
          });
        } else if (change.type == "removed") {
          this.todos = this.todos.filter(todo => todo.id !== change.doc.id);
        } else if (change.type == "modified") {
          this.todos = this.todos.map(todo => {
            if (todo.id == change.doc.id) {
              return { ...change.doc.data(), id: change.doc.id };
            }
            return todo;
          });
        }
      });
    });
  },
  methods: {
    addTodo: function() {
      if (this.title !== "") {
        db.collection("todos").add({
          title: this.title,
          completed: false
        });
        this.title = "";
      } else {
        alert("cannot add blank todo");
      }
    }
  }
};
</script>

<style scoped>
#todoApp {
  border: 2.5px solid #bdbbbb;
  box-shadow: 8px 8px 15px rgb(175, 173, 173) ;
}
</style>

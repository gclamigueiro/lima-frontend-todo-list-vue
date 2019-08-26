<template>
  <div id="app">
    <div class="container">
      <img width="15%" src="./assets/logo.png">

      <h2 class="title">Lima Frontend To do List</h2>

      <div class="stats">
        <div class="stat">
          <label>Total:</label>
          <span>{{ todos.length }}</span>
        </div>
        <div class="stat">
          <label>Realizadas:</label>
          <span>{{ getAmountDone }}</span>
        </div>

        <div class="new-todo">
          <input
            class="new-todo-textbox"
            type="text"
            placeholder="Agregar Nuevo"
            v-model="newTodo"
            @keypress.enter="createTodo"
          >
        </div>
      </div>

      <transition-group name="list" tag="div" class="row todo-list">
        <todo-element
          v-for="(todo,index) in todos"
          :key="todo.id"
          :todo="todo"
          :position="index"
          @remove="remove"
        ></todo-element>
      </transition-group>
    </div>
  </div>
</template>

<script>
import TodoElement from "./components/TodoElement.vue";

export default {
  name: "App",
  components: {
    TodoElement
  },
  data() {
    return {
      todos: [
        { id: 1, text: "Iniciar proyecto con vue cli", done: false },
        { id: 2, text: "Crear componente Todo Element", done: false },
        { id: 3, text: "usar v-for sobre los Todos", done: true },
        { id: 4, text: "..", done: true },
        { id: 5, text: "..", done: true },
        { id: 6, text: "...", done: true }
      ],
      newTodo: "",
      nextId: 7
    };
  },
  computed: {
    getAmountDone: function() {
      return this.todos.filter(t => t.done).length;
    }
  },
  watch: {
    getAmountDone: function(newVal) {
      if (newVal === this.todos.length) {
        console.log("All done");
      }
    }
  },
  methods: {
    createTodo() {
      const text = this.newTodo;
      if (text !== "") {
        this.todos.push({
          id: this.nextId,
          text: text,
          done: false
        });

        this.newTodo = "";
        this.nextId += 1;
      }
    },
    remove(position) {
      this.todos.splice(position, 1);
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Montserrat:400,700");

body {
  background-color: #EEEEEE;
  font-family: "Montserrat", sans-serif;
}
#app {
  text-align: center;
  color: #3E5252;
  margin-top: 20px;
}

.title {
  margin-top: 0px;
  margin-bottom: 25px;
}

.todo-list {
  margin-top: 2px;
  display: flex;
  flex-direction: row;
  justify-content: left;
  flex-wrap: wrap;
}

.stats {
  font-family: "Monserrat";
  text-align: left;
  font-size: 12px;
  font-weight: bold;
  margin-bottom: 12px;
}
.stat label {
  margin-right: 8px;
}
.stat {
  margin-top: 12px;
}

.new-todo-textbox {
  margin-top: 12px;
  border-radius: 0px;
  background-color: white;
  border: none;
  height: 40px;
  text-align: center;
  border-left: 5px solid #3EB3F6;
}
.new-todo-textbox::placeholder {
  text-align: center;
}

.list-enter-active,
.list-leave-active {
  transition: all 0.5s;
}
.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
</style>

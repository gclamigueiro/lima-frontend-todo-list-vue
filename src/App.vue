<template>
  <div id="app">
    <div class="container">
      <img width="15%" src="./assets/logo.png">

      <h2 class="title">Lima Frontend To do List</h2>

      <div class="stats">
        <div class="stat">
          <label>Total:</label>
          <span>{{ tasks.length }}</span>
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
            v-model="newTask"
            @keydown.enter="createTask"
          >
        </div>
      </div>

      <transition-group name="list" tag="div" class="row todo-list">
        <todo-element
          v-for="(task,index) in tasks"
          :key="task.id"
          :todo="task"
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
      tasks: [
        { id: 1, text: "Iniciamos el proyecto con el Vue CLI", done: true },
        { id: 2, text: "Creamos componente ToDo Element", done: false },
        { id: 3, text: "función data() ", done: false },
        {
          id: 4,
          text:
            "Si fuera un proyecto real muchos datos se traerían desde un API",
          done: false
        },
        {
          id: 5,
          text: "Vamos a usar la directiva v-for para recorrer las tareas",
          done: false
        },
        { id: 6, text: "Ponemos unos contadores cools :)", done: false },
        {
          id: 7,
          text:
            "Nos fijamos en la reactividad, como Vue se encarga de cambiar la vista",
          done: false
        },
        { id: 8, text: "propiedades computed, que son?", done: false },
        { id: 9, text: "insertando nueva tarea. Data Binding", done: false },
        { id: 10, text: "Manejando eventos", done: false },
        { id: 11, text: "Enviando datos al componente padre", done: false },
        { id: 12, text: "Router", done: false },
        { id: 12, text: "Ciclo de vida de los componentes (Instance Lifecycle Hooks)", done: false },


      ],
      newTask: "",
      nextId: 12
    };
  },
  computed: {
    getAmountDone: function() {
      return this.tasks.filter(t => t.done).length;
    }
  },
  methods: {
    createTask() {
      const text = this.newTask;
      if (text !== "") {
        this.tasks.push({
          id: this.nextId,
          text: text,
          done: false
        });

        this.newTask = "";
        this.nextId += 1;
      }
    },
    remove(position) {
      this.tasks.splice(position, 1);
    }
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Montserrat:400,700");
@import url("https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/4.3.1/css/bootstrap-grid.min.css");

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
  width: 200px;
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

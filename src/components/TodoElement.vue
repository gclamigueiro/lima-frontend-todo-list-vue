<template>
  <div class="col-6 col-sm-4 col-md-3 col-lg-2">
    <div class="todo" :class="{done: todo.done}">
      <div class="checkbox">
        <input :id="position" class="cbx" 
        type="checkbox" v-model="todo.done">
        <label :for="position" class="check">
          <svg width="18px" height="18px" viewBox="0 0 18 18">
            <path
              d="M1,9 L1,3.5 C1,2 2,1 3.5,1 L14.5,1 C16,1 17,2 17,3.5 L17,14.5 C17,16 16,17 14.5,17 L3.5,17 C2,17 1,16 1,14.5 L1,9 Z"
            ></path>
            <polyline points="1 9 7 14 15 4"></polyline>
          </svg>
        </label>
      </div>

      <h6 class="text">{{todo.text}}</h6>
      <span class="delete" @click="remove()">eliminar</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "todo-element",
  props: ["todo", "position"],
  methods: {
    remove() {
      this.$emit("remove", this.position);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo {
  margin: 10px 0px;
  width: 100%;
  height: 150px;
  box-shadow: 4px 4px 4px rgba(0, 0, 0, 0.3);
  padding: 8px;
  position: relative;
  /*background-color: rgb(238, 232, 232);*/
  font-size: 1.1em;
  background-color: #E0EDF4;
  border-left: 5px solid #3EB3F6;
  color: #3E5252;
  display: inline-block;
}

/* 
Si se desea que cuando la tarea este realizada cambie la visualidad
se puede poner en esta clase
*/
/*.done {

  border-left: 5px solid rgba(104, 236, 104, 0.588);
}*/

.text {
  padding: 12px;
  margin: 0;
  position: absolute;
  top: 50%;
  left: 50%;
  margin-right: -50%;
  transform: translate(-50%, -50%);
}

.delete {
  position: absolute;
  bottom: 8px;
  left: 0px;
  font-size: 12px;
  text-align: center;
  width: 100%;
  color: gray;
  cursor: pointer;
}

/* checkbox css*/
.checkbox {
  float: right;
}
.cbx {
  display: none;
}

.check {
  cursor: pointer;
  position: relative;
  margin: auto;
  width: 18px;
  height: 18px;
  -webkit-tap-highlight-color: transparent;
  transform: translate3d(0, 0, 0);
}
.check:before {
  content: "";
  position: absolute;
  top: -15px;
  left: -15px;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background: rgba(34, 50, 84, 0.03);
  opacity: 0;
  transition: opacity 0.2s ease;
}
.check svg {
  position: relative;
  z-index: 1;
  fill: none;
  stroke-linecap: round;
  stroke-linejoin: round;
  stroke: #c8ccd4;
  stroke-width: 1.5;
  transform: translate3d(0, 0, 0);
  transition: all 0.2s ease;
}
.check svg path {
  stroke-dasharray: 60;
  stroke-dashoffset: 0;
  transition: all 0.3s linear;
}
.check svg polyline {
  stroke-dasharray: 22;
  stroke-dashoffset: 66;
  transition: all 0.3s linear;
}
.check:hover:before {
  opacity: 1;
}
/*.check:hover svg {
  stroke: #4285f4;
}*/
.cbx:checked:checked + .check svg {
  stroke: #4285f4;
}
.cbx:checked + .check svg path {
  stroke-dashoffset: 60;
  transition: all 0.3s linear;
}
.cbx:checked + .check svg polyline {
  stroke-dashoffset: 42;
  transition: all 0.2s linear;
  transition-delay: 0.15s;
}
</style>

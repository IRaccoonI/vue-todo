<template>
  <div>
    <div class="header rounded-top border border-bottom-0">
      <h2>Todos</h2>
    </div>
    <div>
      <b-input-group class="rounded-0 rounded-top">
        <b-form-input v-model="newTodoMsg" class="rounded-0"></b-form-input>
        <b-button variant="success" class="px-3 rounded-0" @click="addTodo"
          >Add</b-button
        >
      </b-input-group>
      <b-button variant="warning" class="w-100 rounded-0" @click="clearTodo"
        >Clear</b-button
      >
    </div>
    <div class="el-wrapper card p-0 rounded-0 rounded-bottom">
      <TodoEl
        v-for="(todo, i) in todoItems"
        :key="i"
        :msg="todo.msg"
        :isChecked="todo.isChecked"
        :isFirst="i == 0"
        :isLast="i == todoItems.length - 1"
        @deleteTodo="deleteTodo(i)"
        @moveTodoKeyUp="moveTodoKey(i, -1)"
        @moveTodoKeyDown="moveTodoKey(i, 1)"
        @toggleChecked="toggleChecked(i)"
        class="px-2"
      ></TodoEl>
    </div>
  </div>
</template>

<script>
import TodoEl from "./TodoEl";

export default {
  props: {
    user: String,
  },
  components: {
    TodoEl,
  },
  methods: {
    addTodo: function () {
      this.todoItems.push({ msg: this.newTodoMsg, isChecked: false });
      this.newTodoMsg = "";
    },
    clearTodo: function () {
      this.todoItems = [];
    },
    deleteTodo: function (ind) {
      this.todoItems.splice(ind, 1);
    },
    moveTodoKey: function (ind, offset) {
      let todoItems = this.todoItems;
      if (ind + offset >= 0 && ind + offset < todoItems.length) {
        let rows = [todoItems[ind], todoItems[ind + offset]];
        if (offset >= 0) {
          todoItems.splice(ind, 2, rows[1], rows[0]);
        } else {
          todoItems.splice(ind + offset, 2, rows[0], rows[1]);
        }
      }
    },
    toggleChecked: function (ind) {
      this.todoItems[ind].isChecked = !this.todoItems[ind].isChecked;
    },
  },
  data() {
    return {
      newTodoMsg: "",
      todoItems: [
        {
          msg: "Add todo",
          isChecked: false,
        },
        {
          msg: "Coockie",
          isChecked: false,
        },
        {
          msg: "Dota2",
          isChecked: true,
        },
      ],
    };
  },
};
</script>

<style scoped>
.header {
  background-color: rgb(238, 255, 239);
}
.header > h2 {
  height: 60px;
  line-height: 60px;
  margin-bottom: 0;
}

.el-wrapper > *:nth-of-type(2n) {
  background: rgba(122, 122, 122, 0.123);
}
.el-wrapper > *:nth-of-type(2n + 1) {
  background: rgba(218, 218, 218, 0.11);
}

.rounded-be-0 {
  border-bottom-right-radius: 0 !important;
}
.rounded-bs-0 {
  border-bottom-left-radius: 0 !important;
}
</style>
    
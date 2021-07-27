<template>
  <div class="el d-flex">
    <div class="">
      <b-button
        @click="$emit('toggleChecked')"
        class="c-button"
        :class="{ 'btn-success': isChecked, 'btn-light': !isChecked }"
      ></b-button>
    </div>
    <div class="message flex-grow-1 text-start mx-4">
      <span :class="{ 'text-decoration-line-through': isChecked }">
        {{ msg }}
      </span>
    </div>
    <div>
      <b-button-toolbar>
        <b-button-group>
          <b-button
            v-if="!isFirst"
            :class="{ 'btn-long': isLast }"
            title="Todo up"
            variant="outline-dark"
          >
            <b-icon
              icon="arrow-up"
              aria-hidden="true"
              @click="$emit('moveTodoKeyUp')"
            ></b-icon>
          </b-button>
          <b-button
            v-if="!isLast"
            :class="{ 'btn-long': isFirst }"
            title="Todo down"
            variant="outline-dark"
          >
            <b-icon
              icon="arrow-down"
              aria-hidden="true"
              @click="$emit('moveTodoKeyDown')"
            ></b-icon>
          </b-button>
          <b-button title="Remove todo" variant="outline-dark">
            <b-icon
              icon="clipboard-x"
              aria-hidden="true"
              @click="$emit('deleteTodo')"
            ></b-icon>
          </b-button>
        </b-button-group>
      </b-button-toolbar>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
    isChecked: Boolean,
    isFirst: Boolean,
    isLast: Boolean,
  },
  components: {},
};
</script>

<style scoped>
.c-button {
  height: 26px;
  width: 68px;
  border: 1px solid black;
}
.el {
  height: 26px;
  padding: 8px 0;
  box-sizing: content-box;
  transition: background-color 0.2s linear;
}
.el:hover {
  background-color: rgb(255, 231, 211) !important;
}
.check-input {
  height: 26px;
}
.message {
  font-size: 1.2em;
  line-height: 26px;
}
.btn {
  padding: 0 5px;
}
.btn-long {
  width: 64px;
}
</style>
    
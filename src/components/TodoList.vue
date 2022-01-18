<template>
  <section>
    <ul>
      <TodoItem v-for="item in todos" :key="item.id" :todo="item" @checkHandler="childEcho" @deleteTodo="deleteTodo"/>
    </ul>
    <article>
        <input type="text" v-model="inputValue" @keyup.enter="$emit('addTodo', inputValue); inputValue = ''"/>
        <button @click="$emit('addTodo', inputValue); inputValue = ''"></button>
    </article>
  </section>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  props: {
    todos: Array,
  },
  components: { TodoItem },
  data() {
      return  {
          inputValue: null
      }
  },
  methods: {
    childEcho(todo){
      this.$emit("checkHandler", todo)
    },
    deleteTodo(todo){
      this.$emit('deleteTodo', todo)
    }
  }
};
</script>

<style scoped>
button{
    padding: 1rem;
}
</style>
<template>
  <div>
    <div v-bind:key="todo.id" v-for="todo in todos_list">
      <Item
        v-bind:list="todos_list"
        v-bind:todo_item="todo"
        v-on:delete-todo="deleteTodo"
        v-on:add-nested-todo="PassAlongInfo"
        v-on:add-done-butt="CreateDone"
      >
      </Item>
      <!-- <NestedAddItem v-on:cancel="cancelInput" id="nested_prompter" /> -->
    </div>
  </div>
</template>

<script>
import Item from './Item.vue'
export default {
  name: 'Todos',
  components: {
    Item
  },
  data() {
    return {
      minitodos: []
    }
  },

  props: ['todos_list'],

  methods: {
    deleteTodo(id) {
      //console.log(id)
      this.$emit('delete-todo', id)
    },
    CreateDone(x) {
      console.log('Hi:', x)
    },
    PassAlongInfo(x) {
      //console.log('this is third step')
      var newNestedTodo = x.newNestedTodo
      var parentid = x.parentid
      //console.log(newNestedTodo)
      this.$emit('add-nested-todo', {
        newNestedTodo,
        parentid
      })
    }
  }
}
</script>

<style scoped></style>

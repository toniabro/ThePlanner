<template>
  <div class="about">
    <Header title="Todo List"></Header>
    <AddItem v-on:add-todo="addTodo" />
    <List
      v-bind:todos_list="todos"
      v-on:delete-todo="deleteTodo"
      v-on:add-nested-todo="addNestedTodo"
    />
  </div>
</template>

<script>
import Header from '../components/Header.vue'
import List from '../components/todo_components/List.vue'
import AddItem from '../components/todo_components/Add_Item.vue'
import NestedItem from '../components/todo_components/Nested_Item.vue'
export default {
  name: 'todo',
  components: {
    Header,
    List,
    AddItem,
    //NestedItem
  },

  data() {
    return {
      todos: [
        {
          id: 0,
          title: 'Zero',
          completed: false,
          date: 'April 0',
          hasChildren: false,
          children: []
        },
        {
          id: 1,
          title: 'First',
          completed: false,
          date: 'April 1',
          hasChildren: true,
          children: [
            {
              id: 1.1,
              title: 'Firsts First Child',
              completed: false,
              date: 'April 30'
            },
            {
              id: 1.2,
              title: 'Firsts Second Child',
              completed: false,
              date: 'April 31'
            }
          ]
        },
        {
          id: 2,
          title: 'Second',
          completed: false,
          date: 'April 2',
          hasChildren: false,
          children: []
        },
        {
          id: 3,
          title: 'Third',
          completed: false,
          date: 'April 3',
          hasChildren: true,
          children: [
            {
              id: 3.1,
              title: 'Thirds First Child',
              completed: false,
              date: 'June 2'
            }
          ]
        }
      ]
    }
  },

  methods: {
    deleteTodo(id) {
      var stop = false
      var prevLength = this.todos.length

      this.todos = this.todos.filter(todo => todo.id != id)
      if (prevLength == this.todos.length) {
        for (var i = 0; i < this.todos.length; i++) {
          if (this.todos[i].hasChildren) {
            for (var j = 0; j < this.todos[i].children.length; j++) {
              if (id == this.todos[i].children[j].id) {
                this.todos[i].children = this.todos[i].children.filter(
                  todo => todo.id != id
                )
                stop = true
                break
              }
            }
            if (stop == true) {
              break
            }
          }
        }
      }
    },

    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo]
    },

    addNestedTodo(input) {
      //console.log("This is it")
      //console.log(input.newNestedTodo)
      //console.log(input.parentid)
      var i = 0
      //This finds the index of the id
      for (; i < this.todos.length; i++) {
        if (input.parentid == this.todos[i].id) {
          break
        }
      }
      this.todos[i].children.push(input.newNestedTodo)
      this.todos[i].hasChildren = true
      //this.todos[i].children = [...this.todos[i].children, input.newNestedTodo]
      //console.log(this.todos[i].children)
    }
  }
}
</script>

<style scoped>
* {
  box-sizing: border-box;
  padding: 0;
}
</style>

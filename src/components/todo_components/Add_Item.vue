<template>
  <div>
    <form @submit="addTodo">
      <input
        type="text"
        v-model="title"
        name="title"
        placeholder="Add Todo..."
      />
      <input
        type="text"
        v-model="date"
        name="date"
        class="date_field"
        placeholder="Add date..."
      />
      <input type="submit" value="Submit" class="button" />
    </form>
  </div>
</template>

<script>
import uuid from 'uuid'
export default {
  name: 'AddItem',
  data() {
    return {
      title: '',
      date: ''
    }
  },

  methods: {
    addTodo(e) {
      e.preventDefault()
      const newTodo = {
        id: uuid.v4(),
        title: this.title,
        completed: false,
        date: this.date,
        hasChildren: false,
        children: []
      }
      //Send to Parent todo.vue
      this.$emit('add-todo', newTodo)
      this.title = ''
      this.date = ''
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
}

input[type='text'] {
  flex: 10;
  padding: 5px;
  background: white;
  border: 2px solid black;
}

input[type='submit'] {
  flex: 2;
}

.button {
  display: inline-block;
  background: #555;
  color: #fff;
  padding: 10px 10px;
  cursor: pointer;
}

.button:hover {
  background: #666;
}
</style>

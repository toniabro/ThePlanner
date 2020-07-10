<template>
  <div>
    <form @submit="addNestedTodo">
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
      <input
        type="button"
        @click="$emit('cancel')"
        value="Cancel"
        class="button"
      />
    </form>
  </div>
</template>

<script>
import uuid from 'uuid'
export default {
  name: 'NestedAddItem',
  data() {
    return {
      title: '',
      date: ''
    }
  },

  methods: {
    addNestedTodo(e) {
      e.preventDefault()
      var parentid = this.parent_id
      const newNestedTodo = {
        id: uuid.v4(),
        title: this.title,
        completed: false,
        date: this.date
      }
      //Send to Parent todo.vue
      //console.log(parentid)
      //console.log(newNestedTodo)
      //console.log('this is first step')
      //this.$emit('add-nested-todo', newNestedTodo)
      this.$emit('add-nested-todo', {
        newNestedTodo,
        parentid
      })
      this.$emit('cancel')
      this.title = ''
      this.date = ''
    }
  },
  props: ['parent_id']
}
</script>

<style scoped>
form {
  display: flex;
  width: 80%;
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
  padding: 8px 8px;
  cursor: pointer;
  border: 1px solid black;
}

.button:hover {
  background: #666;
}
</style>

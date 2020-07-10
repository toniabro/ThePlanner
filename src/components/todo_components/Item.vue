<template>
  <div>
    <div class="item" v-bind:class="{ completed: todo_item.completed }">
      <p name="textone" contenteditable="false">
        <button
          @click="deleteItem(todo_item.id)"
          class="delete"
          contenteditable="false"
        >
          X
        </button>
        <span v-if="this.isChild != true">
          <button
            @click="setPromptTrue(todo_item.id)"
            contenteditable="false"
            class="add"
          >
            +
          </button>
        </span>
        <button
          @click="editItem(todo_item)"
          class="edit"
          contenteditable="false"
        >
          <v-icon id="editbut">mdi-pencil</v-icon>
        </button>
        <input
          type="checkbox"
          v-on:change="markComplete"
          contenteditable="false"
        />
        {{ todo_item.title }}
      </p>
      <p class="date" name="texttwo" contenteditable="false">
        Due: {{ todo_item.date }}
      </p>
    </div>
    <div v-if="todo_item.hasChildren" class="childTodo">
      <div v-bind:key="child.id" v-for="child in todo_item.children">
        <Item
          v-bind:isChild="true"
          v-bind:todo_item="child"
          v-bind:list="list"
          v-on:delete-todo="deleteItem"
        ></Item>
      </div>
    </div>
    <div v-if="nestedPrompt">
      <NestedAddItem
        v-bind:parent_id="todo_item.id"
        v-on:cancel="setPromptTrue()"
        v-on:add-nested-todo="passAlongInfo"
        id="nested_prompter"
      />
    </div>
    <div v-if="editFlag">
      <DoneButt
        name="doneBut"
        v-on:destroy="editItemDone(todo_item)"
      ></DoneButt>
    </div>
  </div>
</template>

<script>
import NestedAddItem from './Nested_Item'
import DoneButt from './Done_Button'
export default {
  name: 'Item',
  components: {
    NestedAddItem,
    DoneButt
  },
  data() {
    return {
      nestedPrompt: false,
      editFlag: false
    }
  },
  props: ['todo_item', 'isChild', 'list'],
  methods: {
    markComplete() {
      this.todo_item.completed = !this.todo_item.completed
    },
    deleteItem(id) {
      //console.log(id)
      this.$emit('delete-todo', id)
    },
    setPromptTrue(id) {
      this.nestedPrompt = !this.nestedPrompt
      //console.log(id)
      //this.$emit('add-to-parent', id)
    },
    editItem(x) {
      this.editFlag = 'true'
      console.log(x.id)
      //console.log(this.editFlag)
      //console.log(x)
      //this.$emit('add-done-butt', x)
      //document.getElementById('doneEdit').style.display = 'flex'
      console.log(document.getElementsByName('textone'))
      console.log(this.list)
      var index = 0
      var stop = false
      console.log('hasChildren: ', x.hasChildren)
      for (var i = 0; i < this.list.length; i++) {
        if (x.id != this.list[i].id) {
          index++
        } else {
          break
        }
        if (this.list[i].hasChildren) {
          console.log('childrenlength: ', this.list[i].children.length)
          for (var j = 0; j < this.list[i].children.length; j++) {
            if (x.id != this.list[i].children[j].id) {
              index++
            } else {
              stop = true
              break
            }
          }
        }
        if (stop) {
          break
        }
      }
      console.log('index:', index)
      document.getElementsByName('textone')[index].contentEditable = 'true'
      document.getElementsByName('texttwo')[index].contentEditable = 'true'
      //x.title = 'Hello'
      //document.getElementById('textone').contentEditable = 'true'
      //document.getElementById('texttwo').contentEditable = 'true'
      //first_para.contenteditable = 'true'
      //second_para.contenteditable = 'true'
    },
    editItemDone(x) {
      console.log('wtf')
      this.editFlag = !this.editFlag
      //console.log(this.editFlag)
      var index = 0
      var stop = false
      for (var i = 0; i < this.list.length; i++) {
        if (x.id != this.list[i].id) {
          index++
        } else {
          break
        }
        if (x.hasChildren) {
          for (var j = 0; j < this.list[i].children.length; j++) {
            if (x.id != this.list[i].children[j].id) {
              index++
            } else {
              stop = true
              break
            }
          }
        }
        if (stop) {
          break
        }
      }
      console.log(index)
      document.getElementsByName('textone')[index].contentEditable = 'false'
      document.getElementsByName('texttwo')[index].contentEditable = 'false'
      //first_para.contenteditable = 'true'
      //second_para.contenteditable = 'true'
    },
    passAlongInfo(x) {
      //console.log('this is second step')
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

<style scoped>
.item {
  margin-top: 1px;
  background: #f4f4f4;
  padding: 10px;
  font-size: 20px;
  border: 1px black solid;
  word-wrap: break-word;
}
.completed {
  text-decoration: line-through;
}

.completed p {
  opacity: 50%;
}

.date {
  text-align: right;
  padding-right: 110px;
}
.add {
  background: #21e758;
  color: #fff;
  border: none;
  padding: 5px 10px;
  border-radius: 25%;
  cursor: pointer;
  float: right;
  margin: 3px;
}
.delete {
  background: #ff0000;
  color: #fff;
  border: none;
  padding: 5px 10px;
  border-radius: 25%;
  cursor: pointer;
  float: right;
  margin: 3px;
}
.edit {
  background: #474e50;
  color: #fff;
  border: none;
  padding: 5px 10px;
  border-radius: 25%;
  cursor: pointer;
  float: right;
  margin: 3px;
}

.childTodo {
  margin-left: 150px;
}
#editbut {
  width: 10%;
  margin-bottom: 3px;
}

#nested_prompter {
  display: flex;
  justify-content: right;
}

input[type='checkbox'] {
  cursor: pointer;
  margin-right: 5px;
}

#doneBut {
  display: flex;
  justify-content: right;
}
</style>

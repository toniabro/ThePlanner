<template>
  <div>
    <button id="doneEdit" @click="buttonClick">
      Done Editing
    </button>
  </div>
</template>

<script>
export default {
  methods: {
    buttonClick() {
      this.$emit('destroy')
    }
  }
}
</script>

<style scoped>
#doneEdit {
  display: flex;
  background: #555555;
  color: #fff;
  border: none;
  padding: 10px 40px;
  cursor: pointer;
  float: right;
  margin: 3px;
  font-size: 17px;
}
</style>

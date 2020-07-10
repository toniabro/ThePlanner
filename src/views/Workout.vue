<template>
  <div class="workout">
    <Header title="Workout Tracker"></Header>
  </div>
</template>

<script>
import Header from '../components/Header.vue'
export default {
  name: 'workout',
  components: {
    Header
  },
  data() {
    return {
      workout: [
        {
        }
      ]
    }
  }
}
</script>

<style></style>

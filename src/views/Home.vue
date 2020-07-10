<template>
  <div class="home">
    <Header title="Home"></Header>
    <h1 id="welcome">Welcome to my website!</h1>
    <div class="info">
      <h2>Email: tonylicong@gmail.com</h2>
      <h2>Github: https://github.com/toniabro</h2>
      <h2>LinkedIn: https://www.linkedin.com/in/tony-li-809471184/</h2>
    </div>
    <div>
      <p>
        This website is meant to eventually replace the notebook in which I keep
        my Todo list, workout notes, and video game notes. 
      </p>
      <img id="WIP" src="../assets/WorkinProgress.jpg" alt="Italian Trulli">
    </div>
  </div>
</template>

<script>
import Header from '../components/Header.vue'
export default {
  name: 'Home',
  components: {
    Header
  }
}
</script>

<style scoped>
#welcome {
  text-align: center;
  font-size: 50px;
  font-family: 'Times New Roman', Times, serif;
}

h2 {
  background-color: #fffdaf;
}

#WIP {
  width: 300px;
}

p {
  margin-top: 20px;
  font-size: 20px;
}
</style>

<template>
  <div id="app">
        <UploadImages :max="1"  @changed="handleImage"/>
        <div class="canvas-container">
          <canvas id="c"></canvas>
        </div>
  </div>
</template>

<script>
import UploadImages from 'vue-upload-drop-images'

export default {
  name: 'App',
  components: {
    UploadImages
  },
  data () {
    return {
      image: ''
    }
  },
  methods: {
    handleImage (files) {
      if (files[0]) {
        const file = files[0]
        const fr = new FileReader()
        fr.onload = (event) => {
          this.image = event.target.result
          console.log(this.image)
        } // onload fires after reading is complete
        fr.readAsDataURL(file)
      }
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.canvas-container{
  display: flex;
  width: 100%;
  align-items: center;
  justify-content: center;
}

</style>

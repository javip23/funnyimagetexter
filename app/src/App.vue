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
  methods: {
    handleImage (files) {
      if (files[0]) {
        const file = files[0]
        const fr = new FileReader()
        fr.onload = (event) => {
          this.setBase64ToCanvas(event.target.result)
        }
        fr.readAsDataURL(file)
      }
    },
    setBase64ToCanvas (base64Image) {
      const canvas = document.getElementById('c')
      const ctx = canvas.getContext('2d')
      ctx.clearRect(0, 0, canvas.width, canvas.height)
      const image = new Image()
      image.onload = () => {
        const canvasWidth = Math.trunc(700 - (100 * image.width / 700))
        const canvasHeight = Math.trunc(700 - (100 * image.height / 700))
        canvas.width = canvasWidth
        canvas.height = canvasWidth
        ctx.drawImage(image, 0, 0, canvasWidth, canvasHeight)
        this.$nextTick(() => {})
      }
      image.src = base64Image
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

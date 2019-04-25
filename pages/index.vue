<template>
  <v-layout>
    <v-flex text-xs-center>
      <v-btn color="danger" @click="$refs.inputUpload.click()">Add Logo</v-btn>
      <input v-show="false" ref="inputUpload" type="file" @change="convert" />
      <div id="container">
        <img src="/logo1.png" alt="logo" />
      </div>
    </v-flex>
  </v-layout>
</template>
<script>
import watermark from 'watermarkjs'
export default {
  methods: {
    convert() {
      const upload = document.querySelector('input[type=file]').files[0]
      watermark([upload, '/logo.png'])
        .image(watermark.image.lowerRight(0.8))
        .then(img => {
          const node = document.getElementById('container')
          node.removeChild(node.firstChild)
          node.appendChild(img)
        })
    }
  }
}
</script>
<style>
img {
  max-width: 100%;
}
</style>

<template>
  <div class="signature">
    <canvas ref="canvas" class="signature" />
  </div>
</template>

<script>
import SignaturePad from 'signature_pad'

export default {
  components: {},
  data: () => ({
    signaturePad: null
  }),
  mounted() {
    this.signaturePad = new SignaturePad(this.$refs.canvas)
    this.resizeCanvas()
  },
  methods: {
    resizeCanvas() {
      const ratio = Math.max(window.devicePixelRatio || 1, 1)
      this.$refs.canvas.width = this.$refs.canvas.offsetWidth * ratio
      this.$refs.canvas.height = this.$refs.canvas.offsetHeight * ratio
      this.$refs.canvas.getContext('2d').scale(ratio, ratio)
      this.signaturePad.clear() // otherwise isEmpty() might return incorrect value
    }
  }
}
</script>

<style>
.signature {
  width: 100%;
  height: 100%;
  min-height: 500px;
}
</style>

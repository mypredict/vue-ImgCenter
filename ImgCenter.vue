<template lang="pug">
  div.img-center(ref="containerSelf")
    img.center-image(:src="thisImgSrc", @load="imgLoaded", ref="imgSelf")
</template>

<script type="text/javascript">
export default {
  name: 'ImgCenter',
  props: {
    imgSrc: String
  },
  data () {
    return {
      thisImgSrc: this.imgSrc
    }
  },
  computed: {
    imgHeightWidth () {
      return this.$refs.imgSelf.height / this.$refs.imgSelf.width
    }
  },
  methods: {
    imgLoaded () {
      this.$nextTick(() => {
        let thisContainer = this.$refs.containerSelf
        let containerWidth = thisContainer.offsetWidth
        let containerWidthHalf = containerWidth / 2
        let containerHeight = thisContainer.offsetHeight
        let containerHeightHalf = containerHeight / 2
        let containerHeightWidth = containerHeight / containerWidth
        let thisImg = this.$refs.imgSelf
        if (containerHeightWidth >= this.imgHeightWidth) {
          thisImg.height = containerHeight
          let imgWidthHalf = thisImg.width / 2
          let leftMove = imgWidthHalf - containerWidthHalf
          thisImg.style.left = -leftMove + 'px'
        } else {
          thisImg.width = containerWidth
          let imgHeightHalf = thisImg.height / 2
          let upMove = imgHeightHalf - containerHeightHalf
          thisImg.style.top = -upMove + 'px'
        }
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.img-center {
  position: relative;
  width: 100%;
  height: 100%;
  background: red;
  overflow: hidden;
  img.center-image {
    position: absolute;
  }
}
</style>

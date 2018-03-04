# VueImgCenter
vue组件,加载的图片全部都居中-等比例缩放不失真
这是一个基于vue的小组件,主要用于第一次加载时能够将各类大小比例的图片能够不失真的显示在自己所定义的盒子内,实现十分简单
## 首先来看一下源码
```
<template lang="pug">
  div.img-center(ref="containerSelf")
    img.center-image(:src="thisImgSrc", @load="imgLoaded" ref="imgSelf")
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
```
## 使用说明

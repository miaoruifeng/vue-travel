<template>
  <div>
    <router-link tag="div" to="/" class="header-abs" v-show="showAbs">
      <div class="iconfont header-abs-back">&#xe624;</div>
    </router-link>
    <div
      class="header-fixed"
      v-show="!showAbs"
      :style="opacityStyle"
    >
      <router-link to="/">
        <div class="iconfont header-fixed-back">&#xe624;</div>
      </router-link>
      景点详情
    </div>
  </div>
</template>

<script>
export default {
  name: 'DetailHeader',
  data () {
    return {
      showAbs: true,
      opacityStyle: {
        opacity: 0
      }
    }
  },
  methods: {
    handleScroll () {
      const top = document.documentElement.scrollTop
      if (top > 60) {
        let opacity = top / 140
        opacity = opacity > 1 ? 1 : opacity
        this.opacityStyle = { opacity }
        this.showAbs = false
      } else {
        this.showAbs = true
      }
    }
  },
  activated () {
    window.addEventListener('scroll', this.handleScroll)
  },
  deactivated () {
    window.removeEventListener('scroll', this.handleScroll)
  },
  mounted () {
    window.addEventListener('scroll', this.handleScroll)
  }
}
</script>

<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .header-abs
    position absolute
    top .2rem
    left .2rem
    width .72rem
    height .72rem
    line-height .72rem
    border-radius .36rem
    background rgba(0, 0, 0, .6)
    text-align center
    .header-abs-back
      font-size .40rem
      color #fff
  .header-fixed
    z-index 5
    position fixed
    top 0
    left 0
    right 0
    height $headerHeight
    line-height $headerHeight
    background $bgColor
    text-align center
    font-size .32rem
    color #fff
    .header-fixed-back
      position absolute
      top 0
      left 0
      width .72rem
      text-align center
      font-size .36rem
      color #fff
</style>

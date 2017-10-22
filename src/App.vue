<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评价</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>

    <router-view></router-view>
  </div>
</template>

<script>
  import header from './components/header/header.vue'

  export default {
    data() {
      return {
        seller: {}
      }
    },
    components: {
      'v-header': header
    },
    created() {
      this.$ajax.get('/api/seller').then((res) => {
        res = res.data
        // console.log(res)
        if(res.errno === 0) {
          this.seller = res.data
          console.log(this.seller)
        }
      }).catch((err) => {
        console.log('error')
      })
    }
  }
</script>

<style lang="stylus">
  @import "./common/stylus/mixin.styl"

  #app
    .tab
      display: flex
      width: 100%
      height: 40px
      line-height: 40px
      border-1px(rgba(7,17,27,.1))
      .tab-item
        flex: 1
        text-align: center
        & > a
          display: block
          font-size: 14px
          color: rgb(77, 85, 93)
          &.active
            color: #f01414
</style>

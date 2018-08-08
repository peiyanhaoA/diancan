<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab border-1px">
        <div class="tab-item">
            <router-link :to="{path: '/goods'}">商品</router-link>
        </div>
        <div class="tab-item">
            <router-link :to="{path: '/ratings'}">评价</router-link>
        </div>
        <div class="tab-item">
            <router-link :to="{path: '/seller'}">商家</router-link>
        </div>
    </div>
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script>
import VHeader from 'components/header/header'
const ERR_OK = 0
export default {
    data(){
        return {
            seller: {}
        }
    },
    created(){
        this.$http.get('/seller').then(res => {
            if(res.data.errno === ERR_OK){
                this.seller = res.data.data
                // console.log(this.seller)
            }
        })
    },
    components: {
        VHeader
    }
}
</script>

<style lang='stylus'>
@import './common/stylus/mixin.styl'
    #app
        .tab
            display flex
            width 100%
            height 40px
            line-height 40px
            border-1px(rgba(7, 17, 27, 0.1))
            .tab-item
                flex 1
                text-align center
                & > a
                    display block
                    font-size 14px
                    color rgb(77, 85, 93)
                    &.router-link-active
                        color rgb(240, 20, 20)
</style>

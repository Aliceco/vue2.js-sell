<template>
 <div class="cartbutton">
   <transition name="move">
   <div @click.stop.prevent="delCart" class="cart-del" v-show="food.count>0">
     <span class="inner icon-remove_circle_outline"></span>
   </div>
   </transition>
   <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
   <div class="cart-add icon-add_circle" @click.stop.prevent="addCart"></div>
 </div>
</template>

<script type="text/ecmascript-6">
  import Vue from 'vue'
  export default {
    props: {
      food: {
        type: Object
      }
    },
    created () {
    },
    methods: {
      addCart (event) {
        if (!event._constructed) {
          return
        }
        if (!this.food.count) {
          Vue.set(this.food, 'count', 1)
        } else {
          this.food.count++
        }
        this.$emit('add', event.target)
//        this.$emit('cart.add', event.target)
      },
      delCart (event) {
        if (!event._constructed) {
          return
        }
        if (this.food.count > 0) {
          this.food.count--
        }
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .cartbutton
    font-size: 0
    .cart-del
      display: inline-block
      padding-right: 6px
      transition: all 0.4s linear
      &.move-transition
        opacity: 1
        transform: translate3D(0, 0, 0,)
      .inner
        display: inline-block
        line-height: 24px
        font-size: 24px
        color: rgb(0, 160, 220)
        transition: all 0.4s linear
        transform: rotate(0)
      &.move-enter, &.move-leave-active
        opacity: 0
        transform: translate3D(24px, 0, 0,)
        .inner
          transform: rotate(180deg)
    .cart-count
      display: inline-block
      vertical-align: top
      width: 12px
      padding-right: 6px
      line-height: 24px
      text-align: center
      font-size: 10px
      color: rgb(147, 153, 159)
    .cart-add
      display: inline-block
      line-height: 24px
      font-size: 24px
      color: rgb(0, 160, 220)
</style>

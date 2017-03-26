<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="cart-decrease icon-remove_circle_outline" v-show="food.count > 0" @click="decreaseCart"></div>
    </transition>
    <div class="cart-count" v-show="food.count > 0">{{ food.count }}</div>
    <div class="cart-add icon-add_circle" @click="addCart"></div>
  </div>
</template>

<script type="text/ecmascript-6">
  import Vue from 'vue';

  export default {
    props: {
      food: {
        type: Object
      }
    },
    created() {
//      console.log(this.food);
    },
    methods: {
      addCart(event) {
        if (!event._constructed) {
          return;  // 解决电脑端点击一次变成双次的bug
        }
        console.log('click');
        if (!this.food.count) {
//          this.food.count = 1;
          Vue.set(this.food, 'count', 1);
        } else {
          this.food.count++;
        }
        this.$emit('cartAdd', event.target); // 在1.0中是$dispatch
      },
      decreaseCart() {
        if (!event._constructed) {
          return;
        }
        if (this.food.count) {
          this.food.count--;
        }
      }
    }
  };

</script>

<style lang="stylus" rel="stylesheet/stylus">
  .cartcontrol
    font-size: 0
    > div
      display: inline-block
    .cart-decrease, .cart-add
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0, 160, 220)
      transform: rotate(180deg)
      &.move-enter-active, &.move-leave-active
        transition: all .4s linear
      &.move-enter, &.move-leave-active
        opacity: 0
        transform: translate3D(24px, 0, 0)
    .cart-count
      vertical-align: top
      width: 12px
      padding-top: 6px
      line-height: 24px
      text-align: center
      font-size: 10px
      color: rgb(147, 158, 159)
    .cart-add
      margin: 0
</style>

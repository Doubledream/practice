<template>
  <div>
    <div class="cartcontrol">
      <transition name="move">
        <div class="cart-decrease" v-show="food.count > 0"
        v-on:click="decreaseCart">
          <span class="inner icon-remove_circle_outline"></span>
        </div>
      </transition>
      <div class="cart-count" v-show="food.count > 0">{{food.count}}</div>
      <div class="cart-add icon-add_circle" v-on:click="addCart"></div>
    </div>
  </div>
</template>

<script>
  import Vue from 'vue';

  export default {
    props: {
      food: {
        type: Object
      }
    },
    methods: {
      addCart(event) {
        let eventHub = new Vue();
        if (!event._constructed) {
          return;
        }
        if (!this.food.count) {
          Vue.set(this.food, 'count', 1);
        } else {
          this.food.count ++;
        }
        eventHub.$emit('cart.add', event.target);
      },
      decreaseCart(event) {
        if (!event._constructed) {
          return;
        }
        if (this.food.count) {
          this.food.count --;
        }
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .cartcontrol
    font-size: 0
    .cart-decrease, .cart-add
      display: inline-block
      padding: 6px
      .inner
        display: inline-block
        line-height: 24px
        font-size: 24px
        color: rgb(0, 160, 220)
        transform: translate3D(24px, 0, 0)
        transform: rotate(0)
    .move-enter-active, .move-leave-active
      transition: all 0.4s linear
    .move-enter, .move-leave-active
      transform: translate3D(0, 0, 0)
      opacity: 0
      transform: rotate(180deg)
    .cart-count
      display: inline-block
      vertical-align: top
      width: 12px
      padding-top: 6px
      line-height: 24px
      text-align: center
      font-size: 10px
      color: rgb(147, 153, 159)
    .cart-add
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0, 160, 220)
</style>

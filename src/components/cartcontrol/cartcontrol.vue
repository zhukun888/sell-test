<template>
  <div class="cartcontrol">
    <div
      class="cart-decrease "
      v-show="food.count>0"
      @click.stop="decrease"
      transition="move"
    ><span class="inner icon-remove_circle_outline" ></span>
    </div>
    <div class="cart-count" v-if="food.count>0">{{ food.count }}</div>
    <div class="cart-add icon-add_circle" @click.stop="addCart"></div>
  </div>
</template>

<script>
// import Vue from 'Vue'
// Vue.set(this.food,'count',0)
import Vue from "Vue";
export default {
  props: {
    food: { type: Object },
  },
  created() {
    //   console.log(this.food)
  },
  data() {
    return {};
  },
  computed: {},
  methods: {
    addCart() {
      // console.log(2)
      if (!this.food.count) {
        Vue.set(this.food, "count", 1);
      } else {
        this.food.count++;
      }
      this.$dispatch('cart.add',event.target);
    },
    decrease() {
      this.food.count--;
    },
  },
};
</script>

<style lang="stylus">
.cartcontrol
   font-size 0
   .cart-decrease
      display inline-block
      padding 6px
      
      &.move-transition
        opacity 1
        transform translate3d(0,0,0)
        transition all 0.4s linear
        .inner
          display inline-block 
          line-height 24px
          font-size 24px
          color rgb(0,160,220)
          transition all 0.4s linear 
          transform rotate(0)
      &.move-enter,&.move-leave
        opacity 0
        transform translate3d(24px,0,0)
        .inner
          transform rotate(180deg)
   .cart-count
      display inline-block
      vertical-align top
      font-size 10px
      color rgb(147,153,159)
      width 12px
      padding-top 6px
      line-height 24px
      text-align center
    .cart-add
      display inline-block
      padding 6px
      line-height 24px
      font-size 24px
      color rgb(0,160,220)
</style>

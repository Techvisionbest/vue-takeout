<template>
  <div class="shopcart">
    <div class="content">
      <div class="content-left">
        <div class="logo-wrapper">
          <div class="logo" :class="{'highlight':totalCount>0}">
            <i class="icon-shopping_cart" :class="{'highlight':totalCount>0}"></i>
          </div>
          <div class="num" v-show="totalCount>0">{{totalCount}}</div>
        </div>
        <div class="price">￥{{totalPrice}}</div>
        <div class="desc">另需配送费￥{{deliveryPrice}}元</div>
      </div>
      <div class="content-right">
        <div class="pay" :class="payClass">{{payDesc}}</div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      selectFoods: {
        type: Array,
        default() {
          return [{
            price: 30,
            count: 2
          }]
        }
      },
      deliveryPrice: {
        type: Number,
        default: 0
      },
      minPrice: {
        type: Number,
        default: 0
      }
    },
    computed: {
      payClass() {
        if (this.totalPrice < this.minPrice) {
          return 'not-enough';
        } else {
          return 'enough';
        }
      },
      totalPrice() {
        let total = 0;
        this.selectFoods.forEach((food) => {
          total += food.price * food.count;
        });
        return total;
      },
      totalCount() {
        let count = 0;
        this.selectFoods.forEach((food) => {
          count += food.count;
        });
        return count;
      },
      payDesc() {
        if (this.totalPrice === 0) {
          return `￥${this.minPrice}元起送`;
        } else if (this.totalPrice < this.minPrice) {
          let diff = this.minPrice - totalPrice;
          return `还差￥${diff}元起送}`;
        } else {
          return '去结算';
        }
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .shopcart
    position fixed
    bottom 0px
    left 0px
    z-index 50
    width 100%
    height 48px
    .content
      display flex
      background #141d27
      color: rgba(255, 255, 255, 0.4)
      .content-left
        color #80858a
        flex: 1
        .logo-wrapper
          display inline-block
          vertical-align top
          width 56px
          height 56px
          background #141d27
          box-sizing border-box
          border-radius 50%
          top -10px
          position relative
          margin 0 12px
          padding 6px
          .num
            position absolute
            right 0
            top 5px
            background red
            color #fff
            border-radius 16px
            width 24px
            height 16px
            font-size 10px
            line-height 16px
            text-align center
            font-weight 700
            box-shadow 0px 4px 8px 0 rgba(7, 17, 27, 0.5)
          .logo
            width 100%
            height 100%
            border-radius 50%
            text-align center
            background #2b343c
            &.highlight
              background deepskyblue
              color #fff
            .icon-shopping_cart
              line-height 44px
              font-size 24px
        .price
          padding-right 15px
          box-sizing border-box
          border-right 1px solid rgba(255, 255, 255, 0.2)
          font-size 16px
          font-weight 700
          text-align center
          line-height 48px
          display inline-block
        .desc
          display inline-block
          font-weight 700
          font-size 10px
          margin-left 10px
      .content-right
        flex: 0 0 105px
        .pay
          text-align center
          line-height 48px
          font-size 10px
          font-weight 700
          &.not-enough
            background #2b333b
          &.enough
            background green
            color #fff
</style>

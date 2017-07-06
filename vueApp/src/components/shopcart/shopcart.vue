<template>
    <div class="shopcart">
        <div class="content">
            <div class="content-left">
                <div class="logo-wrapper">
                    <div class="logo" :class="{'highlight':totalCount>0}">
                        <i class="iconfont icon-shopcart"></i>
                    </div>
                    <div class="num" v-show="totalCount>0">{{totalCount}}</div>
                </div>
                <div class="price" :class="{'highlight':totalPrice>0}">
                    ￥{{totalPrice}}
                </div>
                <div class="description" >
                    另需配送费{{seller.deliveryPrice}}
                </div>
            </div>
            <div class="content-right">
                <div class="pay" :class="{'enough':this.totalPrice >= this.seller.minPrice}">
                    {{payDesc}}
                </div>
            </div>
        </div>
    </div>
</template>

<script type='text/ecmascript-6'>
    export default{
        props: {
            selectFoods: {
                type: Array,
                default: function () {
                    return [];
                }
            },
            seller: Object
        },
        computed: {
            totalPrice() {
                let total = 0;
                this.selectFoods.forEach(function (food) {
                    total += food.price * food.count;
                });
                return total;
            },
            totalCount() {
                let count = 0;
                this.selectFoods.forEach(function (food) {
                    count += food.count;
                });
                return count;
            },
            payDesc() {
                if (this.totalPrice === 0) {
                    return '￥' + this.seller.minPrice + '起送';
                } else if (this.totalPrice < this.seller.minPrice) {
                    let diff = this.seller.minPrice - this.totalPrice;
                    return `还差￥${diff}`;
                } else {
                    return '去结算';
                }
            }
        }
    };
</script>

<style type="text/stylus" lang='stylus' rel='stylesheet/stylus'>
    @import "../../common/stylus/mixin"
    .shopcart
        position: fixed
        bottom: 0
        left: 0
        z-index: 100
        width: 100%
        height: 48px
        .content
            display: flex
            background: #141d27
            font-size: 0
            color: rgba(255, 255, 255, 0.4)
            .content-left
                flex: 1
                .logo-wrapper
                    display: inline-block
                    vertical-align: top
                    position: relative
                    top: -10px
                    margin: 0 12px
                    padding: 6px
                    width: 56px
                    height: 56px
                    box-sizing: border-box
                    border-radius: 50%
                    background: #141d27
                    .logo
                        width: 100%
                        height: 100%
                        border-radius: 50%
                        background: #2b343c
                        text-align: center
                        &.highlight
                            background: rgb(0, 160, 220)
                            .icon-shopcart
                                color: #fff
                        .icon-shopcart
                            line-height: 44px
                            font-size: 24px
                            color: #80858a
                    .num
                        position: absolute
                        top: 0
                        right: 0
                        width: 24px
                        height: 16px
                        line-height: 16px
                        text-align: center
                        border-radius: 16px
                        font-size: 9px
                        font-weight: 700
                        color: #fff
                        background: rgb(240, 20, 20)
                        box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.4)
                .price
                    display: inline-block
                    vertical-align: top
                    line-height: 24px
                    margin-top: 12px
                    padding-right: 12px
                    border-1px(rgba(255, 255, 255, 0.1), right)
                    font-size: 16px
                    font-weight: 700
                    &.highlight
                        color: #fff
                .description
                    display: inline-block
                    vertical-align: top
                    margin: 12px 0 0 12px
                    line-height: 24px
                    font-size: 10px
            .content-right
                flex: 0 0 105px
                width: 105px
                .pay
                    height: 48px
                    line-height: 48px
                    text-align: center
                    font-size: 12px
                    font-weight: 700
                    background: #2b333b
                    &.enough
                        background :#00b43c
                        color:#fff
</style>

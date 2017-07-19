<template>
    <div class="shopcart">
        <div class="content">
            <div class="content-left">
                <div class="logo-wrapper">
                    <div class="logo" :class="{'highlight':totalCount>0}" ref="logo">
                        <i class="iconfont icon-shopcart"></i>
                    </div>
                    <div class="num" v-show="totalCount>0">{{totalCount}}</div>
                </div>
                <div class="price" :class="{'highlight':totalPrice>0}">
                    ￥{{totalPrice}}
                </div>
                <div class="description">
                    另需配送费{{seller.deliveryPrice}}
                </div>
            </div>
            <div class="content-right">
                <div class="pay" :class="{'enough':this.totalPrice >= this.seller.minPrice}">
                    {{payDesc}}
                </div>
            </div>
        </div>
        <div class="ball-container">
            <div v-for="ball in balls">
                <transition name="drop" @before-enter="beforeDrop" @enter="dropping" @after-enter="afterDrop">
                    <div class="ball" v-show="ball.show">
                        <div class="ball-inner ball-hook"></div>
                    </div>
                </transition>
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
        data() {
            return {
                balls: [{
                    show: false
                }, {
                    show: false
                }, {
                    show: false
                }, {
                    show: false
                }, {
                    show: false
                }],
                dropBalls: []
            };
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
        },
        methods: {
            drop(element) {
                for (let i = 0; i < this.balls.length; i++) {
                    let item = this.balls[i];
                    if (!item.show) {
                        item.show = true;
                        item.el = element;
                        this.dropBalls.push(item);
                        return;
                    }
                }
            },
            beforeDrop(el) {
                let count = this.balls.length;
                while (count--) {
                    let ball = this.balls[count];
                    if (ball.show) {
                        let rect = ball.el.getBoundingClientRect();
                        let x = rect.left - 32;
                        let y = -(window.innerHeight - rect.top - 22);
                        el.style.display = '';
                        el.style.webkitTransform = `translate3d(0,${y}px,0)`;
                        el.style.transform = `translate3d(0,${y}px,0)`;
                        let inner = el.getElementsByClassName('ball-hook')[0];
                        inner.style.webkitTransform = `translate3d(${x}px,0,0)`;
                        inner.style.transform = `translate3d(${x}px,0,0)`;
                    }
                }
            },
            dropping(el, done) {
                /* eslint-disable no-unused-vars */
                let rf = el.offsetHeight;
                this.$nextTick(() => {
                    el.style.webkitTransform = 'translate3d(0,0,0)';
                    el.style.transform = 'translate3d(0,0,0)';
                    let inner = el.getElementsByClassName('ball-hook')[0];
                    inner.style.webkitTransform = 'translate3d(0,0,0)';
                    inner.style.transform = 'translate3d(0,0,0)';
                    el.addEventListener('transitionend', done);
                    setTimeout(() => {
                        this.$refs.logo.style.transform = 'scale(0.5)';
                    }, 0.5);
                });
            },
            afterDrop(el) {
                let ball = this.dropBalls.shift();
                if (ball) {
                    ball.show = false;
                    el.style.display = 'none';
                }
                this.$refs.logo.style.transform = 'scale(1)';
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
                        transition: all 0.5s
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
                        background: #00b43c
                        color: #fff
        .ball-container
            .ball
                position: fixed
                bottom: 22px
                left: 32px
                z-index: 200
                transition: all 0.5s cubic-bezier(0.49, -0.29, 0.75, 0.41)
                .ball-inner
                    width: 16px
                    height: 16px
                    border-radius: 50%
                    background: rgb(0, 160, 220)
                    transition: all 0.5s linear
</style>

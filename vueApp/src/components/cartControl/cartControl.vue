<template>
    <div class="cart-control">
        <div class="decrease" v-show="food.count>0">
            <i class="iconfont icon-decrease"></i>
        </div>
        <div class="count" v-show="food.count>0">{{food.count}}</div>
        <div class="add" @click="addCart">
            <i class="iconfont icon-add"></i>
        </div>
    </div>
</template>

<script type='text/ecmascript-6'>
    import Vue from 'vue';
    export default{
        props: {
            food: Object
        },
        methods: {
            addCart() {
                if (!event._constructed) {
                    return;
                }
                if (!this.food.count) {
                    Vue.set(this.food, 'count', 1);
                } else {
                    this.food.count++;
                }
            }
        }
    };
</script>

<style type="text/stylus" lang='stylus' rel='stylesheet/stylus'>
    .cart-control
        font-size: 0
        .decrease, .add
            display: inline-block
            padding: 6px
            color: rgb(0, 160, 220)
            .iconfont
                line-height: 24px
                font-size: 24px
        .count
            display: inline-block
            vertical-align: top
            width: 12px
            padding-top: 6px
            line-height: 24px
            text-align: center
            font-size: 12px
            color: rgb(147, 153, 159)
</style>


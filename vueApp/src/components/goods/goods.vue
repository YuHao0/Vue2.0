<template>
    <div class="goods">
        <div class="menu-wrapper">
            <ul class="menu-list">
                <li v-for="item in goods" class="menu-item">
                    <span class="text">
                        <span v-show="item.type>0" class="type-icon" v-bind:class="supportIcon[item.type]"></span>{{item.name}}
                    </span>
                </li>
            </ul>
        </div>
        <div class="foods-wrapper"></div>
    </div>
</template>

<script type='text/ecmascript-6'>
    export default{
        props: {
            seller: Object
        },
        data() {
            return {
                goods: [],
                supportIcon: ['decrease', 'discount', 'special', 'invoice', 'guarantee']
            };
        },
        created() {
            this.$http.get('/api/goods').then((result) => {
                result = result.body;
                if (result.errorCode === 0) {
                    this.goods = result.data;
                }
            });
        }
    };
</script>

<style type="text/stylus" lang='stylus' rel='stylesheet/stylus'>
    @import "../../common/stylus/mixin"
    .goods
        display: flex
        position: absolute
        top: 174px
        width: 100%
        bottom: 46px
        overflow: hidden
        .menu-wrapper
            flex: 0 0 80px
            width: 80px
            background: #f3f5f7
            .menu-list
                overflow-y: auto;
                height: 100%;
            .menu-item
                display: table
                height: 54px
                width: 56px
                padding :0 12px
                line-height: 14px
                font-size: 14px
                .type-icon
                    display: inline-block
                    vertical-align: top
                    width: 12px
                    height: 12px
                    margin-right: 2px
                    background-size: 12px 12px
                    background-repeat: no-repeat
                    &.decrease
                        bg-image('decrease_3')
                    &.discount
                        bg-image('discount_3')
                    &.guarantee
                        bg-image('guarantee_3')
                    &.invoice
                        bg-image('invoice_3')
                    &.special
                        bg-image('special_3')
                .text
                    display: table-cell
                    width: 56px
                    vertical-align: middle
                    font-size: 12px
                    border-1px(rgba(7, 17, 27, 0.1))
        .foods-wrapper
            flex: 1
</style>

<template>
    <div class="shopcart">
        <div class="content">
            <div class="content-left">
                <div class="logo-wrapper">
                    <div class="logo">
                        <i class="iconfont icon-shopcart"></i>
                    </div>
                </div>
                <div class="price">
                    ￥0
                </div>
                <div class="description">
                    另需配送费￥{{seller.deliveryPrice}}元
                </div>
            </div>
            <div class="content-right">

            </div>
        </div>
    </div>
</template>

<script type='text/ecmascript-6'>
    export default{
        props: {
            seller: Object
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
                        .icon-shopcart
                            line-height: 44px
                            font-size: 24px
                            color: #80858a
                .price
                    display: inline-block
                    vertical-align: top
                    line-height: 24px
                    margin-top: 12px
                    padding-right: 12px
                    border-1px(rgba(255, 255, 255, 0.1), right)
                    font-size: 16px
                    font-weight: 700
                    color: rgba(255, 255, 255, 0.4)
                .description
                    display: inline-block
                    vertical-align: top
                    margin: 12px 0 0 12px
                    line-height: 24px
                    color: rgba(255, 255, 255, 0.4)
                    font-size: 10px
            .content-right
                flex: 0 0 105px
                width: 105px

</style>


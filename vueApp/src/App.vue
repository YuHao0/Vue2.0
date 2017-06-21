<template>
    <div id="app">
        <v-header :seller="seller"></v-header>
        <div class="tab border-1px">
            <router-link class="tab-item" to="/goods">商品</router-link>
            <router-link class="tab-item" to="/ratings">评论</router-link>
            <router-link class="tab-item" to="/seller">商家</router-link>
        </div>
        <router-view></router-view>
    </div>
</template>

<script type='text/ecmascript-6'>
    import header from 'components/header/header.vue';
    const ERR_OK = 0;
    export default {
        data() {
            return {
                seller: {
                    loading: false
                }
            };
        },
        created() {
            this.$http.get('/api/seller').then(function (result) {
                result = result.body;
                if (result.errorCode === ERR_OK) {
                    this.seller = result.data;
                    this.seller.loading = true;
                }
            });
        },
        components: {
            'v-header': header
        }
    };
</script>

<style type="text/stylus" lang="stylus" rel="stylesheet/stylus">
    @import "./common/stylus/mixin"

    .tab
        display: flex
        width: 100%
        height: 40px
        line-height: 40px
        border-1px(rgba(7, 17, 27, 0.1))
        .tab-item
            flex: 1
            text-align: center
            display: block
            font-size: 14px
            color: rgb(77, 85, 93)
        .active
            color: rgb(240, 20, 20)
</style>

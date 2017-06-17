<template>
    <div id="app">
        <v-header></v-header>
        <div class="tab">
            <router-link class="tab-item" to="/goods">商品</router-link>
            <router-link class="tab-item" to="/ratings">评论</router-link>
            <router-link class="tab-item" to="/seller">商家</router-link>
        </div>
        <router-view></router-view>
    </div>
</template>

<script>
    import header from './components/header/header.vue';

    export default {
        components: {
            'v-header': header
        }
    };
</script>

<style rel="stylesheet/stylus" lang="stylus">
    #app
        .tab
            display:flex
            width:100%
            height:40px
            line-height:40px
            justify-content: space-around
            .tab-item
                display: inline-block
</style>

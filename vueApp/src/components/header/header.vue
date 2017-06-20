<template>
    <div class="header">
        <div class="content-wrapper">
            <div class="avatar">
                <img  width="64" height="64" :src="seller.avatar" alt=""/>
            </div>
            <div class="content">
                <div class="title">
                    <span class="brand"></span>
                    <span class="name">{{seller.name}}</span>
                </div>
                <div class="description">
                    {{seller.description}}/{{seller.description}}分钟送达
                </div>
            </div>
        </div>
        <div class="bulletin"></div>
    </div>
</template>

<script type='text/ecmascript-6'>
    export default{
        props: {
            seller: {
                type: {}
            }
        }
    };
</script>

<style type="text/stylus" rel="stylesheet/stylus" lang="stylus">

</style>

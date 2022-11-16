<template>
    <div class="logo-cmp">
        <span class="logo-cmp-ru">RU.</span>
        <span class="logo-cmp-s">S</span>
        <span class="logo-cmp-mart">MART</span>
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>
@import '/src/assets/styles/custom.scss';

.logo-cmp {
    height: 60px;
    width: auto;
    margin-left: 10px;
    @include flexRow( flex-start, center ); 

    &-ru {
        font-size: 28px;
        font-weight: normal;
        font-family:sans-serif;
        color: $main-light;
    }

    &-s {
        font-size: 28px;
        font-weight: normal;
        font-family:sans-serif;
        color: $warning-color;
    }

    &-mart {
        font-size: 28px;
        font-weight: normal;
        font-family:sans-serif;
        color: $main-light;
    }
}
</style>
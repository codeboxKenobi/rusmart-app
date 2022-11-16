<template>
    <button class="button-cmp" type="button" @click="$emit( 'click-handler' )">
        {{ name }}
    </button>
</template>

<script>
    export default {
        props: {
            name: { type: String, default: 'BTN'}
        }
    }
</script>

<style lang="scss" scoped>
@import '/src/assets/styles/custom.scss'; 

.button-cmp {
    height: 34px;
    width: auto;
    padding: 0px 10px 0px 10px;
    margin: 0px 15px 0px 10px;
    outline: none;
    border: $main-border-dark1;
    border-radius: 4px; 

    &:hover {
        border: $main-border-red1;
        background-color: $main-dark;
        color: $main-light;
    }
}
</style>
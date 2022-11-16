<template>
    <span class="text-field">{{ fieldData }}</span>
</template>

<script>
    export default {
        props: {
            fieldData: { type: String, default: 'Поле'}
        }
    }
</script>

<style lang="scss" scoped>
@import '/src/assets/styles/custom.scss'; 

.text-field {
    @include flexRow( flex-start, center );
    opacity: 0.7;
    min-height: 32px;
    height: 32px;
    min-width: 95%;
    padding: 0px 10px 0px 10px;
    border: $main-border-dark1;
    border-radius: 4px;
    outline: none;
    background-color: #fff;
    font-size: 16px;
    font-weight: normal;
    font-family:sans-serif;
    color: $main-dark;

    &:hover {
        border: $main-border-red1;
        opacity: 1;
    }

    &:focus {
        border: $main-border-red1;
        opacity: 1;
    };
}
</style>
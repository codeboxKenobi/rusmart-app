<template>
    <textarea class="text-area" name="" id=""></textarea>
</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>
@import '/src/assets/styles/custom.scss'; 

.text-area {
    max-height: 154px;
    height: 154px;
    max-width: 95%;
    width: 95%;
    margin-top: 20px;
    resize: none;
    padding: 10px;
    outline: none;
    border: $main-border-dark1;
    border-radius: 4px;

    &:hover {
        border: $main-border-red1;
    }

    &:focus {
        border: $main-border-red1;
    }
}
</style>
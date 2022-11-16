<template>
    <input class="input" 
        v-model="value"
        :type="type" 
        name="" 
        id=""
        :placeholder="placeholder"
        @change="$emit( 'emit-value', value )">
</template>

<script>

    export default {
       props: {
            type: { type: String, default: 'input' },
            placeholder: { type: String, default: 'placeholder'}
       },

       data() {
            return {
                value: ''
            }
       }
    }

</script>

<style lang="scss" scoped>
@import '/src/assets/styles/custom.scss'; 

.input {
    height: 32px;
    width: 95%;
    padding: 0px 10px 0px 10px;
    border: $main-border-dark1;
    border-radius: 4px;
    outline: none;
    background-color: #fff;

    &:hover {
        border: $main-border-red1;
    }

    &:focus {
        border: $main-border-red1;
    }
}
</style>
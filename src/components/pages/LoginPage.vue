<template>
    <div class="login-page">
        <logo-cmp />
        <login-form @to-reg="toReg" @resp-ok="$emit( 'resp-ok')" @login-user="loginUser" v-if="!registration" />
        <registration-form v-if="registration" @cancel-reg="cancelReg" />
    </div>
</template>

<script>
import LogoCmp from '../UI/LogoCmp.vue'
import LoginForm from '../form/LoginForm.vue'
import RegistrationForm from '../form/RegistrationForm.vue'

    export default {
        data() {
            return {
                registration: false
            }
        },

        methods: {
            toReg() {
                this.registration = true
            },

            cancelReg() {
                this.registration = false
            },

            loginUser() {
                this.$emit( 'login-user' )
            }
        },

        components: {
            LogoCmp,
            LoginForm,
            RegistrationForm
        }
    }
</script>

<style lang="scss" scoped>
@import '/src/assets/styles/custom.scss';    

.login-page {
    @include flexCol( center, center );
    height: 100vh;
    width: 100vw;
    background-color: $main-dark;
}


</style>
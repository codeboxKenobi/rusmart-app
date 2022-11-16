<template>
    <form class="form" action=""> 
            <div class="form-name">
                Вход
            </div>
            <div class="form-input-section">
                <input-cmp placeholder="Почта"
                    @emit-value="emitEmail" />
                <span class="warning-section">
                    {{ queryMessage }}
                </span>
                <input-cmp type="password" placeholder="Пароль" 
                    @emit-value="emitPassword" />
                <span class="warning-section">
                    {{ queryMessage }}    
                </span>
            </div>
            <div class="form-button-section">
                <button-cmp name="Войти"
                    @click-handler="login" />
                <button-cmp @click-handler="$emit( 'to-reg' )" name="Регистрация" />
            </div>
        </form>
</template>

<script>
import InputCmp from '../UI/InputCmp.vue';
import ButtonCmp from '../UI/ButtonCmp.vue';

export default {
        data() {
            return {
                queryMessage: '',

                inputData: {
                    email: '',
                    password: ''
                },

                baseReg: 'http://localhost:7000/api/registration',
                baseUrl: 'http://localhost:7000/api/user',
                baseLogin: 'http://localhost:7000/api/login',
            }
        },

        components: {
            InputCmp,
            ButtonCmp
        },

        mounted() {
            this.getUsers()
            this.messageOff( 3000 );
        },

        methods: {
            messageOff( time ) {
                if ( !time ) {
                    setTimeout( () => {
                        this.queryMessage = '';
                    }, 5000 );
                } else {
                    setTimeout( () => {
                        this.queryMessage = '';
                    }, time );
                }
            },

            emitEmail( data ) {
                console.log( 'Email :', data );
                this.inputData.email = data
            },

            emitPassword( data ) {
                console.log( 'Password :', data );
                this.inputData.password = data
            },

            async login() {

                console.log( this.inputData );

                if ( this.inputData.email !== '' && this.inputData.password !== '' ) {
                    try {
                        const response = await fetch( this.baseLogin, {
                            method: 'POST',
                            mode: 'cors', 
                            cache: 'no-cache',
                            credentials: 'same-origin',
                        headers: {
                            'Content-Type': 'application/json'
                        },

                        body: JSON.stringify( this.inputData ) 
                });
                        const respData = await response.json();
                        localStorage.setItem( 'ssntkn', respData.accessToken );
                        localStorage.setItem( 'userEmail', respData.user.email );
                        this.queryMessage = respData.message;
                        this.getUsers(respData.userData)

                        if ( response ) {
                            console.log( 'resp ok' );
                            this.$emit( 'resp-ok', true )
                        }
  
                    } catch ( error ) {
                        console.log( error );
                        this.notValid = true
                    }
                } else {
                    this.queryMessage = 'Некорректный ввод';
                }

                this.messageOff( 3000 );
            },

            async getUsers(dta) {
                try {

                    const usrKey = localStorage.getItem( 'ssntkn' )
                    const userData = await fetch( this.baseUrl, {
                        method: 'GET',
                        headers: {
                            Authorization: `Bearer ${ usrKey }`,
                        },

                        body: JSON.stringify( dta )
                    } )

                    const data = await userData.json();

                    if ( data.message === 'Вы не авторизованы' ) {
                        this.$emit( 'to-auth-page' )
                    } else {
                        this.$emit( 'login-user' )
                    }

                    

                    console.log(data);
                    this.queryMessage = data.message
                } catch (error) {
                    console.log( error );
                }

                this.messageOff( 3000 );
            }
        
        }
    }

</script>

<style lang="scss" scoped>
@import '/src/assets/styles/custom.scss'; 

.warning-section {
    @include flexRow( flex-start, center );
    height: 20px;
    width: 100%;
    font-size:10px;
    color: $warning-color;
}
.form {
    @include flexCol( flex-start, center );
    height: 295px;
    width: 300px;
    border-radius: 4px;
    background-color: $main-light;

    &-name {
        @include flexRow( flex-start, center );
        margin-top: 20px;
        margin-bottom: 20px;
        height: 30px;
        width: 90%;
        font-size: 18px;
        font-weight: normal;
        font-family: sans-serif;
        color: $main-dark;
    }

    &-input-section {
        width: 82%;
        margin-bottom: 20px;
        @include flexCol( space-between, center );
    }

    &-button-section {
        @include flexCol( space-between, center );
        height: 26%;
    }
}
</style>
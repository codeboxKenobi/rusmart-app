<template>
    <form class="form" action=""> 
            <div class="form-name">
                Регистрация
            </div>
            <div class="form-input-section">
                <input-cmp placeholder="Почта"
                    @emit-value="emitEmail" />
                <span class="warning-section">
                    {{ queryMessage }}
                </span>
                <input-cmp placeholder="Пароль"
                    @emit-value="emitPassword" />
                <span class="warning-section">
                    {{ queryMessage }}
                </span>
                <input-cmp placeholder="Повторите пароль"
                    @emit-value="emitPasswordConfirm" />
                <span class="warning-section">
                    {{ queryMessage }}
                </span>
            </div>
            <div class="form-button-section">
                <button-cmp name="Зарегистрироваться" @click-handler="regUser" />
                <button-cmp name="Отмена" @click-handler="$emit( 'cancel-reg' )" />
            </div>
        </form>
</template>

<script>
import InputCmp from '../UI/InputCmp.vue';
import ButtonCmp from '../UI/ButtonCmp.vue';

export default {
        data() {
            return {
                baseReg: 'http://localhost:7000/api/registration',
                queryMessage: '* Все поля должны быть заполнены',

                inputData: {
                    email: '',
                    password: '',
                    passwordConfirm: ''
                },
            }
        },

        methods: {
            emitEmail( data ) {
                console.log( 'Email :', data );
                this.inputData.email = data
            },

            emitPassword( data ) {
                console.log( 'Password :', data );
                this.inputData.password = data
            },

            emitPasswordConfirm( data ) {
                console.log( 'Password Confirm :', data );

                if ( this.inputData.password === data ) {
                    this.inputData.passwordConfirm = data
                }
               
            },

            async regUser() {
                console.log( this.inputData );

                if ( this.inputData.email !== '' 
                    && this.inputData.password !== '' 
                    && this.inputData.passwordConfirm !== '' ) {

                    try {
                        const response = await fetch( this.baseReg, {
                            method: 'POST',
                            mode: 'cors',
                            cache: 'no-cache',
                            credentials: 'same-origin', 

                        headers: {
                            'Content-Type': 'application/json'
                        },

                        body: JSON.stringify( this.inputData )
                        
                } );

                        const respData = await response.json();
                        console.log(respData);
         
                        this.queryMessage = respData.message;

                    } catch ( error ) {
                        console.log( error );
                        this.notValid = true
                    }
                } else {
                    this.queryMessage = 'Некорректный ввод';
                }

                this.messageOff( 3000 );
            }
        },

        components: {
            InputCmp,
            ButtonCmp
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
    height: 350px;
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
        height: 22%;
    }
}
</style>
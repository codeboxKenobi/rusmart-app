<template>
    <form class="form" action=""> 
            <div class="form-name">
                Регистрация
            </div>
            <div class="form-input-section">
                <input-cmp placeholder="Почта" />
                <span class="warning-section">
                    {{ warningMessage }}
                </span>
                <input-cmp placeholder="Пароль" />
                <span class="warning-section">
                    {{ warningMessage }}
                </span>
                <input-cmp placeholder="Повторите пароль" />
                <span class="warning-section">
                    {{ warningMessage }}
                </span>
            </div>
            <div class="form-button-section">
                <button-cmp name="Зарегистрироваться" />
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
                warningMessage: '* Все поля должны быть заполнены'
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
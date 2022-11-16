<template>
    <div class="add-service">
        <div class="add-service-form">
            <div class="add-service-form-header">
                <span class="add-service-form-header-text">
                    Создание услуги
                </span>
                <button-cmp name="Закрыть"
                    @click-handler="$emit( 'close-add-modal' )" />
            </div>
            <div class="add-service-form-section">
                <div class="add-service-form-section-input">
                    <input-cmp placeholder="Название услуги" /> 
                </div>
                <div class="add-service-form-section-input">
                    <input-cmp placeholder="Расходы на услугу" />
                </div>
                <div class="add-service-form-section-input">
                    <input-cmp placeholder="Стоимость услуги" />
                </div>
                <div class="add-service-form-section-button">
                    <button-cmp name="Дoбавить услугу" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import ButtonCmp from '../UI/ButtonCmp.vue'
import InputCmp from '../UI/InputCmp.vue'
    export default {
  components: { ButtonCmp, InputCmp },
        
    }
</script>

<style lang="scss" scoped>
@import '/src/assets/styles/custom.scss'; 

.add-service {
    @include flexRow( center, center );
    position: absolute;
    top: 0px;
    left: 0px;
    z-index: 10;
    height: 100%;
    width: 100%;
    background-color: $main-backdrop;
    

    &-form {
        @include flexCol( flex-start, center );
        height: 50%;
        width: 50%;
        background-color: $main-light;
        border: $main-border-dark1;

        &-header {
            @include flexRow( space-between, center );
            height: 50px;
            width: 100%;
            border-bottom: $main-border-dark1;

            &-text {
                @include flexRow( center, center );
                height: 100%;
                width: auto;
                padding: 10px;
                font-size: 16px;
                font-weight: normal;
                font-family:sans-serif;
                color: $main-dark;
            }
        }

        &-section {
            @include flexCol( flex-start, center );
            height: calc( 100% - 40px );
            width: 100%;
            // background-color: rgb(202, 122, 122);

            &-input {
                @include flexRow( center, center );
                margin-top: 10px;
                height: 20%;
                width: 97%;
            }

            &-button {
                @include flexRow( flex-end, center );
                height: 20%;
                margin-right: 10px;
                width: 100%;
            }
        }
    }
}
</style>
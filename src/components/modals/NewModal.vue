<template>
    <div class="new-modal">
        <div class="new-modal-form">
            <div class="new-modal-form-header">
                <div class="new-modal-form-header-order">Новый заказ</div>
                <div class="new-modal-form-header-closed">
                    <button-cmp name="Закрыть"
                        @click-handler="$emit( 'close-new-modal' )" />
                </div>
            </div>
            <div class="new-modal-form-section">
                <div class="new-modal-form-section-left">
                    <div class="new-modal-form-section-left-inputs-section">
                        

                        <div class="new-modal-form-section-left-inputs-section-bottom">
                            <span class="field-description">Клиент :</span>
                            <input-cmp class="mt-10" placeholder="Имя клиента *" />
                            <input-cmp class="mt-10" placeholder="Номер телефона *" />
                        </div>
                        
                        
                        <div class="new-modal-form-section-left-inputs-section-bottom">
                            <span class="field-description">Устройство :</span>
                            <input-cmp class="mt-10" placeholder="Причина обращения" />
                            <input-cmp class="mt-10" placeholder="Тип устройства" />
                            <input-cmp class="mt-10" placeholder="Производитель" />
                            <input-cmp class="mt-10" placeholder="Модель " />

                        </div>

                        <div class="new-modal-form-section-left-inputs-section-bottom">
                            <span class="field-description">Условные параметры :</span>
                            <input-cmp class="mt-10" placeholder="Примерная стоимость услуги в рублях" />
                            <input-cmp class="mt-10" placeholder="Примерная дата выдачи" />
                        </div>
                    </div>

                </div>

                <div class="new-modal-form-section-right">
                    <div class="new-modal-form-section-right-inputs-section">
                        

                        <div class="new-modal-form-section-right-inputs-section-bottom">
                            <span class="field-description">Предоплата по заказу :</span>
                            <input-cmp class="mt-10" placeholder="Сумма предоплаты в рублях" />
                            <input-cmp class="mt-10" placeholder="Метод предоплаты ( карта / наличные / перевод )" />
                        </div>
                        
                        
                        <div class="new-modal-form-section-right-inputs-section-bottom">
                            <span class="field-description">Опрос :</span>
                            <input-cmp class="mt-10" placeholder="Откуда узнали о нас ?" />
                        </div>

                        <div class="new-modal-form-section-right-inputs-section-bottom col-y    ">
                            <span class="field-description">Комментарий :</span>
                            <text-area-cmp />
                        </div>

                        <div class="confirm-section">
                            <button-cmp name="Создать заказ" 
                                @click-handler="$emit( 'close-new-modal' )" />
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import ButtonCmp from '../UI/ButtonCmp.vue';
import InputCmp from '../UI/InputCmp.vue';
import TextAreaCmp from '../UI/TextAreaCmp.vue';

    export default {
        components: {
            ButtonCmp,
            InputCmp,
            TextAreaCmp
        }
    }
</script>

<style lang="scss" scoped>
@import '/src/assets/styles/custom.scss'; 

.new-modal {
    @include flexRow( center, center );
    position: absolute;
    height: 100vh;
    width: 100vw;
    background-color: $main-backdrop;

    &-form {
        @include flexCol( flex-start, center );
        height: 98%;
        width: 99%;
        background-color: $main-light;

        &-header {
            @include flexRow( space-between, center );
            height: 50px;
            width: 100%;
            border-bottom: $main-border-dark1;

            &-order {
                @include flexRow( center, center );
                height: 100%;
                width: auto;
                margin-left: 10px;
                font-size: 24px;
                font-weight: normal;
                font-family:sans-serif;
                color: $main-dark;
            }

            &-closed {
                @include flexRow( center, center );
                height: 100%;
                width: auto;
            }
        }

        &-section {
            @include flexRow( space-between, center );
            height: calc( 100% - 50px );
            width: 100%;

            &-left {
                @include flexRow( center, center );
                height: 100%;
                width: 40%;

                &-inputs-section {
                    @include flexCol( flex-start, center );
                    height: 90%;
                    width: 90%;

                    &-bottom {
                        margin-top: 20px;
                        width: 100%;
                    }
                }
            }

            &-right {
                @include flexRow( center, center );
                height: 100%;
                width: 60%;

                &-inputs-section {
                    @include flexCol( flex-start, center );
                    height: 90%;
                    width: 90%;

                    &-bottom {
                        margin-top: 20px;
                        width: 100%;
                    }
                }
            }
        }
    }
}

.confirm-section {
    @include flexRow( flex-end, center );
    margin-top: 15px;
    height: 50px;
    width: 99%;
}
</style>
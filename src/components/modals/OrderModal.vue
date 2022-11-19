<template>
    <div class="order-modal">
        <add-service v-if="addServiceItem"
            @close-add-modal="closeAddModal" />
        <div class="order-modal-form">
            <div class="order-modal-form-header">
                <div class="order-modal-form-header-order">Заказ № {{ orderData.client_number }}</div>
                <div class="order-modal-form-header-closed">
                    <button-cmp name="Закрыть"
                        @click-handler="$emit( 'close-order-modal' )" />
                </div>
            </div>
            <div class="order-modal-form-section">
                <div class="order-modal-form-section-left">
                    <div class="order-modal-form-section-left-inputs-section">
                        

                        <div class="order-modal-form-section-left-inputs-section-bottom col-y">
                            <span class="field-description">Клиент :</span>
                            <text-field class="mt-10" :fieldData="orderData.client_name" />
                            <text-field class="mt-10" :fieldData="orderData.client_tel_number" />
                        </div>
                        
                        <div class="order-modal-form-section-left-inputs-section-bottom">
                            <span class="field-description">Устройство :</span>
                            <text-field class="mt-10" :fieldData="orderData.client_reason" />
                            <text-field class="mt-10" :fieldData="orderData.client_device_type" />
                            <text-field class="mt-10" :fieldData="orderData.client_device_manufacturer" />
                            <text-field class="mt-10" :fieldData="orderData.client_device_model" />

                        </div>

                        <div class="order-modal-form-section-left-inputs-section-bottom">
                            <span class="field-description">Условные параметры :</span>
                            <text-field class="mt-10" fieldData="Примерная стоимость услуг 500 рублей" />
                            <text-field class="mt-10" fieldData="Нет записей" />
                        </div>
                    </div>

                </div>

                <div class="order-modal-form-section-right">
                    <div class="order-modal-form-section-right-inputs-section">
                        
                        <div class="order-modal-form-section-right-inputs-section-bottom">
                            <span class="field-description">Предоставленные услуги :</span>
                            <div class="service-item-section">
                                
                                <div class="service-item-section-item">
                                    <div class="service-item-section-item-field">
                                        <span class="field-description-small">Услуга</span>
                                        <span class="service-item-value">Замена дисплейного модуля</span>
                                    </div>
                                    <div class="service-item-section-item-field">
                                        <span class="field-description-small">Стоимость запчастей</span>
                                        <span class="service-item-value">2200 &#8381;</span>
                                    </div>
                                    <div class="service-item-section-item-field">
                                        <span class="field-description-small">Стоимость работ</span>
                                        <span class="service-item-value">2400 &#8381;</span>
                                    </div>
                                    <div class="service-item-section-item-field">
                                        <span class="field-description-small">Стоимость услуги</span>
                                        <span class="service-item-value">4600 &#8381;</span>
                                    </div>
                                </div>
                                <div class="service-item-section-item">
                                    <div class="service-item-section-item-field">
                                        <span class="field-description-small">Услуга</span>
                                        <span class="service-item-value">Замена аккумулятора</span>
                                    </div>
                                    <div class="service-item-section-item-field">
                                        <span class="field-description-small">Стоимость запчастей</span>
                                        <span class="service-item-value">700 &#8381;</span>
                                    </div>
                                    <div class="service-item-section-item-field">
                                        <span class="field-description-small">Стоимость работ</span>
                                        <span class="service-item-value">1400 &#8381;</span>
                                    </div>
                                    <div class="service-item-section-item-field">
                                        <span class="field-description-small">Стоимость услуги</span>
                                        <span class="service-item-value">2100 &#8381;</span>
                                    </div>
                                </div>
                                <div class="service-item-section-item">
                                    <div class="service-item-section-item-field">
                                        <span class="field-description-small">Услуга</span>
                                        <span class="service-item-value">Замена задней крышки</span>
                                    </div>
                                    <div class="service-item-section-item-field">
                                        <span class="field-description-small">Стоимость запчастей</span>
                                        <span class="service-item-value">900 &#8381;</span>
                                    </div>
                                    <div class="service-item-section-item-field">
                                        <span class="field-description-small">Стоимость работ</span>
                                        <span class="service-item-value">1200 &#8381;</span>
                                    </div>
                                    <div class="service-item-section-item-field">
                                        <span class="field-description-small">Стоимость услуги</span>
                                        <span class="service-item-value">2100 &#8381;</span>
                                    </div>
                                </div>

                            </div>
                            <div class="confirm-section">
                                <button-cmp name="Добавить услугу" 
                                    @click-handler="addService" />
                            </div>
                        </div>

                        <div class="order-modal-form-section-right-inputs-section-bottom col-y    ">
                            <span class="field-description">Общая стоимость всех  услуг :</span>
                            <text-field class="mt-10" fieldData="Итого" />
                        </div>

                        <!-- <div class="confirm-section">
                            <button-cmp name="Создать заказ" 
                                @click-handler="$emit( 'close-order-modal' )" />
                        </div> -->
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import ButtonCmp from '../UI/ButtonCmp.vue';
import AddService from '../modals/AddService.vue'
// import InputCmp from '../UI/InputCmp.vue';
// import TextAreaCmp from '../UI/TextAreaCmp.vue';

import TextField from '../UI/TextField.vue'

    export default {
        props: {
            orderData: { type: Object, default: () => { return {} } }
        },

        data() {
            return {
                addServiceItem: false
            }
        },

        components: {
            ButtonCmp,
            AddService,
            // InputCmp,
            // TextAreaCmp,
            TextField
        },

        mounted() {
            console.log( this.orderData );
        },

        methods: {
            addService() {
                this.addServiceItem = true
            },

            closeAddModal() {
                this.addServiceItem = false
            }
        }
    }
</script>

<style lang="scss" scoped>
@import '/src/assets/styles/custom.scss'; 

.order-modal {
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
            height: auto;
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

.service-item-section {
    @include flexCol( flex-start, center );
    overflow-y: scroll;
    max-height: 240px;
    min-height: 70px;
    height: auto;
    width: 95%;
    margin-top: 15px;
    padding: 0px 10px 10px 10px;
    border: $main-border-dark1;
    border-radius: 4px;
    outline: none;
    background-color: #fff; 

    &-item {
        @include flexRow( space-between, center );
        min-height: 50px;
        height: 50px;
        width: 98%;
        margin-top: 15px;
        border: $main-border-dark1;
        border-radius: 4px;
        outline: none;
        background-color: #fff;

        &:hover {
              border: $main-border-red1;
        }

        &-field {
            @include flexCol( space-between, flex-start );
            height: 80%;
            width: 100%;
            margin: 2px;
            padding: 5px 0px 5px 5px;
        }

        &-field:first-child {
            @include flexCol( space-between, flex-start );
            width: 200%;
            margin: 2px;
            padding: 5px 0px 5px 5px;
        }
    }
}
</style>
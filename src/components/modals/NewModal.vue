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
                            <input-cmp class="mt-10" placeholder="Имя клиента *"
                                @emit-value="emitName" />
                            <input-cmp class="mt-10" placeholder="Номер телефона *"
                                @emit-value="emitTelNumber" /> 
                        </div>
                        
                        
                        <div class="new-modal-form-section-left-inputs-section-bottom">
                            <span class="field-description">Устройство :</span>
                            <input-cmp class="mt-10" placeholder="Причина обращения"
                                @emit-value="emitClientReason" />
                            <input-cmp class="mt-10" placeholder="Тип устройства"
                                @emit-value="emitClientDeviceType" />
                            <input-cmp class="mt-10" placeholder="Производитель"
                                @emit-value="emitClientDeviceManufacturer" />
                            <input-cmp class="mt-10" placeholder="Модель"
                                @emit-value="emitClientDeviceModel" />
                        </div>

                        <div class="new-modal-form-section-left-inputs-section-bottom">
                            <span class="field-description">Условные параметры :</span>
                            <input-cmp class="mt-10" placeholder="Примерная стоимость услуги в рублях"
                                @emit-value="emitClientApproximateCost" />
                            <input-cmp class="mt-10" placeholder="Примерная дата выдачи"
                                @emit-value="emitClientApproximateDate" />
                        </div>
                    </div>

                </div>

                <div class="new-modal-form-section-right">
                    <div class="new-modal-form-section-right-inputs-section">
                        

                        <div class="new-modal-form-section-right-inputs-section-bottom">
                            <span class="field-description">Предоплата по заказу :</span>
                            <input-cmp class="mt-10" placeholder="Сумма предоплаты в рублях"
                                @emit-value="emitClirntPrepaymentAmount" />
                            <input-cmp class="mt-10" placeholder="Метод предоплаты ( карта / наличные / перевод )"
                                @emit-value="emitClientPrepaymentMethod" />
                        </div>
                        
                        
                        <div class="new-modal-form-section-right-inputs-section-bottom">
                            <span class="field-description">Опрос :</span>
                            <input-cmp class="mt-10" placeholder="Откуда узнали о нас ?"
                                @emit-value="emitClientInterview" />
                        </div>

                        <div class="new-modal-form-section-right-inputs-section-bottom col-y    ">
                            <span class="field-description">Комментарий :</span>
                            <text-area-cmp @emit-value="emitClientComment" />
                        </div>

                        <div class="confirm-section">
                            <button-cmp name="Создать заказ" 
                                @click-handler="createOrder()" />
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
        data() {
            return {
                baseCreateUrl: 'http://localhost:7000/api/client/create',

                newClientData: {
                    client_name: '',
                    client_tel_number: '',
                    client_reason: '',
                    client_device_type: '',
                    client_device_manufacturer: '',
                    client_device_model: '',
                    client_approximate_cost_service: '',
                    client_approximate_return_date: '',
                    client_prepayment_amount: '',
                    client_prepayment_method: '',
                    client_interview: '',
                    client_comment: '',
                }
            }
        },

        components: {
            ButtonCmp,
            InputCmp,
            TextAreaCmp
        },

        methods: {
            // ---------------------------------------------------
            emitName( data ) {
                this.newClientData.client_name = data
            },
            emitTelNumber( data ) {
                this.newClientData.client_tel_number = data
            },
            emitClientReason( data ) {
                this.newClientData.client_reason = data
            },
            emitClientDeviceType( data ) {
                this.newClientData.client_device_type = data
            },
            emitClientDeviceManufacturer( data ) {
                this.newClientData.client_device_manufacturer = data
            },
            emitClientDeviceModel( data ) {
                this.newClientData.client_device_model = data
            },
            emitClientApproximateCost( data ) {
                this.newClientData.client_approximate_cost_service = data
            },
            emitClientApproximateDate( data ) {
                this.newClientData.client_approximate_return_date = data
            },
            emitClirntPrepaymentAmount( data ) {
                this.newClientData.client_prepayment_amount = data
            },
            emitClientPrepaymentMethod( data ) {
                this.newClientData.client_prepayment_method = data
            },
            emitClientInterview( data ) {
                this.newClientData.client_interview = data
            },
            emitClientComment( data ) {
                this.newClientData.client_comment = data
            },
            // ---------------------------------------------------

            async createOrder() {

                // console.log( this.newClientData );

                    try {
                        const usrKey = localStorage.getItem( 'ssntkn' )
                        const response = await fetch( this.baseCreateUrl, {
                            
                            method: 'POST',
                            mode: 'cors', 
                            cache: 'no-cache',
                            credentials: 'same-origin',
                            headers: {
                                Authorization: `Bearer ${ usrKey }`,
                                'Content-Type': 'application/json' 
                            },

                            body: JSON.stringify( this.newClientData ) 
                        });
                            const respData = await response.json();
                            return respData
                    } catch ( error ) {
                        console.log( error );
                    }

                this.messageOff( 3000 );
            },
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
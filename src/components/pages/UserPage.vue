<template>
    <div class="user-page">
        <new-modal v-if="newModal"
            @close-new-modal="closeNewOrder" />

            <order-modal v-if="orderModal" :orderData="orderData" @close-order-modal="closeOrderModal" />
        <header class="header">
            <logo-header-cmp />
            <button-cmp name="Выйти" 
                @click-handler="logout()" />
        </header>

        <div class="content">
            <div class="content-order-section">
                <div class="content-order-section-header">
                    <button-cmp class="ml-5" name="Новый заказ"
                        @click-handler="addNewOrder" />
                    <div class="content-order-section-header-search mr--5">
                        <input-cmp placeholder="Поиск" />
                        <button-cmp class="ml-5" name="Найти" />
                    </div>
                </div>

                <!-- ORDER ITEM -->
                <div class="content-order-section-item" 
                    @click="getItemData( elem )"
                    v-for="( elem, elemIndex ) in  mockOrderData " :key="elemIndex" >

                    <div class="content-order-section-item-elems"
                    v-for="( item, itemIndex ) in  Object.entries( elem ) " :key="itemIndex" >
                        <span class="content-order-section-item-elems-description">
                            {{ item[ 0 ] }}
                        </span>
                        <span class="content-order-section-item-elems-value">
                            {{ item[ 1 ] }}
                        </span>
                    </div>
                    
                </div>
                <!-- ORDER ITEM -->

            </div>
        </div>

    </div>
</template>

<script>
import LogoHeaderCmp from '../UI/LogoHeaderCmp.vue'
import ButtonCmp from '../UI/ButtonCmp.vue';
import InputCmp from '../UI/InputCmp.vue';

import NewModal from '../modals/NewModal.vue'
import OrderModal from '../modals/OrderModal.vue'

import { mockOrderData } from '/src/assets/data/mockData.js'

    export default {
        data() {
            return {
                baseLogout: 'http://localhost:7000/api/logout',

                orderData: {},
                mockOrderData,
                newModal: false,
                orderModal: false   
            }
        },

        methods: {
            addNewOrder() {
                this.newModal = true
            },

            closeNewOrder() {
                this.newModal = false
            },

            closeOrderModal() {
                this.orderModal = false
            },

            getItemData( payload ) {
                this.orderModal = true
                this.orderData = payload
                console.log( payload );
            },

            async logout() {
                const response = await fetch( this.baseLogout, {
                    method: 'POST',
                    mode: 'cors',
                    cache: 'no-cache',
                    credentials: 'same-origin',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    redirect: 'follow',
                    referrerPolicy: 'no-referrer',
                });

                const respData = await response.json();
                console.log( respData );
                localStorage.removeItem( 'ssntkn' );
                this.$emit( 'to-auth-page' );
            }
        
        },

        components: {
            LogoHeaderCmp,
            ButtonCmp,
            InputCmp,
            NewModal,
            OrderModal
        }
    }
</script>

<style lang="scss" scoped>
@import '/src/assets/styles/custom.scss'; 

.user-page {
    height: 100vh;
    @include flexCol( space-between, center );
}

.header {
    @include flexRow( space-between, center );
    height: 50px;
    width: 100%;
    background-color: $main-dark;
}

.content {
    @include flexRow( center, center );
    height: calc( 100vh - 51px );
    width: 100%;
    background-color: $main-dark;

    &-order-section {
        @include flexCol( flex-start, center );
        height: 99%;
        width: 99.6%;
        overflow: auto;
        background-color: #fff;

        &-header {
            @include flexRow( space-between, center );
            min-height: 40px;
            width: 99.2%;
            margin-top: 2px;
            background-color: $main-dark;

            &-search {
                @include flexRow( space-between, center );
                height: 100%;
                width: auto;
            }
        }

        &-item {
            @include flexRow( space-between, center );
            min-height: 40px;
            width: 99.1%;
            margin: 2px 0px 2px 0px;
            border: $main-border-dark1;

             &:hover {
                background-color: $main-hover-grey;
             }

            &-elems {
                @include flexCol( flex-start, flex-start );
                height: 96%;
                width: 100%;
                margin: 0px 4px 0px 4px;
                // border: $main-border-red1;

                &-description {
                    @include flexRow( flex-start, center );
                    height: 50%;
                    font-size: 9px;
                    margin: 0px 5px 0px 5px;
                    font-weight: normal;
                    font-family:sans-serif;
                    color: $main-dark;
                }

                &-value {
                    height: 50%;
                    font-size: 11px;
                    margin-left: 5px;
                    margin: 0px 5px 0px 5px;
                    font-weight: normal;
                    font-family:sans-serif;
                    color: $main-dark;
                }
            }
        }
    }
}



</style>
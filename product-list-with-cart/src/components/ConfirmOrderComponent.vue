<script setup>
import { ref, defineProps, computed } from "vue";

const props = defineProps({
    cart: {
        type: Object,
        required: true,
    },
    show: {
        type: Boolean,
    },
});

const totalPrice = computed(() => {
    let total = 0;
    for (const key in props.cart) {
        const item = props.cart[key];
        total += item.count * item.price;
    }
    return total.toFixed(2);
});
</script>

<template>
    <div class="confirm-order-page" v-show="props.show">
        <div class="confirm-order">
            <img src="/icon-order-confirmed.svg" alt="" />
            <div class="confirm-order-content">
                <h2 class="title">Order Confirmed</h2>
                <p class="description">We hope you enjoy your food!</p>
            </div>
            <div class="confirm-order-result">
                <div class="orders">
                    <div
                        class="order"
                        v-for="(item, key) in cart"
                        :key="item.id"
                    >
                        <img :src="item.image.thumbnail" alt="" />
                        <div class="order-content">
                            <div class="left">
                                <p class="order-name">{{ item.name }}</p>
                                <div class="order-detail">
                                    <p class="order-count">{{ item.count }}x</p>
                                    <p class="order-price">
                                        ${{ item.price.toFixed(2) }}
                                    </p>
                                </div>
                            </div>
                            <div class="right">
                                <p class="total-price">
                                    ${{ (item.count * item.price).toFixed(2) }}
                                </p>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="order-total">
                    <p>Order Total</p>
                    <p class="order-total-price">${{ totalPrice }}</p>
                </div>
            </div>

            <button
                class="start-new-order"
                @click="
                    () => {
                        $emit('open', false);
                        $emit('reset');
                    }
                "
            >
                Start New Order
            </button>
        </div>
    </div>
</template>

<style scoped lang="scss">
.confirm-order-page {
    width: 100%;
    height: 100%;
    position: fixed;
    top: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    @media screen and (max-width: 768px) {
        align-items: flex-end;
    }

    .confirm-order {
        width: 550px;
        min-height: 550px;
        background: white;
        padding: 40px;
        display: flex;
        flex-direction: column;
        gap: 20px;
        border-radius: 10px;
        @media screen and (max-width: 768px) {
            min-height: 750px;
            padding: 20px;
        }

        img {
            width: 50px;
            height: 50px;
        }

        .confirm-order-content {
            .title {
                font-size: 32px;
                color: var(--rose-900);
            }

            .description {
                color: var(--rose-400);
                margin-top: 10px;
            }
        }

        .confirm-order-result {
            background: var(--rose-100);
            border-radius: 5px;
            .orders {
                border-radius: 15px;

                .order {
                    display: flex;
                    gap: 20px;
                    font-family: var(--red-hat);
                    padding: 20px;
                    border-bottom: 1px solid #e3e3e3;

                    img {
                        border-radius: 5px;
                    }

                    .order-content {
                        display: flex;
                        justify-content: space-between;
                        width: 100%;
                        .left {
                            display: flex;
                            flex-direction: column;
                            justify-content: center;
                            gap: 10px;
                            .order-name {
                                color: var(--rose-900);
                                font-weight: var(--font-weight-semibold);
                                font-size: 15px;
                            }
                            .order-detail {
                                display: flex;
                                gap: 10px;

                                .order-count {
                                    color: var(--red);
                                    font-weight: var(--font-weight-semibold);
                                    font-size: 14px;
                                }

                                .order-price {
                                    color: var(--rose-400);
                                    font-size: 14px;
                                }
                            }
                        }
                        .right {
                            display: flex;
                            justify-content: center;
                            align-items: center;

                            font-weight: var(--font-weight-semibold);
                            color: var(--rose-900);
                        }
                    }
                }
            }

            .order-total {
                display: flex;
                justify-content: space-between;
                padding: 30px 20px;

                align-items: center;

                p {
                    font-size: 14px;
                    color: rgba(0, 0, 0, 0.5);
                    font-weight: var(--font-weight-semibold);
                }

                .order-total-price {
                    font-size: 22px;
                    font-weight: var(--font-weight-bold);
                    color: var(--rose-900);
                }
            }
        }

        .start-new-order {
            border: none;
            background: var(--red);
            color: var(--rose-50);
            padding: 15px 0px;
            font-size: 16px;
            font-family: var(--font-red-hat);
            font-weight: var(--font-weight-semibold);
            border-radius: 35px;
        }
    }
}
</style>

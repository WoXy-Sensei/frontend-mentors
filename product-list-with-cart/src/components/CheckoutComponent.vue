<script setup>
import { defineProps, ref, computed } from "vue";

const props = defineProps({
    cart: Object,
});

const totalPrice = computed(() => {
    let total = 0;
    for (const key in props.cart) {
        const item = props.cart[key];
        total += item.count * item.price;
    }
    return total.toFixed(2);
});

const totalCount = computed(() => {
    let count = 0;
    for (const key in props.cart) {
        count += props.cart[key].count;
    }
    return count;
});

const isCartEmpty = computed(() => {
    return Object.keys(props.cart).length === 0;
});
</script>

<template>
    <div class="check-out">
        <h2 class="title">Your Cart ({{ totalCount }})</h2>
        <div class="cart">
            <div class="cart-is-empty" v-if="isCartEmpty">
                <div class="image">
                    <img src="/illustration-empty-cart.svg" alt="" />
                </div>
                <p>Your added items will appear here</p>
            </div>
            <div
                v-for="(item, key) in cart"
                :key="key"
                class="cart-dessert"
                v-else
            >
                <div class="dessert-content">
                    <div class="dessert-name">{{ item.name }}</div>
                    <div class="dessert-detail">
                        <p class="dessert-count">{{ item.count }}x</p>
                        <p class="dessert-price">${{ item.price.toFixed(2) }}</p>
                        <p class="dessert-total-price">
                            ${{ (item.count * item.price).toFixed(2) }}
                        </p>
                    </div>
                </div>
                <div class="dessert-actions">
                    <button
                        class="dessert-remove-button"
                        @click="$emit('remove', item.id)"
                    >
                        <img src="/icon-remove-item.svg" alt="Remove Item" />
                    </button>
                </div>
            </div>
        </div>
        <div class="order-total" v-if="!isCartEmpty">
            <p>Order Total</p>
            <p class="order-total-price">${{ totalPrice }}</p>
        </div>

        <div class="neutral-info" v-if="!isCartEmpty">
            <img src="/icon-carbon-neutral.svg" alt="" />
            <p>This is a <strong>carbon-neutral</strong> delivery</p>
        </div>

        <button class="confirm-order-button" v-if="!isCartEmpty" @click="$emit('open',true)">
            Confirm Order
        </button>
    </div>
</template>

<style lang="scss">
.check-out {
    background: white;
    display: flex;
    flex-direction: column;
    gap: 20px;
    padding: 25px;
    border-radius: 15px;
    @media screen and (max-width: 768px) {
        width: 100%;
    }

    .title {
        font-family: var(--font-red-hat);
        color: var(--red);
    }
    .cart {
        .cart-is-empty {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            gap: 20px;
            
            .image{
                height: 160px;
                
                img {
                    width: 100%;
                    height: 100%;
                    object-fit: contain;
                }
            }
            
            p{
                color: var(--rose-500);
                font-weight: var(--font-weight-semibold);
            }
        }
        .cart-dessert {
            border-bottom: 1px solid #eee;
            display: flex;
            width: 100%;
            justify-content: space-between;
            align-items: center;
            padding: 15px 0px;
            .dessert-content {
                display: flex;
                flex-direction: column;
                gap: 10px;
                .dessert-name {
                    color: var(--rose-900);
                    font-weight: var(--font-weight-semibold);
                }
                .dessert-detail {
                    font-family: var(--font-red-hat);
                    .dessert-count {
                        margin-right: 12px;
                        color: var(--red);
                        font-weight: var(--font-weight-semibold);
                    }
                    .dessert-price {
                        color: var(--rose-500);
                    }
                    .dessert-total-price {
                        color: var(--rose-500);
                        font-weight: var(--font-weight-semibold);
                    }
                    display: flex;
                    gap: 8px;
                }
            }
            .dessert-actions {
                button {
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    width: 25px;
                    height: 25px;
                    border-radius: 100%;
                    padding: 5px;
                    border: 1px solid var(--rose-500);
                    background: transparent;
                    color: var(--rose-500);
                }
            }
        }
    }

    .order-total {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 10px;
        p {
            color: var(--rose-900);
            font-size: 16px;
            font-family: var(--font-red-hat);
        }
        .order-total-price {
            font-weight: var(--font-weight-bold);
            font-size: 24px;
            color: var(--rose-900);
        }
    }

    .neutral-info {
        display: flex;
        margin: auto auto;
        padding: 20px 60px;
        background: var(--rose-50);
        color: var(--rose-900);
        gap: 10px;
        
        @media screen and (max-width: 768px) {
            padding: 20px 10px;
            font-size: 14px;
        }

    }

    .confirm-order-button {
        border: none;
        background: var(--red);
        color: var(--rose-50);
        padding: 18px 0px;
        font-size: 18px;
        font-family: var(--font-red-hat);
        font-weight: var(--font-weight-semibold);
        border-radius: 35px;
    }
}
</style>

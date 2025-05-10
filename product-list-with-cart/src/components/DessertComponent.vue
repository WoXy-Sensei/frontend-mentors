<script setup>
import { defineProps } from "vue";

const props = defineProps({
    dessert: Object,
    cartInfo: Object,
});

const priceFormat = (price) => {
    return price.toLocaleString("en-US", {
        minimumFractionDigits: 2,
        maximumFractionDigits: 2,
    });
};
</script>

<template>
    <div class="dessert">
        <div class="image">
            <img
                :src="`/${props.dessert.image.desktop}`"
                alt=""
                :class="{ active: props.cartInfo && props.cartInfo.count > 0 }"
            />
        </div>
        <div
            class="add-to-cart-button image-button"
            v-if="!props.cartInfo || props.cartInfo.count == 0"
        >
            <button @click="$emit('addedToCart', props.dessert.id)">
                <img src="/icon-add-to-cart.svg" alt="" />
                Add To Cart
            </button>
        </div>

        <div class="inc-dec-button image-button" v-else>
            <button class="inc" @click="$emit('inc', props.dessert.id)">
                <img src="/icon-increment-quantity.svg" alt="Remove Item" />
            </button>
            <span>{{ props.cartInfo.count }}</span>
            <button class="dec" @click="$emit('dec', props.dessert.id)">
                <img src="/icon-decrement-quantity.svg" alt="Remove Item" />
            </button>
        </div>

        <div class="content">
            <p class="category">{{ props.dessert.category }}</p>
            <p class="name">{{ props.dessert.name }}</p>
            <p class="price">${{ priceFormat(props.dessert.price) }}</p>
        </div>
    </div>
</template>

<style scoped lang="scss">
.dessert {
    width: 280px;
    position: relative;

    @media screen and (max-width: 768px) {
        width: 100%;
    }

    .image {
        width: 100%;
        margin-bottom: 30px;
        img {
            &.active {
                border: var(--red) 3px solid;
                border-radius: 10px;
            }
            width: 100%;
            height: 100%;
            border-radius: 10px;
            object-fit: cover;
        }
    }
    .image-button {
        position: absolute;
        top: 250px;
        left: 50%;
        transform: translateX(-50%);
    }
    .add-to-cart-button {
        button {
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 10px;
            border: 1px solid var(--rose-300);
            background: var(--rose-50);
            padding: 12px 25px;
            font-size: 14px;
            font-family: var(--font-red-hat);
            font-weight: 600;
            border-radius: 50px;
            width: 170px;
            outline: none;
        }
    }

    .inc-dec-button {
        display: flex;
        justify-content: space-between;
        flex-direction: row;
        align-items: center;
        border: 1px solid black;
        padding: 12px 10px;
        width: 170px;
        background: var(--red);
        border-radius: 50px;
        color: var(--rose-50);
        border: none;

        span {
            font-size: 15px;
        }

        button {
            border: var(--rose-50) 1px solid;
            border-radius: 100%;
            height: 16px;
            width: 16px;
            display: flex;
            justify-content: center;
            align-items: center;
            background: none;
            color: var(--rose-50);
            padding: 9px;
            font-weight: var(--font-weight-semibold);
            outline: none;
        }
    }

    .content {
        font-family: var(--font-red-hat);
        display: flex;
        flex-direction: column;
        gap: 1px;
        .category {
            color: black;
            opacity: 50%;
            font-size: 14px;
        }
        .name {
            font-size: 16px;
            font-weight: var(--font-weight-semibold);
        }
        .price {
            color: var(--red);
            font-weight: var(--font-weight-semibold);
        }
    }
}
</style>

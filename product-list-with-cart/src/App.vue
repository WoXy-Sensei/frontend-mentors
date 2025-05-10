<script setup>
import { ref } from "vue";
import DessertComponent from "./components/DessertComponent.vue";
import CheckoutComponent from "./components/CheckoutComponent.vue";
import ConfirmOrderComponent from "./components/ConfirmOrderComponent.vue";
const data = ref([
    {
        id: 1,
        image: {
            thumbnail: "image-waffle-thumbnail.jpg",
            mobile: "image-waffle-mobile.jpg",
            tablet: "image-waffle-tablet.jpg",
            desktop: "image-waffle-desktop.jpg",
        },
        name: "Waffle with Berries",
        category: "Waffle",
        price: 6.5,
    },
    {
        id: 2,
        image: {
            thumbnail: "image-creme-brulee-thumbnail.jpg",
            mobile: "image-creme-brulee-mobile.jpg",
            tablet: "image-creme-brulee-tablet.jpg",
            desktop: "image-creme-brulee-desktop.jpg",
        },
        name: "Vanilla Bean Crème Brûlée",
        category: "Crème Brûlée",
        price: 7.0,
    },
    {
        id: 3,
        image: {
            thumbnail: "image-macaron-thumbnail.jpg",
            mobile: "image-macaron-mobile.jpg",
            tablet: "image-macaron-tablet.jpg",
            desktop: "image-macaron-desktop.jpg",
        },
        name: "Macaron Mix of Five",
        category: "Macaron",
        price: 8.0,
    },
    {
        id: 4,
        image: {
            thumbnail: "image-tiramisu-thumbnail.jpg",
            mobile: "image-tiramisu-mobile.jpg",
            tablet: "image-tiramisu-tablet.jpg",
            desktop: "image-tiramisu-desktop.jpg",
        },
        name: "Classic Tiramisu",
        category: "Tiramisu",
        price: 5.5,
    },
    {
        id: 5,
        image: {
            thumbnail: "image-baklava-thumbnail.jpg",
            mobile: "image-baklava-mobile.jpg",
            tablet: "image-baklava-tablet.jpg",
            desktop: "image-baklava-desktop.jpg",
        },
        name: "Pistachio Baklava",
        category: "Baklava",
        price: 4.0,
    },
    {
        id: 6,
        image: {
            thumbnail: "image-meringue-thumbnail.jpg",
            mobile: "image-meringue-mobile.jpg",
            tablet: "image-meringue-tablet.jpg",
            desktop: "image-meringue-desktop.jpg",
        },
        name: "Lemon Meringue Pie",
        category: "Pie",
        price: 5.0,
    },
    {
        id: 7,
        image: {
            thumbnail: "image-cake-thumbnail.jpg",
            mobile: "image-cake-mobile.jpg",
            tablet: "image-cake-tablet.jpg",
            desktop: "image-cake-desktop.jpg",
        },
        name: "Red Velvet Cake",
        category: "Cake",
        price: 4.5,
    },
    {
        id: 8,
        image: {
            thumbnail: "image-brownie-thumbnail.jpg",
            mobile: "image-brownie-mobile.jpg",
            tablet: "image-brownie-tablet.jpg",
            desktop: "image-brownie-desktop.jpg",
        },
        name: "Salted Caramel Brownie",
        category: "Brownie",
        price: 4.5,
    },
    {
        id: 9,
        image: {
            thumbnail: "image-panna-cotta-thumbnail.jpg",
            mobile: "image-panna-cotta-mobile.jpg",
            tablet: "image-panna-cotta-tablet.jpg",
            desktop: "image-panna-cotta-desktop.jpg",
        },
        name: "Vanilla Panna Cotta",
        category: "Panna Cotta",
        price: 6.5,
    },
]);

const cart = ref({});
const showConfirmModalRef = ref(false);

const showConfirmModal = (show) => {
    showConfirmModalRef.value = show;
};

const resetCart = () => {
    console.log("test");
    cart.value = {};
};

const addItemToCart = (itemId) => {
    if (!cart.value[itemId]) {
        cart.value[itemId] = {
            count: 1,
            ...data.value.find((item) => item.id == itemId),
        };
    } else {
        cart.value[itemId].count = 1;
    }
};

const incItem = (itemId) => {
    cart.value[itemId].count += 1;
};

const decItem = (itemId) => {
    if (cart.value[itemId].count - 1 == 0) {
        delete cart.value[itemId];
        return;
    }
    cart.value[itemId].count -= 1;
};

const removeItemFromCart = (itemId) => {
    console.log(itemId);
    delete cart.value[itemId];
};
</script>

<template>
    <div class="page">
        <div class="desserts-section">
            <h1 class="title">Desserts</h1>
            <div class="desserts">
                <DessertComponent
                    v-for="(dessert, index) in data"
                    :dessert="dessert"
                    :key="index"
                    @addedToCart="addItemToCart"
                    @inc="incItem"
                    @dec="decItem"
                    :cart-info="cart[dessert.id]"
                />
            </div>
        </div>
        <div class="checkout-section">
            <CheckoutComponent
                :cart="cart"
                @remove="removeItemFromCart"
                @open="showConfirmModal"
            />
        </div>

        <ConfirmOrderComponent
            :cart="cart"
            @open="showConfirmModal"
            @reset="resetCart"
            :show="showConfirmModalRef"
        />
    </div>
</template>

<style scoped lang="scss">
.page {
    display: flex;
    flex-direction: row;
    margin-top: 70px;
    margin-bottom: 70px;
    max-width: 1400px;
    margin: 70px auto;
    padding: 20px;

    @media screen and (max-width: 768px) {
        flex-direction: column;
        justify-content: center;
        align-items: center;
        width: 100%;
        margin: 30px auto;
    }

    .desserts-section {
        display: flex;
        gap: 30px;
        flex-direction: column;
        width: 900px;

        @media screen and (max-width: 768px) {
            flex-direction: column;
            justify-content: center;
            align-items: center;
            width: 100%;
        }

        .title {
            font-family: var(--font-red-hat);
            font-size: 2.3rem;
            color: var(--rose-900);
        }

        .desserts {
            display: flex;
            flex-direction: row;
            flex-wrap: wrap;
            gap: 20px;

            @media screen and (max-width: 768px) {
                flex-direction: column;
                justify-content: center;
                align-items: center;
            }
        }
    }
    .checkout-section {
        width: 450px;
        @media screen and (max-width: 768px) {
            flex-direction: column;
            justify-content: center;
            align-items: center;
            width: 100%;
            margin: 20px;
        }
    }
}
</style>

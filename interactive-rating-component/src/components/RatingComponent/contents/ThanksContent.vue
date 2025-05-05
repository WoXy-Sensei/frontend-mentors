<script setup>
import { defineProps } from "vue";

const props = defineProps({
    rating: {
        type: Number,
        required: true,
    },
});
</script>

<template>
    <div class="thanks-content">
        <div class="thanks-image">
            <img src="/illustration-thank-you.svg" alt="" />
        </div>
        <div class="rating-info">
            <p>You selected {{ props.rating }} out of 5</p>
        </div>
        <div class="content">
            <div class="title">Thank You!</div>
            <div class="description">
                We appreciate you taking the time to give a rating. If you ever
                need more support, don’t hesitate to get in touch!
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.thanks-content {
    display: flex;
    flex-direction: column;
    justify-content: space-around;
    align-items: center;
    height: 100%;
    width: 100%;

    .rating-info {
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 8px 25px;
        background-color: var(--neutral-grey-900);
        color: var(--primary-orange);
        border-radius: 50px;
    }

    .content {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;

        .title {
            font-size: 32px;
            font-weight: bold;
            margin-bottom: 16px;
        }

        .description {
            font-size: 16px;
            line-height: 1.5;
            text-align: center;
            color: var(--neutral-grey-500);
        }
    }
}
</style>

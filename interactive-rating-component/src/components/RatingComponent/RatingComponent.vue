<script setup>
import RatingContent from "./contents/RatingContent.vue";
import ThanksContent from "./contents/ThanksContent.vue";

import { ref } from "vue";

const rating = ref(0);
const isSubmitted = ref(false);

const handleRating = (value) => {
    rating.value = value;
};

const handleSubmit = () => {
    isSubmitted.value = true;
};
</script>

<template>
    <div class="rating">
        <ThanksContent :rating="rating" v-if="isSubmitted" />
        <RatingContent @rating="handleRating" @submit="handleSubmit" v-else />
    </div>
</template>

<style scoped lang="scss">
.rating {
    width: 450px;
    height: 460px;

    box-shadow: 0px 4px 16px rgba(0, 0, 0, 0.1);
    border-radius: 32px;

    background: radial-gradient(
        circle at top center,
        var(--neutral-grey-900),
        var(--neutral-grey-950)
    );

    padding: 35px;
}
</style>

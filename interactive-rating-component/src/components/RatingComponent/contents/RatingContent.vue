<script setup>
import { ref } from "vue";

const selectedRating = ref(null);

const emit = defineEmits(["rating"]);

const handleRating = (rating) => {
    selectedRating.value = rating;
    emit("rating", rating);
};
</script>

<template>
    <div class="rating-content">
        <div class="star">
            <img src="/icon-star.svg" alt="" />
        </div>
        <div class="content">
            <div class="title">How did we do?</div>
            <div class="description">
                Please let us know how we did with your support request. All
                feedback is appreciated to help us improve our offering!
            </div>
        </div>
        <div class="ratings">
            <button
                class="rating-btn"
                :class="{ active: selectedRating === 1 }"
                @click="handleRating(1)"
            >
                1
            </button>
            <button
                class="rating-btn"
                :class="{ active: selectedRating === 2 }"
                @click="handleRating(2)"
            >
                2
            </button>
            <button
                class="rating-btn"
                :class="{ active: selectedRating === 3 }"
                @click="handleRating(3)"
            >
                3
            </button>
            <button
                class="rating-btn"
                :class="{ active: selectedRating === 4 }"
                @click="handleRating(4)"
            >
                4
            </button>
            <button
                class="rating-btn"
                :class="{ active: selectedRating === 5 }"
                @click="handleRating(5)"
            >
                5
            </button>
        </div>

        <div class="submit">
            <button class="submit-btn" @click="$emit('submit')">Submit</button>
        </div>
    </div>
</template>

<style scoped lang="scss">
.rating-content {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100%;

    .star {
        padding: 12px;
        background-color: var(--neutral-grey-900);
        display: flex;
        align-items: center;
        justify-content: center;
        width: 55px;
        height: 55px;
        border-radius: 50%;

        img {
            width: 18px;
            height: 18px;
        }
    }

    .content {
        .title {
            font-size: 28px;
            font-weight: bold;
            margin-bottom: 12px;
        }

        .description {
            font-size: 16px;
            line-height: 1.8;
            color: var(--neutral-grey-500);
        }
    }

    .ratings {
        display: flex;
        justify-content: space-around;

        .rating-btn {
            background-color: var(--neutral-grey-900);
            display: flex;
            align-items: center;
            justify-content: center;
            width: 55px;
            height: 55px;
            border-radius: 50%;
            border: none;
            color: var(--neutral-grey-500);
            font-size: 16px;
            font-weight: 500;
            transition: background-color 0.2s ease;
            cursor: pointer;

            &:hover {
                background-color: var(--neutral-white);
                color: var(--neutral-grey-900);
            }

            &.active {
                background-color: var(--primary-orange);
                color: var(--neutral-white);
            }
        }
    }

    .submit {
        .submit-btn {
            background-color: var(--primary-orange);
            display: flex;
            align-items: center;
            justify-content: center;
            width: 100%;
            border-radius: 50px;
            border: none;
            color: var(--neutral-grey-950);
            font-weight: 500;
            letter-spacing: 2px;
            text-transform: uppercase;
            padding: 16px 0px;
            font-size: 16px;
            cursor: pointer;
            transition: background-color 0.2s ease;

            &:hover {
                background-color: var(--neutral-white);
            }
        }
    }
}
</style>

<script setup>
import { defineProps } from "vue";
import { useStore } from "../store/store";

const store = useStore();
</script>

<template>
    <nav>
        <div class="logo">
            <div class="logo-img">
                <img src="../assets/images/logo-solo.svg" alt="" />
            </div>
            <div class="logo-text">Extensions</div>
        </div>
        <div class="theme-button">
            <button @click="$emit('toggle-theme')">
                <img
                    src="../assets/images/icon-sun.svg"
                    alt=""
                    v-if="store.isDarkMode"
                />
                <img src="../assets/images/icon-moon.svg" alt="" v-else />
            </button>
        </div>
    </nav>
</template>

<style lang="scss">
nav {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    background-color: var(--neutral-800);
    padding: 0.9rem;
    border-radius: 18px;
    width: 100%;
    margin-bottom: 3.5rem;

    .logo {
        display: flex;
        flex-direction: row;
        gap: 16px;
        justify-content: center;
        align-items: center;

        .logo-img {
            width: 45px;
            height: 45px;
            img {
                height: 100%;
                width: 100%;
            }
        }

        .logo-text {
            font-size: 24px;
            font-weight: 700;
            color: var(--neutral-100);
        }
    }

    .theme-button {
        button {
            background-color: var(--neutral-700);
            display: flex;
            align-items: center;
            justify-content: center;
            border: none;
            padding: 14px;
            cursor: pointer;
            border-radius: 12px;
            transition: background-color 0.3s ease;

            &:hover {
                background-color: var(--neutral-600);
            }
        }
    }
}
</style>

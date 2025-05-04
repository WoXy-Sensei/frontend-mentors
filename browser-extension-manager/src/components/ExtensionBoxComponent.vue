<script setup>
import { defineProps } from "vue";

const props = defineProps({
    extension: {
        type: Object,
        required: true,
    },
    onRemove: {
        type: Function,
        required: true,
    },
    onChangeStatus: {
        type: Function,
        required: true,
    },
});
</script>

<template>
    <div class="box">
        <div class="box-header">
            <div class="box-image">
                <img :src="extension.logo" alt="" width="50px" />
            </div>
            <div class="box-content">
                <div class="title">{{ extension.name }}</div>
                <div class="description">
                    {{ extension.description }}
                </div>
            </div>
        </div>
        <div class="box-footer">
            <div class="box-actions">
                <button class="remove" @click="onRemove(extension.id)">
                    Remove
                </button>
                <label class="switch">
                    <input
                        type="checkbox"
                        :checked="extension.isActive"
                        @change="
                            onChangeStatus(extension.id, !extension.isActive)
                        "
                    />
                    <span class="slider round"></span>
                </label>
            </div>
        </div>
    </div>
</template>

<style lang="scss">
.box {
    height: 210px;
    width: 395px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    background-color: var(--neutral-800);
    border: 1px solid var(--neutral-600);
    border-radius: 16px;
    padding: 1.5rem;

    @media (max-width: 768px) {
        width: 330px;
    }

    .box-header {
        display: flex;
        flex-direction: row;
        gap: 16px;
        .box-content {
            display: flex;
            flex-direction: column;
            .title {
                font-size: 20px;
                font-weight: 700;
                margin-bottom: 8px;
                color: var(--neutral-100);
            }
            .description {
                font-size: 14px;
                font-weight: 400;
                margin-bottom: 8px;
                color: var(--neutral-300);
            }
        }
    }
    .box-footer {
        width: 100%;
        .box-actions {
            display: flex;
            align-items: center;
            justify-content: space-between;
            width: 100%;
            .remove {
                background-color: var(--neutral-800);
                border-radius: 20px;
                border: none;
                padding: 10px 18px;
                color: var(--neutral-100);
                border: 1px solid var(--neutral-600);
                font-size: 14px;
                font-weight: 500;
                cursor: pointer;
                transition: background-color 0.1s ease-in-out;

                &:hover {
                    background-color: var(--red-400);
                    color: var(--neutral-900);
                    border-color: var(--red-400);
                }
            }
            .switch {
                position: relative;
                display: inline-block;
                width: 46px;
                height: 25px;

                &:hover {
                    input:checked + .slider {
                        background-color: var(--red-500);
                    }
                }

                input {
                    opacity: 0;
                    width: 0;
                    height: 0;
                }

                .slider {
                    position: absolute;
                    cursor: pointer;
                    top: 0;
                    left: 0;
                    right: 0;
                    bottom: 0;
                    background-color: var(--neutral-600);
                    -webkit-transition: 0.4s;
                    transition: 0.4s;

                    &:before {
                        position: absolute;
                        content: "";
                        height: 17px;
                        width: 17px;
                        left: 4px;
                        bottom: 4px;
                        background-color: white;
                        -webkit-transition: 0.4s;
                        transition: 0.4s;
                    }
                }

                input:checked + .slider {
                    background-color: var(--red-400);

                    &:before {
                        -webkit-transform: translateX(21px);
                        -ms-transform: translateX(21px);
                        transform: translateX(21px);
                    }
                }

                .slider.round {
                    border-radius: 34px;

                    &:before {
                        border-radius: 50%;
                    }
                }
            }
        }
    }
}
</style>

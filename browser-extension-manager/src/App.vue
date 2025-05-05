<script setup>
import { ref, computed } from "vue";
import NavbarComponent from "./components/NavbarComponent.vue";
import ExtensionBoxComponent from "./components/ExtensionBoxComponent.vue";
import { useStore } from "./store/store";

const store = useStore();

const tab = ref("all");
const theme = ref("dark");

const filteredExtensions = ref([...store.allExtensions]);

const applyFilter = () => {
    if (tab.value === "all") {
        filteredExtensions.value = [...store.allExtensions];
    } else if (tab.value === "active") {
        filteredExtensions.value = store.activeExtensions;
    } else if (tab.value === "inactive") {
        filteredExtensions.value = store.inactiveExtensions;
    }
};

const removeExtension = (id) => {
    store.removeExtension(id);
    filteredExtensions.value = filteredExtensions.value.filter(
        (ext) => ext.id !== id,
    );
};

const handleChangeStatus = (id, newStatus) => {
    store.changeExtensionStatus(id, newStatus);
};

const changeTab = (newTab) => {
    tab.value = newTab;
    applyFilter();
};

const toggleTheme = () => {
    store.isDarkMode = !store.isDarkMode;
};
</script>

<template>
    <div class="page" :class="{ 'light-theme': !store.isDarkMode }">
        <div class="container">
            <NavbarComponent @toggle-theme="toggleTheme" />
            <div class="extension-list">
                <div class="head">
                    <div class="head-title">Extension List</div>
                    <div class="head-filter-tabs">
                        <a
                            href="#"
                            class="tab"
                            @click.prevent="changeTab('all')"
                            :class="{ active: tab === 'all' }"
                            >All</a
                        >
                        <a
                            href="#"
                            class="tab"
                            @click.prevent="changeTab('active')"
                            :class="{ active: tab === 'active' }"
                            >Active</a
                        >
                        <a
                            href="#"
                            class="tab"
                            @click.prevent="changeTab('inactive')"
                            :class="{ active: tab === 'inactive' }"
                            >Inactive</a
                        >
                    </div>
                </div>
                <div class="extensions">
                    <ExtensionBoxComponent
                        v-for="extension in filteredExtensions"
                        :key="extension.id"
                        :extension="extension"
                        :on-remove="removeExtension"
                        :on-change-status="handleChangeStatus"
                    />
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.page {
    padding: 3rem;
    .container {
        width: 1200px;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        margin: auto auto;

        @media (max-width: 1200px) {
            width: 800px;
        }

        @media (max-width: 830px) {
            width: 330px;
        }
    }
}
.extension-list {
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 3rem;
    .extensions {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        gap: 0.7rem;

        @media (max-width: 1200px) {
            grid-template-columns: repeat(2, 1fr);
        }

        @media (max-width: 830px) {
            grid-template-columns: 1fr;
        }
    }
    .head {
        display: flex;
        justify-content: space-between;
        align-items: center;
        width: 100%;

        @media (max-width: 830px) {
            flex-direction: column;
            gap: 2rem;
        }

        .head-title {
            color: var(--neutral-100);
            font-weight: 700;
            font-size: 30px;
        }

        .head-filter-tabs {
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 10px;

            .tab {
                color: var(--neutral-100);
                background-color: var(--neutral-700);
                font-weight: 500;
                font-size: 18px;
                padding: 8px 16px;
                border-radius: 24px;
                border: 1px solid var(--neutral-600);
                transition: background-color 0.3s ease;

                &:hover {
                    background-color: var(--neutral-600);
                }

                &.active {
                    color: var(--neutral-900);
                    background-color: var(--red-400);
                    border: none;

                    &:hover {
                        background-color: var(--red-500);
                    }
                }
            }
        }
    }
}
</style>

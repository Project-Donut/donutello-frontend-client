<script setup>
import { ref, onMounted } from 'vue';
import DonuttelloLogo from './components/svg/DonuttelloLogo.vue';
import UserInterface from './components/UserInterface.vue';
import ThreeScene from './scripts/three.js';
let model = ref(null);
let viewPort = ref(null);
const canvasSetup = () => {
    if (viewPort.value) {
        model.value = new ThreeScene(viewPort.value);
        model.value.sceneSetup();
    }
}
onMounted(() => {

    canvasSetup();

});
</script>

<template>
    <span class="app">
        <div class="__header">
            <DonuttelloLogo alt />
        </div>
        <div class="__viewPort">
            <div class="viewPort" ref="viewPort"></div>
        </div>
        <div class="__userInterface">
            <UserInterface v-if="model" :model="model" />
        </div>
    </span>
</template>

<style scoped>
.viewPort {
    height: 100vh;
}

.app {
    height: 100vh;
    display: grid;
    grid-template-columns: 300px 1fr;
    grid-template-rows: 60px 1fr;
    grid-template-areas:
        "header header"
        "ui viewport";
}

.__header {
    grid-area: header;
    border-bottom: 1px solid var(--surface-400);
    padding: .25em;
}

.__userInterface {
    grid-area: ui;
    overflow-y: auto;
    background-color: var(--surface-100);

    border-right: 1px solid var(--surface-400);
    box-shadow: 0px 5px 10px 0px rgba(0, 0, 0, 0.2);
}

.viewPort {
    grid-area: viewport;
    background-color: var(--color-heaven);
    height: 100vh;
}

@media screen and (max-width: 768px) {
    .app {
        display: flex;
        flex-direction: column;
    }

    .__header {
        height: 60px;
        display: flex;
        justify-content: center;
        z-index: 10;
    }

    .__viewPort {
        position: absolute;
        top: 60px;
        height: 100vh;
        width: 100vw;
    }

    .__userInterface {
        z-index: 10;
        background-color: transparent;
    }
    ::-webkit-scrollbar {
        display: none;
    }
}
</style>

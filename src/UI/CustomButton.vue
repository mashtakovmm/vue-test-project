<script setup>
const emit = defineEmits(['buttonClick'])

const handleButtonClick = () => {
    emit('buttonClick')
}
</script>

<template>
    <button class="custom-button" @click="handleButtonClick">
        <slot></slot>
    </button>
</template>

<style scoped>
.custom-button {
    border: solid 3px rgba(2, 168, 168, 0.5);
    background-color: transparent;
    border-radius: 5px;
    margin-top: 10px;
    min-width: 250px;
    min-height: 55px;
    align-self: center;
    transition: 0.25s;
    font-size: 20px;
    align-self: flex-end;
}

.custom-button:hover {
    background-color: rgba(2, 168, 168, 0.1);
}

.custom-button:active {
    background-color: rgba(2, 168, 168, 0.4);
}
</style>
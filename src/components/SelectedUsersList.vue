<script setup>
    const props = defineProps({
        selectedUsers : {
            required: true
        }
    })
</script>

<template>
    <div class="general-conainer">
        <h2>Исходный</h2>
        <div>
            <div v-for="name in selectedUsers" :key="Date.now()">
                <p class="p">{{ name }}</p>
            </div>
        </div>
    </div>
</template>

<style scoped>
.p {
    font-size: 20px;

}
</style>
<script setup>
import UsersSeacrh from './components/UsersSeacrh.vue';
import SelectedUsersList from './components/SelectedUsersList.vue';
import { ref } from 'vue';

const selectedUsers = ref([]);

function changeSelectedUsers(emitData) {
    selectedUsers.value = emitData
}

</script>

<template>
    <UsersSeacrh @emit-selected-users="changeSelectedUsers"/>
    <SelectedUsersList :selectedUsers="selectedUsers"/>
</template>

<style scoped>

</style>

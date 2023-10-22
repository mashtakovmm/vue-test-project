<script setup>
import { onBeforeMount, onMounted, ref } from 'vue';
import CustomButton from '../UI/CustomButton.vue';
const users = ref(null);
const searchQuery = ref('');
const isHidden = ref(false);
const selectedUsers = ref([])
let inputWidth;

onBeforeMount(() => {
    fetch('https://jsonplaceholder.typicode.com/users')
        .then(response => {
            console.log(response);
            response.json()
        })
        .then(json => {
            users.value = json
        })
})

function handleChooseName(name) {
    searchQuery.value = name
    isHidden.value = true
}

function handleInputClick() {
    isHidden.value = false
}

function handleButtonClick() {
    selectedUsers.value = !selectedUsers.value.includes(searchQuery.value) ? [...selectedUsers.value, searchQuery.value] : selectedUsers.value
    searchQuery.value = ''
    emit('emitSelectedUsers', selectedUsers.value);
}

const resizeObserver = new ResizeObserver(entries => {
    entries.forEach(entry => {
        inputWidth = entry.contentRect.width.toString()
    });
});

onMounted(() => {
    resizeObserver.observe(document.querySelector(".input"))
})

const emit = defineEmits(['emitSelectedUsers'])
</script>

<template>
    <div class="general-conainer">
        <h2>Найти пользователя</h2>
        <div class="user-input-container">
            <input v-model="searchQuery" type="text" placeholder="Enter surname, id or username..." class="input"
                @focus="handleInputClick()">
            <div>
                <ul class="options-list" :style="{ width: inputWidth + 'px' }">
                    <template v-for="user in users" :key="user.id">
                        <li class="name-option" :class="{ hide: isHidden }"
                            v-if="searchQuery && user.name.toLowerCase().startsWith(searchQuery.toLowerCase())"
                            @click="handleChooseName(user.name)">{{ user.name }}</li>
                    </template>
                </ul>
            </div>
            <CustomButton @button-click="handleButtonClick()">Добавить в список</CustomButton>
        </div>
    </div>
</template>

<style scoped>
.user-input-container {
    width: 600px;
    display: flex;
    flex-direction: column;
    justify-content: center;
}


.options-list {
    list-style: none;
    font-size: 20px;
    max-height: 200px;
    overflow-y: scroll;
    background-color: white;
    position: absolute;
}

.options-list::-webkit-scrollbar {
    display: none;
}

.name-option {
    padding: 5px;
    border: solid 2px rgba(0, 128, 128, 0.25);
    border-top: none;
    transition: 0.7s;
}

.name-option:hover {
    background-color: rgba(0, 128, 128, 0.15);
    cursor: pointer;
}

input {
    min-height: 40px;
    min-width: 90%;
    border: none;
    outline: 0;
    border-bottom: 2px solid rgb(1, 77, 77);
    font-size: 20px;
    text-indent: 5px;
}

input::placeholder {
    color: rgba(1, 56, 56, 0.548);
}
</style>
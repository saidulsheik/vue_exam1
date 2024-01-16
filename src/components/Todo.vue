<script setup>
import { ref, reactive } from 'vue';

const tasks = ref([
    { name: 'Task 1', time: 60 },
    { name: 'Task 2', time: 75 },
]);

const showPopup = ref(false);

const newTask = reactive({
    name: '',
    time: 0,
});

const removeTask = (index) => {
    tasks.value.splice(index, 1);
};

const openPopup = () => {
    showPopup.value = true;
};

const closePopup = () => {
    showPopup.value = false;
    newTask.name = '';
    newTask.time = 0;
};

const addTask = () => {
    if (newTask.name && newTask.time > 0) {
        tasks.value.push({ ...newTask });
        closePopup();
    } else {
        alert('Please enter valid task details.');
    }
};
</script>


<template>
    <h1 class="text-3xl font-bold mb-4">Task List</h1>
    <ul>
        <li v-for="(task, index) in tasks" :key="index"
            class="bg-white p-4 mb-4 shadow-md flex justify-between items-center">
            <span>{{ task.name }} - {{ task.time }} minutes</span>
            <button @click="removeTask(index)">Remove</button>
        </li>
    </ul>

    <button @click="openPopup">Add Task</button>

    <div v-if="showPopup">
        <div>
            <form @submit.prevent="addTask">
                <label for="taskName">Task Name:</label>
                <input type="text" id="taskName" v-model="newTask.name" required>
                <br>
                <label for="taskTime">Time
                    (minutes):</label>
                <input type="number" id="taskTime" v-model="newTask.time" required>
                <br>

                <button type="submit">Add Task</button>
            </form>
            <button @click="closePopup">Close</button>
        </div>
    </div>
</template>
<link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet"></link>
<style></style>
<script lang="ts" setup>
import { ref } from "vue";

const emit = defineEmits<{
    addTask: [newTask: string]
}>();

const error = ref("");
const newTask = ref("");

const formSubmitted = () => {
    if (newTask.value.trim()) {
        emit("addTask", newTask.value);
        newTask.value = "";
        error.value = "";
    } else {
        error.value = "Task cannot be empty";
    }
};
</script>

<template>
    <form @submit.prevent="formSubmitted">
        <label for="newTask">Add a new task
            <input v-model="newTask" name="newTask" :aria-invalid="!!error || undefined" @input="error = ''" />
            <small v-if="error" role="alert" id="invalid-helper">{{ error }}</small>
        </label>
        <div class="button-container">
            <button>Add</button>
        </div>
    </form>
</template>
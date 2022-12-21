<template>
    <div class="todo-controls mb-4">
        <h1 class="h2">Add Yo Stuff</h1>
        <form @submit.prevent="createTodo">
            <div class="d-flex">
                <input type="text" class="form-control" v-model="newTodo" />
                <button type="submit" class="btn btn-primary ms-2 text-nowrap" :disabled="!hasTodo">More Drudgery</button>
            </div>
        </form>
    </div>
</template>

<script setup>
    import { ref, computed, defineEmits } from 'vue'

    const emit = defineEmits(['created'])

    let newTodo = ref('')
    let currentId = ref(3)

    const hasTodo = computed(() => {
        return newTodo.value.length
    })

    const incrementId = () => {
        currentId.value += 1
    }

    const resetInput = () => {
        newTodo.value = ''
    }

    const createTodo = () => {
        incrementId()

        const payload = ({
            id: currentId.value,
            value: newTodo.value
        })

        emit('created', payload)

        resetInput()
    }
</script>

<style lang="scss" scoped>

</style>

<template>
    <div class="todo">
        <div v-if="!state.editing" class="title">
            {{ todo.value }}
        </div>
        <div v-else class="edit-input flex-grow-1">
            <input class="form-control w-100" v-model="state.localValue" />
        </div>
        <div class="controls ms-2">
            <div v-if="!state.editing" class="default">
                <button class="btn btn-outline-success" @click="toggleEdit">oops</button>
                <button class="btn btn-outline-danger ms-2" @click="remove">nah</button>
            </div>
            <div v-else class="edit">
                <button class="btn btn-outline-danger ms-2" @click="cancelEdit">nm.</button>
                <button class="btn btn-outline-primary" @click="saveEdit">kay</button>
            </div>
        </div>
    </div>
</template>

<script setup>
    import { reactive, defineProps, defineEmits, onMounted } from 'vue'

    const emit = defineEmits(['edit', 'remove'])

    const props = defineProps({
        todo: {
            type: Object,
            default () {
                return {}
            }
        }
    })

    const state = reactive({
        editing: false,
        localValue: ''
    })

    onMounted (() => {
        state.localValue = props.todo.value
    })

    const toggleEdit = (bool) => {
        state.editing = !state.editing || bool
    }

    const saveEdit = () => {
        emit('edit', {
            id: props.todo.id,
            update: state.localValue
        })

        toggleEdit(false)
    }

    const cancelEdit = () => {
        toggleEdit(false)
        state.localValue = props.todo.value
    }

    const remove = () => {
        emit('remove', props.todo.id)
    }
</script>

<style lang="scss" scoped>
    .todo {
        display: flex;
        justify-content: space-between;
        align-items: center;
        max-width: 100%;
        padding: .25rem 0;
        background-color: $white;

        &:not(:last-child) {
            margin-bottom: 1rem;
            border-bottom: 2px solid $medium-gray;
        }
    }

    .controls {
        .btn {
            border: none;
        }
    }
</style>

<template>
    <div class="todo-table">
        <todo-controls @created="addTodo"/>
        <h2 class="h3">Do this stuff</h2>
        <div v-if="hasTodos" class="todo-list">
            <todo
                v-for="todo in state.todos"
                :key="todo.id"
                :todo="todo"
                @remove="removeTodo"
                @edit="editTodo"
            />
        </div>
        <todo-empty v-else />
    </div>
</template>

<script setup>
  import { reactive, computed, onMounted } from 'vue'

    import TodoControls from '@/components/TodoControls.vue'
    import TodoEmpty from '@/components/TodoEmpty.vue'
    import Todo from '@/components/Todo.vue'

    const state = reactive({
        todos: null
    })

    const hasTodos = computed(() => {
        return state.todos?.length
    })

    onMounted(() => {
        state.todos = [
            {
                id: 1,
                value: 'One'
            },
            {
                id: 2,
                value: 'Two'
            },
            {
                id: 3,
                value: 'Three'
            }
        ]
    })

    const addTodo = (todo) => {
        state.todos.push(todo)
    }

    const removeTodo = (id) => {
        const index = getIndex(id)

        if (index > -1) {
            state.todos.splice(index, 1)
        }
    }

    const editTodo = ({ id, update }) => {
        const index = getIndex(id)

        if (index > -1) {
            state.todos[index] = {
                id,
                value: update
            }
        }
    }

    const getIndex = (id) => {
        const index = state.todos.findIndex(t => t.id === id)

        return index
    }
</script>

<style lang="scss" scoped>
.todo-list {
    background-color: $white;
    padding: 1.5rem;
    border: 1px solid $medium-gray;
    border-radius: .5rem;
}
</style>

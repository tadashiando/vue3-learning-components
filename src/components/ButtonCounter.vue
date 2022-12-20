<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
    setup() {
        const counter = ref(0)
        const increment = () => counter.value++
        return {
            counter, increment
        }
    }
})
</script>

<template>
    <button @click="increment" class="btn btn-info">Counter {{counter}}</button>
</template>

<style>

</style>
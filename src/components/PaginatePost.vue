<script setup>
    const props = defineProps({
        postsLength: String,
        start: String,
        end: String,
    })
    const emit = defineEmits(['next', 'previous'])
    console.log(props.postsLength);
</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button
            type="button"
            class="btn btn-outline-primary"
            :disabled="props.start <= 0"
            @click="emit('previous')">
            Previous
        </button>
        <button
            type="button"
            class="btn btn-outline-primary"
            :disabled="props.end >= props.postsLength"
            @click="emit('next')">
            Next
        </button>
    </div>
</template>
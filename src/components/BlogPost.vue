<script>
import { defineComponent } from 'vue'

export default defineComponent({
    props: {
        id: Number,
        title: String,
        message: {
            type: String,
            default: "Sin descripción"
        },
        colorText: String
    },
    emits: ['toggleFavourite'],
    setup(props, { emit }) {
        const favoritar = () => {
            emit('toggleFavourite', props.title)
        }
        return {favoritar}
    }
})
</script>

<template>
    <div class="card bg-dark">
        <div class="card-body">
            <h5 class="card-title" :class="`text-${colorText}`">{{ id }} - {{ title }}</h5>
            <p>{{ message }}</p>
            <button @click="favoritar" class="btn btn-outline-info">Favorito</button>
        </div>
    </div>
</template>
<script setup>

//const props = defineProps(['title', 'content', "colorText"])
defineProps({
    title: String,
    id: Number,
    content: {
        type: String,
        default: 'Sin descripcion'
    },
    colorText: String
})

const emit = defineEmits(['cambiarFavorito'])

</script>

<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title" :class="`text-${colorText}`">{{ id }} - {{ title }}</h5>
            <p>{{ content }}</p>
            <button @click="emit('cambiarFavorito', title)" class="btn btn-outline-primary">Favorito</button>
        </div>
    </div>
</template>
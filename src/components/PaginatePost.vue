<script setup>
    import {computed} from 'vue'
    defineProps(['inicio','fin', "totalSize"])
    const emit = defineEmits(['nextPage','previusPage'])
</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" @click="emit('previusPage')" :disabled="inicio === 0" class="btn btn-primary">Previus</button>
        <button type="button" @click="emit('nextPage')" :disabled="fin >= totalSize" class="btn btn-primary">Next</button>
    </div>
</template>
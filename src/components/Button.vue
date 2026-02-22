<template>
    <button class="button" @click="eventoClick" :disabled="cronometroRodando">
        <span class="icon">
            <i :class="['fas', icone]"></i>
        </span>
        <span>{{ nome }}</span>
    </button>
</template>

<script lang='ts'>
import { defineComponent, PropType } from "vue"

export default defineComponent({
    name: 'ButtonTracker',
    props: {
        nome: { type: String, required: true },
        icone: { type: String, required: true },
        eventoClick: { type: Function as PropType<() => void>, required: true },
        cronometroRodando: { type: Boolean }
    }
})
</script>
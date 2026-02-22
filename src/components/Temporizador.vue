<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <CronometroTracker :tempoEmSegundos="tempoEmSegundos" />
        <ButtonTracker nome="play" icone="fa-play" :eventoClick="iniciar" :disabled="cronometroRodando" />
        <ButtonTracker nome="stop" icone="fa-stop" :eventoClick="finalizar" :disabled="!cronometroRodando" />
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import CronometroTracker from './Cronometro.vue'
import ButtonTracker from './Button.vue'

export default defineComponent({
    name: 'TemporizadorTracker',
    emits: [ 'aoTemporizadorFinalizado' ],
    components: { CronometroTracker, ButtonTracker },
    data() {
        return {
            tempoEmSegundos: 0,
            cronometro: 0,
            cronometroRodando: false
        }
    },
    methods: {
        iniciar() {
            this.cronometroRodando = true
            this.cronometro = setInterval(() => {
                this.tempoEmSegundos++
            }, 1000)
        },
        finalizar() {
            this.cronometroRodando = false
            clearInterval(this.cronometro)
            this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
            this.tempoEmSegundos = 0
        }
    }
})
</script>
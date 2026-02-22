<template>
    <BoxContent>
        <div class="columns">
            <div class="column is-7">
                {{ tarefa.descricao || 'Tarefa sem descrição' }}
            </div>
            <div class="column">
                <CronometroTracker :tempoEmSegundos="tarefa.duracaoEmSegundos" />
            </div>
        </div>
    </BoxContent>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import CronometroTracker from './Cronometro.vue'
import BoxContent from './Box.vue'
import ITarefa from '@/interfaces/ITarefa';

export default defineComponent({
    name: 'TarefaTracker',
    components: { CronometroTracker, BoxContent },
    props: {
        tarefa: {
            type: Object as PropType<ITarefa>,
            required: true
        }
    }
})
</script>


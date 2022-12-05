<template>
    <TemplateBox>
        <div class="columns">
            <div class="column is-7">
                <strong>
                    {{listaTarefa.descricao || 'Tarefa sem descrição' }}
                </strong>
            </div>
            <div class="column">
                <CronometroTarefa :tempoEmSegundos="listaTarefa.duracaoEmSegundos" />
            </div>
        </div>
    </TemplateBox>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import CronometroTarefa from './CronometroTarefa.vue'
import IListaTarefa from  '../interfaces/IListaTarefa'
import TemplateBox from  './TemplateBox.vue'

export default defineComponent({
    name: 'ListaTarefa',
    components: {
        CronometroTarefa,
        TemplateBox
    },
    props: {
        listaTarefa: {
            type: Object as PropType<IListaTarefa>,
            required: true
        }
    },
    computed: {
        tempoGasto () : string {
            return new Date(this.listaTarefa.duracaoEmSegundos * 1000)
                .toISOString()
                .substr(11, 8)
        }
    }
})
</script>

<style scoped>
    .box {
        background: #ADD8E6;
    }
    strong {
        color: #2b2d42;
    }
</style>
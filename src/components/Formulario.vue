<template>
  <div class="box">
    <div class="columns">
      <div class="column is-7" role="form" aria-label="Formulário para criação de uma nova tarefa">
        <input type="text" class="input" placeholder="Qual tarefa você deseja iniciar?" v-model="descricao" />
      </div>
      <div class="column">
        <Temporizador @aoFinalizarTarefa="salvarTarefa" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Temporizador from './Temporizador.vue'

export default defineComponent({
  name: "Formulario",
  emits: ['aoSalvarTarefa'],
  components: {
    Temporizador
  },
  data() {
    return {
      descricao: '' as string
    }
  },
  methods: {
    salvarTarefa(tempoEmSegundos: number): void {
      this.$emit('aoSalvarTarefa', {
        duracaoEmSegundos: tempoEmSegundos,
        descricao: this.descricao
      })
      this.descricao = ''
    }
  }
});
</script>
<style>
.button {
  margin-left: 8px;
}

.box {
  background-color: var(--bg-primario);
  color: var(--texto-primario);
}
</style>
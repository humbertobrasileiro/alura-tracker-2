<template>
  <section>
    <router-link to="/projetos/novo" class="button">
      <span class="icon is-small">
        <i class="fas fa-plus"></i>
      </span>
      <span>Novo projeto</span>
    </router-link>
    <table class="table is-fullwidth">
      <thead>
        <tr>
          <th>ID</th>
          <th>Nome</th>
          <th>Ações</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="projeto in projetos" :key="projeto.id">
          <td>{{ projeto.id }}</td>
          <td>{{ projeto.nome }}</td>
          <td>
            <router-link :to="`/projetos/${projeto.id}`" class="button">
              <span class="icon is-small">
                <i class="fas fa-pencil-alt"></i>
              </span>
            </router-link>
            <button class="button ml-2 is-danger" @click="excluir(projeto.id)">
              <span class="icon is-small">
                <i class="fas fa-trash"></i>
              </span>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script lang="ts">
import { computed, defineComponent } from 'vue';
import { useStoreProjeto } from '@/store/projeto-store';
import { EXCLUIR_PROJETO } from '@/store/tipo-mutacoes';

export default defineComponent({
  name: 'ListaProjetos',
  setup() {
    const storeProjeto = useStoreProjeto();
    const projetos = computed(() => storeProjeto.state.projetos);

    const excluir = (id: string) => {
      storeProjeto.commit(EXCLUIR_PROJETO, id);
    };

    return {
      storeProjeto,
      projetos,
      excluir
    }
  }
})
</script>

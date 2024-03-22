<template>
  <main class="main-content">
    <YourList :ingredientes="ingredientes" />

    <KeepAlive include="SelectIngredients">
      <SelectIngredients
        v-if="conteudo === 'SelectIngredients'"
        @adicionar-ingrediente="adicionarIngrediente"
        @remover-ingrediente="removerIngrediente"
        @buscar-receitas="navegar('ShowRecipes')"
      />

      <ShowRecipes
        v-else-if="conteudo === 'ShowRecipes'"
        :ingredientes="ingredientes"
        @editar-ingredientes="navegar('SelectIngredients')"
      />
    </KeepAlive>
  </main>
</template>

<script lang="ts">
import SelectIngredients from "./SelectIngredients.vue";
import ShowRecipes from "./ShowRecipes.vue";
import YourList from "./YourList.vue";

type Page = "SelectIngredients" | "ShowRecipes";

export default {
  data() {
    return {
      ingredientes: [] as string[],
      conteudo: "SelectIngredients" as Page,
    };
  },

  components: {
    SelectIngredients,
    YourList,
    ShowRecipes,
  },

  methods: {
    adicionarIngrediente(ingrediente: string) {
      this.ingredientes.push(ingrediente);
    },
    removerIngrediente(ingrediente: string) {
      // this.ingredientes = this.ingredientes.filter(iLista => ingrediente !== iLista);
      this.ingredientes.splice(this.ingredientes.indexOf(ingrediente), 1);
    },
    navegar(page: Page) {
      this.conteudo = page;
    },
  },

  // if we use Composition API, it would be this way:
  // setup() {
  //   const ingredientes = ref<string[]>([]);

  //   function adicionarIngrediente(ingrediente: string) {
  //     ingredientes.value.push(ingrediente)
  //   }
  //   function removerIngrediente(ingrediente: string) {
  //     ingredientes.value = ingredientes.value.filter(iLista => ingrediente !== iLista);
  //   }

  //   return {
  //     ingredientes,
  //     adicionarIngrediente,
  //     removerIngrediente
  //   }
  // },
  // components: { SelecionarIngredientes, SuaLista },

  // we have the <script setup> too, that could be used to make our code simpler and smaller
  // the <script setup> turn our script into a already existing setup, without needed to add the setup attribute
};
</script>

<style scoped>
.main-content {
  padding: 6.5rem 7.5rem;
  border-radius: 3.75rem 3.75rem 0rem 0rem;
  background: var(--creme, #fffaf3);
  color: var(--cinza, #444);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5rem;
}

@media only screen and (max-width: 1300px) {
  .main-content {
    padding: 5rem 3.75rem;
    gap: 3.5rem;
  }
}

@media only screen and (max-width: 767px) {
  .main-content {
    padding: 4rem 1.5rem;
    gap: 4rem;
  }
}
</style>

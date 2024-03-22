<template>
  <section class="show-recipes">
    <h1 class="header recipes-title">Receitas</h1>
    <p class="paragrafo-lg found-results">
      Resultados encontrados: {{ receitasResultado.length }}
    </p>
    <div v-if="receitasResultado.length" class="recipes-wrapper">
      <p class="paragraph-lg info">
        Veja as opções de receitas que encontramos com os ingredientes que você
        tem por aí!
      </p>
      <ul class="recipes">
        <li v-for="receita in receitasResultado" :key="receita.nome">
          <RecipeCard :receita="receita" />
        </li>
      </ul>
    </div>
    <div v-else class="recipes-empty">
      <p class="paragrafo-lg recipes-empty__info">
        Ops, não encontramos resultados para sua combinação. Vamos tentar de
        novo?
      </p>
      <img
        src="../assets/images/no-recipes.png"
        alt="Desenho de um ovo quebrado. A gema tem um rosto com uma expressão triste."
      />
    </div>
    <MainButton text="Editar lista" @click="$emit('editarIngredientes')" />
  </section>
</template>

<script lang="ts">
import { itensDeLista1EstaoEmLista2 } from "@/operations/lists";
import { getRecipes } from "@/http/index";
import type IRecipe from "@/interfaces/IRecipe";
import RecipeCard from "./RecipeCard.vue";
import MainButton from "./MainButton.vue";
import type { PropType } from "vue";

export default {
  components: {
    RecipeCard,
    MainButton,
  },

  props: {
    ingredientes: {
      type: Array as PropType<string[]>,
      required: true,
    },
  },

  data() {
    return {
      receitasResultado: [] as IRecipe[],
    };
  },

  async created() {
    const receitas = await getRecipes();

    this.receitasResultado = receitas.filter((receita) => {
      const possoFazerReceita = itensDeLista1EstaoEmLista2(
        receita.ingredientes,
        this.ingredientes
      );
      return possoFazerReceita;
    });
  },

  emits: ["editarIngredientes"],
};
</script>

<style scoped>
.show-recipes {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

.recipes-title {
  color: var(--verde-medio, #3d6d4a);
  margin-bottom: 1.5rem;
}

.found-results {
  color: var(--verde-medio, #3d6d4a);
  margin-bottom: 0.5rem;
}

.recipes-wrapper {
  margin-bottom: 3.5rem;
}

.info {
  margin-bottom: 2rem;
}

.recipes {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.recipes-empty {
  margin-bottom: 2rem;
}

.recipes-empty__info {
  margin-bottom: 0.5rem;
}

@media only screen and (max-width: 767px) {
  .recipes-wrapper {
    margin-bottom: 2rem;
  }
}
</style>

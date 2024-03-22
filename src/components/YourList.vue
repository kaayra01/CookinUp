<template>
  <section>
    <span class="subtitle-lg your-list-text"> Sua lista:</span>

    <ul v-if="ingredientes.length" class="your-list-ingredients">
      <li v-for="ingrediente in ingredientes" :key="ingrediente">
        <Tag :text="ingrediente" active />
      </li>
    </ul>

    <p v-else class="paragraph your-list-empty">
      <img
        src="../assets/images/icons/empty-list.svg"
        alt="Ícone de pesquisa"
      />
      Sua lista está vazia, selecione ingredientes para iniciar.
    </p>
  </section>
  <!-- <button class="clear-button" @click="limparIngredientes()">Limpar</button> -->
</template>

<script lang="ts">
import type { PropType } from "vue";
import Tag from "./Tag.vue";

export default {
  components: {
    Tag,
  },

  props: {
    ingredientes: { type: Array as PropType<string[]>, required: true },
  },

  // methods: {
  //   limparIngredientes() {
  //     while (this.ingredientes.length > 0) {
  //       this.ingredientes.pop();
  //     }
  //   },
  // },
};
</script>

<style scoped>
.your-list-text {
  color: var(--coral, #f0633c);
  display: block;
  text-align: center;
  margin-bottom: 1.5rem;
}

.your-list-ingredients {
  display: flex;
  justify-content: center;
  gap: 1rem 1.5rem;
  flex-wrap: wrap;
}

.your-list-empty {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  gap: 0.25rem;
  color: var(--coral, #f0633c);
  text-align: center;
}

.clear-button {
  width: 10rem;
  padding: 0.5rem 1rem;
  border-radius: 2rem;
  font-weight: 700;
  color: var(--creme, #fffaf3);
  background: var(--coral, #f0633c);
  box-shadow: 4px 4px 15px 0px rgba(255, 115, 76, 0.25);
  cursor: pointer;
  transition: 0.2s;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>

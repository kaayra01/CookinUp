<template>
  <button class="ingredient" @click="aoClicar()" :aria-pressed="selecionado">
    <Tag :text="ingrediente" :active="selecionado" />
  </button>
</template>

<script lang="ts">
import Tag from "./Tag.vue";

export default {
  components: {
    Tag,
  },

  props: {
    ingrediente: {
      type: String,
      required: true,
    },
  },

  data() {
    return {
      selecionado: false,
    };
  },

  methods: {
    aoClicar() {
      this.selecionado = !this.selecionado;

      if (this.selecionado) {
        this.$emit("adicionarIngrediente", this.ingrediente);
      } else {
        this.$emit("removerIngrediente", this.ingrediente);
      }
    },
  },

  emits: ["adicionarIngrediente", "removerIngrediente"],
};
</script>

<style scoped>
.ingredient {
  cursor: pointer;
}
</style>

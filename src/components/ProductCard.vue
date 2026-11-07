<script>
// Cada produto é exibido pelo mesmo componente.
// O pai informa nome, preço, imagem e descrição por props.
export default {
  name: 'ProductCard',
  props: {
    nome: { type: String, required: true },
    preco: { type: Number, required: true },
    imagem: { type: String, required: true },
    descricao: { type: String, required: true }
  },
  emits: ['adicionar'],
  computed: {
    precoFormatado() {
      return this.preco.toLocaleString('pt-BR', {
        style: 'currency', currency: 'BRL'
      });
    }
  }
};
</script>

<template>
  <article class="produto">
    <img :src="imagem" :alt="'Imagem de ' + nome">
    <h3>{{ nome }}</h3>
    <p class="descricao">{{ descricao }}</p>
    <p class="preco">{{ precoFormatado }}</p>
    <!-- $emit informa ao componente pai que o botão foi clicado. -->
    <button type="button" @click="$emit('adicionar')">Adicionar ao Carrinho</button>
  </article>
</template>

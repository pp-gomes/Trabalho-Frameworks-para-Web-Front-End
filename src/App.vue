<script>
import ProductCard from './components/ProductCard.vue';

// O App é o componente pai. Ele guarda os produtos, a busca e o carrinho.
export default {
  components: { ProductCard },
  data() {
    return {
      busca: '',
      itensCarrinho: 0,
      produtos: [
        { id: 1, nome: 'Mouse USB', preco: 39.90, imagem: '/img/mouse.svg', descricao: 'Mouse simples para computador.' },
        { id: 2, nome: 'Teclado', preco: 69.90, imagem: '/img/teclado.svg', descricao: 'Teclado para estudar e trabalhar.' },
        { id: 3, nome: 'Fone de Ouvido', preco: 89.90, imagem: '/img/fone.svg', descricao: 'Fone para músicas e videoaulas.' },
        { id: 4, nome: 'Monitor', preco: 599.90, imagem: '/img/monitor.svg', descricao: 'Monitor para o dia a dia.' }
      ]
    };
  },
  computed: {
    produtosFiltrados() {
      const texto = this.busca.toLowerCase().trim();
      return this.produtos.filter(produto =>
        produto.nome.toLowerCase().includes(texto)
      );
    }
  },
  methods: {
    adicionarAoCarrinho() {
      this.itensCarrinho += 1;
    }
  }
};
</script>

<template>
  <header class="cabecalho">
    <div class="cabecalho-conteudo">
      <div>
        <h1>Loja de Informática</h1>
        <p class="subtitulo">Projeto escolar feito com Vue.js</p>
      </div>
      <div class="carrinho" aria-live="polite">
        🛒 Itens no carrinho: {{ itensCarrinho }}
      </div>
    </div>
  </header>

  <main class="conteudo">
    <h2>Nossos produtos</h2>
    <div class="busca-container">
      <label for="busca">Pesquisar produto</label>
      <input id="busca" type="search" v-model="busca" placeholder="Digite o nome do produto...">
    </div>

    <div v-if="produtosFiltrados.length > 0" class="grade-produtos">
      <ProductCard
        v-for="produto in produtosFiltrados"
        :key="produto.id"
        :nome="produto.nome"
        :preco="produto.preco"
        :imagem="produto.imagem"
        :descricao="produto.descricao"
        @adicionar="adicionarAoCarrinho"
      />
    </div>
    <p v-else class="sem-resultados">Nenhum produto encontrado. Tente outra pesquisa.</p>
  </main>

  <footer class="rodape">Trabalho prático de Frameworks para Web Front-End</footer>
</template>

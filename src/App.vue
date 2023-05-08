<script setup>
import { ref, computed } from 'vue'
const produtos = ref([
  {
    id: 1,
    nome: 'Camiseta',
    quantidade: 0,
    preco: 49.90
  },
  {
    id: 2,
    nome: 'Calça',
    quantidade: 0,
    preco: 99.90
  },
  {
    id: 3,
    nome: 'Meia',
    preco: 9.90,
    quantidade: 0
  },
  {
    id: 4,
    nome: 'Sapato',
    quantidade: 0,
    preco: 199.90
  },
  {
    id: 5,
    nome: 'Boné',
    preco: 29.90,
    quantidade: 0
  },
  {
    id: 6,
    nome: 'Óculos',
    quantidade: 0,
    preco: 99.90
  },
  {
    id: 7,
    nome: 'Relógio',
    quantidade: 0,
    preco: 299.90
  },
  {
    id: 8,
    nome: 'Bermuda',
    quantidade: 0,
    preco: 79.90
  },
  {
    id: 9,
    nome: 'Cueca',
    quantidade: 0,
    preco: 19.90
  },
  {
    id: 10,
    nome: 'Calcinha',
    preco: 2.90,
    quantidade: 0
  },
  {
    id: 11,
    nome: 'Latex',
    preco: 5.30,
    quantidade: 0
  },
  {
    id: 12,
    nome: 'Calça cargo',
    preco: 50.90,
    quantidade: 0
  }
]
)
// Carrinho
const carrinho = ref({
  items: [],
  total: 0
})
// Valor total 
let valorTotal = ref(0)
// Função adicionar carrinho
function adicionarCarrinho(produto) {
  carrinho.value.items.push({
    id: produto.id,
    nome: produto.nome,
    preco: produto.preco,
    quantidade: produto.quantidade,
    total: produto.preco * produto.quantidade
  });
  carrinho.value.total += produto.preco * produto.quantidade
}
// Função adicionar item
function mais(index) {
  produtos.value[index].quantidade++
  const pos = carrinho.value.items.indexOf(carrinho.value.items.find(c => c.id === produtos.value[index].id))
  if (pos != -1) {
    carrinho.value.total -= carrinho.value.items[pos].total
    carrinho.value.items[pos].total = ++carrinho.value.items[pos].quantidade * carrinho.value.items[pos].preco
    carrinho.value.total += carrinho.value.items[pos].total
  }
}
function menos(index) {
  produtos.value[index].quantidade--
  const pos = carrinho.value.items.indexOf(carrinho.value.items.find(c => c.id === produtos.value[index].id))
  if (pos != +1) {
    carrinho.value.total -= carrinho.value.items[pos].total
    carrinho.value.items[pos].total = --carrinho.value.items[pos].quantidade * carrinho.value.items[pos].preco
    carrinho.value.total += carrinho.value.items[pos].total
  }
}
// Limpar carrinho
function limparCarrinho(){
carrinho.value.items = 0
carrinho.value.total = 0
}
// computed mudar cor
const mudarCor = computed(() => {
    return 
}
)
</script>

<template>
  <div class="container">
    <!-- Button modal -->
    <button type="button" class="btn btn-primary p-3 mt-2 " data-bs-toggle="modal" data-bs-target="#exampleModal">
      Carrinho
    </button>
    <!-- Modal -->
    <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="exampleModalLabel">Modal title</h1>
            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <div class="modal-body">
            <p>{{ carrinho }}</p>
            <p>{{ valorTotal }}</p>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Fechar</button>
            <button @click="limparCarrinho" type="button" class="btn btn-warning">Limpar carrinho</button>
          </div>
        </div>
      </div>
    </div>

    <div class="row">

      <!-- div que tem o v-for -->

      <div v-for="(produto, index) in produtos" :key="produto.id" class="col-3">

        <div class="tema">
          <b> {{ produto.id }} - {{ produto.nome }} </b>
          <br>
          <h6>Preço: {{ produto.preco }}</h6>
          <h6>Quantidade: {{ produto.quantidade }}</h6>

          <button type="button" @click="menos(index)" class="btn bg-white p-1 h-r">-</button>
          <button type="button" @click="mais(index)" class="btn bg-white p-1 ml-b h-g">+</button>
          <button type="button" @click="adicionarCarrinho(produto)" class="btn bg-white p-1 ml-b h-g">Adicionar</button>
        </div>
      </div>
      <!-- FIM DIV FOR-V -->
    </div>
    <!-- FIM DIV.CONTAINER -->
  </div>
</template>


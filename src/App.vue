<template>
 <div>
    <h2>Produtos</h2>
    <div v-for="produto in produtos" :key="produto.id" class="product">
      <span>{{ produto.nome }} - R$ {{ produto.preco }}</span>
      <button @click="adicionarProduto(produto)">Adicionar ao Carrinho</button>
    </div>

    <h2>Ver Carrinho</h2>
    <button @click="verCarrinho">Ver Carrinho</button>

    <div v-if="mostrarCarrinho" class="cart">
      <h3>Itens no Carrinho</h3>
      <div v-for="item in carrinho.items" :key="item.id" class="product">
        <span>{{ item.nome }} - R$ {{ item.preco }}</span>
        <input type="number" min="1" v-model="item.quantidade" @input="atualizarValorTotal(item)">
        <button @click="removerItem(item)">Remover</button>
      </div>
      <div class="total">Total: R$ {{ carrinho.total }}</div>
    </div>
  </div>
</template>


<script>
export default {
  data() {
    return {
      produtos: [
        {
          id: 1,
          nome: 'Camiseta',
          preco: 49.90
        },
        {
          id: 2,
          nome: 'Calça',
          preco: 99.90
        },
        {
          id: 3,
          nome: 'Meia',
          preco: 9.90
        },
        {
          id: 4,
          nome: 'Sapato',
          preco: 199.90
        },
        {
          id: 5,
          nome: 'Boné',
          preco: 29.90
        },
        {
          id: 6,
          nome: 'Óculos',
          preco: 99.90
        },
        {
          id: 7,
          nome: 'Relógio',
          preco: 299.90
        },
        {
          id: 8,
          nome: 'Bermuda',
          preco: 79.90
        },
        {
          id: 9,
          nome: 'Cueca',
          preco: 19.90
        },
        {
          id: 10,
          nome: 'Meia',
          preco: 9.90
        }
      ],
      carrinho: {
        items: [],
        total: 0
      },
      mostrarCarrinho: false
    };
  },
  methods: {
    adicionarProduto(produto) {
      const itemExistente = this.carrinho.items.find(item => item.id === produto.id);
      if (itemExistente) {
        itemExistente.quantidade++;
        itemExistente.valorTotal = itemExistente.preco * itemExistente.quantidade;
      } else {
        const novoItem = {
          id: produto.id,
          nome: produto.nome,
          preco: produto.preco,
          quantidade: 1,
          valorTotal: produto.preco
        };
        this.carrinho.items.push(novoItem);
      }
      this.atualizarTotal();
    },
    removerItem(item) {
      const index = this.carrinho.items.indexOf(item);
      if (index > -1) {
        this.carrinho.items.splice(index, 1);
        this.atualizarTotal();
      }
    },
    atualizarValorTotal(item) {
      item.valorTotal = item.preco * item.quantidade;
      this.atualizarTotal();
    },
    atualizarTotal() {
      this.carrinho.total = this.carrinho.items.reduce((total, item) => total + item.valorTotal, 0);
    },
    verCarrinho() {
      this.mostrarCarrinho = !this.mostrarCarrinho;
    }
  }
};
</script>

<style scoped>
  body {
    background: linear-gradient(to bottom right, #00f098, #f01607);
  }
  .product {
    margin-bottom: 10px;
    padding: 10px;
    border: 1px solid #3fee39ce;
    border-radius: 5px;
    background-color: #290285;
    color: #ffffff;
  }
  .product span {
    display: inline-block;
    margin-right: 10px;
    font-weight: bold;
  }
  .product button {
    background-color: #4CAF50;
    border: none;
    color: rgb(255, 255, 255);
    padding: 8px 16px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
  }
  .cart {
    margin-top: 20px;
    padding: 10px;
    border: 1px solid #5e5e5e;
    border-radius: 5px;
    background-color: #878888;
    color: #000000;
  }
  .cart h3 {
    margin-top: 0;
  }
  .cart .product {
    margin-bottom: 10px;
    padding: 10px;
    border: 1px solid #4e4e4e;
    border-radius: 5px;
    background-color: #474747;
  }
  .cart .product span {
    display: inline-block;
    margin-right: 10px;
    font-weight: bold;
  }
  .cart .product input {
    width: 60px;
    margin-right: 10px;
    text-align: center;
    border: none;
    border-bottom: 1px solid #5c15b9;
    font-size: 16px;
  }
  .cart .product button {
    background-color: #ff1403;
    border: none;
    color: white;
    padding: 8px 16px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
  }
  .cart .total {
    margin-top: 10px;
    font-weight: bold;
    text-align: right;
  }
  .cart .total::before {
    content: "Total: ";
    
  }
  button {
    background-color: #4caf54;
    border: none;
    color: white;
    padding: 8px 16px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    border-radius: 5px;
    cursor: pointer;
    display: flex ;
  }
  button:hover {
    background-color: #3e8e41;
  }
  h2 {
    font-size: 28px;
    margin-bottom: 10px;
    color: #ff00d4;
  }
  h3 {
    font-size: 24px;
    margin-bottom: 10px;
    color: rgb(0, 0, 0);
  }
  .body{
    background-color: rgb(255, 255, 255);
  }
</style>
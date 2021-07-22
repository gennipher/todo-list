<template>
  <div class="container">
    <h1 class="text-center mt-5">Supermercado Todo List</h1>
    <h3 class="text-center">Jennifer Omena</h3>

    <div class="d-flex">
      <input v-model="produto" type="text" placeholder="Produto" class="form-control mt-5 border border-info" @keydown.enter="adicionar">
      <button @click="adicionar" class="btn btn-info rounded-0 mt-5">ADICIONAR</button>
    </div>

    <table class="table table-borderless mt-5">
      <thead>
        <tr>
          <th scope="col">PRODUTO</th>
          <th scope="col" class="text-center"></th>
          <th scope="col" class="text-center"></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(produto, index) in produtos" :key="index">
          <td>{{ produto.nome }}</td>
          <td>
            <div class="text-center" @click="editar(index)">
              <span class="fa fa-pen" style="color:deepskyblue"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deletar(index)">
              <span class="fa fa-trash" style="color:deepskyblue"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>

  </div>
</template>

<script>
export default {
  name: 'TodoList',
  props: {
    msg: String
  },

  data () {
    return {
      produto: '',
      produtoEditado: null,
      produtos: [
        { id: 1, nome: 'Açúcar' },
        { id: 2, nome: 'Margarina' },
        { id: 3, nome: 'Café' },
        { id: 4, nome: 'Tomate' },
      ]
    }
  },

  methods: {
    adicionar() {
      if (!this.produto) {
        return
      }

      let nomeProduto = {
        nome: this.produto,
        id: this.produtos.length + 1
      }

      if (this.produtoEditado  == null) {
        this.produtos.push(nomeProduto)
        this.produto = ''
      } else {
        this.produtos[this.produtoEditado].nome = this.produto
        this.produtoEditado = null
      }
    },

    editar(index) {
      this.produto = this.produtos[index].nome
      this.produtoEditado = index
    },

    deletar(index) {
      this.produtos.splice(index, 1)
    }
  }
}
</script>
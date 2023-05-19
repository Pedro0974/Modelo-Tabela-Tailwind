<template>
  <div class="container-modelo-tabela">
    <table class="container-tabela">
      <thead class="cabecalho-tabela">
        <tr>
          <th scope="col" class="p-4">
            <div class="flex items-center">
              <input id="checkbox-all" type="checkbox"
                class="checkbox">
              <label for="checkbox-all" class="sr-only">checkbox</label>
            </div>
          </th>
          <th scope="col" class="px-6 py-3">
            #
          </th>
          <th scope="col" class="px-6 py-3">
            Nome/Razão
          </th>
          <th scope="col" class="px-6 py-3">
            Tipo
          </th>
          <th scope="col" class="px-6 py-3">
            Status
          </th>
          <th scope="col" class="px-6 py-3">
            Ações
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(pessoa, index) in listaPessoas"
          :key="index"
          class="escopo-tabela">
          <td class="w-4 p-4">
            <div class="flex items-center">
              <input id="checkbox-table-1" type="checkbox"
                class="checkbox">
              <label for="checkbox-table-1" class="sr-only">checkbox</label>
            </div>
          </td>
          <th scope="row" class="px-6 py-4 font-medium text-gray-900 whitespace-nowrap dark:text-white">
            {{ index + 1 }}
          </th>
          <td class="px-6 py-4">
            {{ pessoa.nome_razao }}
          </td>
          <template v-if="pessoa.pessoa_fisica !== null">
            <td class="px-6 py-4">
              <i class="fas fa-user"></i>
            </td>
          </template>
          <template v-if="pessoa.pessoa_juridica !== null">
            <td class="px-6 py-4">
              <i class="fas fa-factory"></i>
            </td>
          </template>
          <template v-if="pessoa.pessoa_fisica !== null">
            <tempalte v-if="pessoa.pessoa_fisica.ativo === true">
              <td class="px-6 py-4">
                <i class="fas fa-cicle-check"></i>
              </td>
            </tempalte>
            <tempalte v-if="pessoa.pessoa_fisica.ativo === false">
              <td class="px-6 py-4">
                <i class="fas fa-circle-close"></i>
              </td>
            </tempalte>
          </template>

          <template v-if="pessoa.pessoa_juridica !== null">
            <tempalte v-if="pessoa.pessoa_juridica.ativo === true">
              <td class="px-6 py-4">
                <i class="fas fa-cicle-check"></i>
              </td>
            </tempalte>
            <tempalte v-if="pessoa.pessoa_juridica.ativo === false">
              <td class="px-6 py-4">
                <i class="fas fa-circle-close"></i>
              </td>
            </tempalte>
          </template>

          <td class="px-6 py-4">
            <a href="#" class="font-medium text-blue-600 dark:text-blue-500 hover:underline">Edit</a>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'HelloWorld',
  data() {
    return {
      error: [],
      listaPessoas: [],
    }
  },

  created() {
    this.getListaPessoas()
  },

  methods: {
    async getListaPessoas() {

      const token = '9d66326f76faa71872b0ebec30f27e4e20539e7b'

      axios.get('http://orolglass.managerglass:8000/api/v1/pessoas/', {
        headers: {
          'Authorization': `Token ${token}`
        }
      })
        .then(response => {
          this.listaPessoas = response.data
          console.log(response.data)
        })
        .catch(error => {
          console.log(error);
        })

    }
  }
}
</script>

<style lang="scss">
.container-modelo-tabela {
  @apply relative overflow-x-auto shadow-md sm:rounded-lg;
}

.container-tabela{
  @apply w-full text-sm text-left text-gray-500 dark:text-gray-400;
}

.cabecalho-tabela {
  @apply text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400;
}

.checkbox {
  @apply w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 dark:focus:ring-blue-600 dark:ring-offset-gray-800 dark:focus:ring-offset-gray-800 focus:ring-2 dark:bg-gray-700 dark:border-gray-600;
}

.escopo-tabela {
  @apply bg-white border-b dark:bg-gray-800 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-600;
}
</style>

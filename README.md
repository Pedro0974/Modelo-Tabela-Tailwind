# Model Table in Vuejs end TailwindCSS

### Change Urls in HelloWorld Component
```
async getListaPessoas() {

      const token = 'TOKEN-DA-SUA-API-SE-REQUER-AUTORIZAÇÃO'

      axios.get('URL-DA-SUA-API-LISTA-PESSOA', {
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
```

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```



### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

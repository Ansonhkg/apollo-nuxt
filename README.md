# How to add Apollo to your Nuxt application
![landing]

## Install dependencies by Nuxt community https://github.com/nuxt-community/apollo-module
```
yarn add @nuxtjs/apollo graphql-tag apollo-link-http
```

## nuxt.config.js

Add the following before the last closing bracket
```javascript
  modules: ['@nuxtjs/apollo'],
  apollo: {
    clientConfigs: {
      default: '~/apollo/client-configs/default.js'
    }
  }
```

## ~/apollo/client-configs/default.js
```javascript
import { HttpLink } from 'apollo-link-http'
import { InMemoryCache } from 'apollo-cache-inmemory'

// Replace this with your project's endpoint
const API = 'http://localhost:4000/graphql'

export default () => ({
  link: new HttpLink({ uri: API }),
  cache: new InMemoryCache(),
  defaultHttpLink: false
})

```

## Vue Component sample

#### template
```html
<template>
  <section class="container">
    {{ books }}
  </section>
</template>
```

#### script
```js
import gql from 'graphql-tag'

const getBooksQuery = gql`
    {
        books{
            name
            id
            author{
                name
                age
            }
        }
    }
`

export default {
  data(){
    return{
      loading: 0,
    }
  },
  apollo:{
    $loadingKey: 'loading',
    books: {
      query: getBooksQuery
    }
  }
}
```

# ApolloQuery Component Sample
index.vue

```html
<template>
  <ApolloQuery
  :query="require('../queries/books.gql')"
>
  <template v-slot="{ result: { error, data }, isLoading }">
    <!-- Loading -->
    <div v-if="isLoading" class="loading apollo">Loading...</div>

    <!-- Error -->
    <div v-else-if="error" class="error apollo">An error occurred</div>

    <!-- Result -->
    <div v-else-if="data" class="result apollo">{{ data }}</div>

    <!-- No result -->
    <div v-else class="no-result apollo">No result :(</div>
  </template>
</ApolloQuery>
</template>
```

## ./queries/getBooks.gql
```sql
query getBooks{
    books{
        name
        id
        author{
            name
            age
        }
    }
}
```

# Apollo Mutation
```js
  handleSubmit(){
      this.$apollo.mutate({
          mutation: addBook,
          variables:{
              name: this.name,
              genre: this.genre,
              authorId: this.authorId
          }
      }).then(mutationResult => {
          this.$apollo.queries.books.refresh() // Refetch books query when a new book is added
          console.log("Book added!")
      })
  }
```

[landing]: https://i.gyazo.com/a016457c1796a5768655714008df436e.gif
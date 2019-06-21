# How to add Apollo to your Nuxt application

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

template
```html
<template>
  <section class="container">
    {{ books }}
  </section>
</template>
```

script
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
  apollo:{
    books: {
      query: getBooksQuery
    }
  }
}
```
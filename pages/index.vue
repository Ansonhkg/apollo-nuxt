<template>
  <section class="container">
    {{ books }}
  </section>
</template>

<script>
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
</script>
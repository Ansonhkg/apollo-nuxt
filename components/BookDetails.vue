<template>
  <ApolloQuery
  :query="require('../queries/getBook.gql')"
  :variables="{ bookId }"
>
  <template v-slot="{ result: { error, data }, isLoading }">
    <!-- Loading -->
    <div v-if="isLoading" class="loading apollo">Loading...</div>

    <!-- Error -->
    <div v-else-if="error" class="error apollo">An error occurred</div>

    <!-- Result -->
    <div v-else-if="data" class="result apollo">
        <h2>{{ data.book.name }}</h2>
        <p>{{ data.book.genre }}</p>
        <p>{{ data.book.author.name }}</p>
        <p>All books by this author</p>
        <ul className="other-books">
            <li v-for="book in data.book.author.books" :key="book.id">
                {{ book.name }}
            </li>
        </ul>
    </div>

    <!-- No result -->
    <div v-else class="no-result apollo">No result :(</div>
  </template>

</ApolloQuery>
</template>

<script>
export default {
    props:{
        bookId:{
            type: String || Number
        }
    },
}
</script>

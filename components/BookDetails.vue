<template>
  <ApolloQuery id="book-details"
  :query="require('../queries/getBook.gql')"
  :variables="{ bookId }"
>
  <template v-slot="{ result: { error, data }, isLoading }">
    <!-- Loading -->
    <div v-if="isLoading" class="loading apollo">Loading...</div>

    <!-- Error -->
    <div v-else-if="error" class="error apollo">An error occurred</div>

    <!-- Result -->
    <div v-else-if="data.book != null" class="result apollo">
        <h2>{{ data.book.name }}</h2>
        <p>{{ data.book.genre }}</p>
        <p>{{ data.book.author.name }} : {{ data.book.author.id }}</p>
        <p>All books by this author</p>
        <ul className="other-books">
            <li v-for="book in data.book.author.books" :key="book.id">
                {{ book.name }}
            </li>
        </ul>
    </div>

    <!-- No result -->
    <div v-else class="no-result apollo">Click a book to see details..</div>
  </template>
</ApolloQuery>
</template>

<script>
export default {
    props:{
        bookId:{
            type: String || Number,
        }
    }
}
</script>

<style>
#book-details{
  position:fixed;
  top: 0;
  right: 0;
  width: 40%;
  height: 100%;
  background-color:#AD1457;
  padding: 30px;
  overflow:auto;
  box-shadow: -2px -3px 5px rgba(0,0,0,0.3);
  box-sizing: border-box;
  color: #fff;
}
</style>

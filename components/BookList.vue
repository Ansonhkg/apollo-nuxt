<template>
  <ApolloQuery
  :query="require('../queries/getBooks.gql')"
>
  <template v-slot="{ result: { error, data }, isLoading }">
    <!-- Loading -->
    <div v-if="isLoading" class="loading apollo">Loading...</div>

    <!-- Error -->
    <div v-else-if="error" class="error apollo">An error occurred</div>

    <!-- Result -->
    <div v-else-if="data" class="result apollo">
      <ul>
        <li @click="setSelected(book.id)" v-for="book in data.books" :key="book.id">
          {{ book.name }} - {{ book.author.name }} ({{book.author.age}})
        </li>
      </ul>
    </div>

    <!-- No result -->
    <div v-else class="no-result apollo">No result :(</div>
  </template>

    <BookDetails :bookId="selected"/>
</ApolloQuery>
</template>

<script>
import BookDetails from '~/components/BookDetails'

export default {
    components:{
        BookDetails
    },
    data(){
        return{
            selected: null
        }
    },
    methods:{
        setSelected(bookId){
            this.selected = bookId
        }
    }

}
</script>
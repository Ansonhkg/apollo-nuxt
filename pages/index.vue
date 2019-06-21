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

<script>

export default {

}
</script>
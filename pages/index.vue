<template>
  <div id="main">
    <h2>My Ninja Book List</h2>
    <BookList/>
    <AddBook/>
  </div>
</template>

<script>
import BookList from '~/components/BookList'
import AddBook from '~/components/AddBook'

export default {
  components:{
    BookList,
    AddBook,
  }
}
</script>
<template>
  <div id="main">
    <h2>My Ninja Book List</h2>
    <BookList/>
  </div>
</template>

<script>
import BookList from '~/components/BookList'

export default {
  components:{
    BookList
  }
}
</script>
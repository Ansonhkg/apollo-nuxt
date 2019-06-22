<template>
    <form id="add-book" @submit.prevent="handleSubmit">
        <div class="field">
            <label>Book name:</label>
            <input type="text" v-model="name"/>
        </div>

        <div class="field">
            <label>Genre:</label>
            <input type="text" v-model="genre"/>
        </div>

        <div class="field">
            <label>Author:</label>
            <select v-model="authorId">
                <option>Select author</option>
                <option v-if="loading">Loading Authors..</option>
                <option v-else v-for="author in authors" :key="author.id" :value="author.id">
                    {{ author.name }}
                </option>
            </select>
        </div>

        <button type="submit">+</button>
    </form>
</template>

<script>
import getAuthors from '~/queries/getAuthors.gql'
import addBook from '~/queries/addBook.gql'
import getBooks from '~/queries/getBooks.gql'

export default {
    data(){
        return{
            loading: 0,

            // form state
            name: '',
            genre: '',
            authorId: '',
        }
    },
    methods:{
        handleSubmit(){
            console.log(this.$apollo.queries)
            this.$apollo.mutate({
                mutation: addBook,
                variables:{
                    name: this.name,
                    genre: this.genre,
                    authorId: this.authorId
                }
            }).then(mutationResult => {
                this.$apollo.queries.books.refresh()
                console.log("Book added!")
            })
        }
    },
    apollo:{
        authors:{
            $loadingKey: 'loading',
            query: getAuthors
        },
        books:{
            query: getBooks
        }
    }
}
</script>

<style>
#add-book{
    @apply border absolute pin-b pin-l m-2 p-2 rounded;
}
#add-book .field{
    display:grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 10px;
    @apply mt-2 mb-2;
}
#add-book label{
    text-align:right;
    padding:6px;
}
#add-book .field input, #add-book .field select{
    @apply border;
    box-sizing: border-box;
}
#add-book button{
    @apply rounded-full h-10 w-10 flex items-center justify-center bg-red-light text-3xl;
}
</style>

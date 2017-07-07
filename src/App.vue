<template>
  <div class="container">
    <div class="page-header">
      <h1>Vue.js 2 FireBase</h1>
    </div>

    <div class="panel panel-default">
      <div class="panel-heading">
        <h3>Add Book</h3>
      </div>
      <div class="panel-body">
        <form class="form-block" v-on:submit.prevent="addBook">
          <div class="form-group">
            <label for="bookTitle">Title: </label>
            <input type="text" id="bookTitle" class="form-control" v-model="newBook.title">
          </div>
           <div class="form-group">
            <label for="bookAuthor">Author: </label>
            <input type="text" id="bookAuthor" class="form-control" v-model="newBook.author">
          </div>
           <div class="form-group">
            <label for="bookUrl">URL: </label>
            <input type="text" id="bookUrl" class="form-control" v-model="newBook.url">
          </div>
          <input type="submit" class="btn btn-primary" value="Add Book">
        </form>
      </div>
    </div>

    <div class="panel panel-default">
      <div class="panel-heading">
        <h3>Books List</h3>
      </div>
      <div class="panel-body">
        <table class="table table-striped">
          <thead>
            <tr>
              <th>Title</th>
              <th>Author</th>
              <th>Delete</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="book in books">
              <td><a :href="book.url">{{ book.title }}</a></td>
              <td>{{ book.author }}</td>
              <td><span class="glyphicon glyphicon-trash" @click="removeBook(book)"></span></td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>

import Hello from './components/Hello.vue'

import Firebase from 'firebase'

let config = {
   apiKey: "AIzaSyB4WY1vQzL08RYruPncH6JBQBLHig1nFlg",
    authDomain: "vue-database-fd763.firebaseapp.com",
    databaseURL: "https://vue-database-fd763.firebaseio.com",
    projectId: "vue-database-fd763",
    storageBucket: "vue-database-fd763.appspot.com",
    messagingSenderId: "660283934835"
}

let app = Firebase.initializeApp(config);

let db = app.database();

let booksRef = db.ref('books');

export default {
   firebase : {
    books: booksRef
   },
   data() {
     return {
      newBook: {
        title: '',
        author: '',
        url: ''
      }
     }
   },
   methods:{
    addBook(){
      booksRef.push(this.newBook);
      this.newBook.title = '';
      this.newBook.author = '';
      this.newBook.url = '';
    },
    removeBook(book){
      booksRef.child(book['.key']).remove();
    }
   }
}
</script>

<style>

</style>

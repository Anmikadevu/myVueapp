<template>

  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-md-8 col-md-offset-2">
          <div class="panel panel-default">
            <div class="panel-heading"><h4 class="head"> List of users</h4></div>
            <div class="panel-body">
              <table class="table">
                <thead>

                </thead>
                <tbody>
                  <tr v-for="user in users">
                    <td><a v-on:click="select($event)" v-bind:id="user.id">{{user.name}}</a></td>
                   
                  </tr>

                </tbody>
              </table>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="middle">
      
      <ul>
        <h3>Title of the posts</h3>
        <li v-for="post in posts">

          <a v-on:click="selectPosts($event)" v-bind:id="post.id">{{post.title}}</a>
        </li>
      </ul>


    </div>
    <div class="right">

      <ul>
       
        <li v-for="postDetail in  postDetails"> <h2>Details of the post</h2> {{postDetail.body}}</li>
      </ul>


    </div>
  </div>



</template>
<script>
  import axios from 'axios';

  export default {
    name: 'app',
    data: function () {
      return {
        users: [],
        posts: [],
        postDetails:[]
      }
    },

    methods: {
      selectPosts : function (e) {

        console.log((e.currentTarget.id));
        var app = this;

        axios.get('https://jsonplaceholder.typicode.com/posts', {
          params: {
            id: e.currentTarget.id
          }
        })
          .then(function (response) {
            console.log(response.Data);
            let postDetails = response.data;
            console.log("postDetails", postDetails);
          
            app.postDetails = postDetails;
          })
          .catch(function (error) {
            console.log(error);
          });
        // console.log(posts);
      },


      select: function (e) {

        console.log((e.currentTarget.id));
        var app = this;

        axios.get('https://jsonplaceholder.typicode.com/posts', {
          params: {
            userId: e.currentTarget.id
          }
        })
          .then(function (response) {
            
            let posts = response.data;
            console.log(posts);
            app.posts = posts;
          })
          .catch(function (error) {
            console.log(error);
          });
       // console.log(posts);
      },

      getUsers: function () {

        var app = this;

        axios.get('https://jsonplaceholder.typicode.com/users')
          .then(function (response) {
            app.users = response.data;
          })
          .catch(function (error) {
            console.log(error.message);
          });

      },

    },

    created() {
      this.getUsers();
     
    },

  }


</script>
<style>
  @import 'App.css';
  /*#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }*/
</style>

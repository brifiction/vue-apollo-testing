<template>
  <div class="users-list">
    <h1>{{ msg }}</h1>
    <h2>List of users (via ApolloQuery)</h2>
    <!-- Apollo Query -->
    <ApolloQuery :query="require('./graphql/users.gql')">
      <!-- The result will automatically updated -->
      <template slot-scope="{ result: { data, loading } }">
        <!-- Some content -->
        <div v-if="loading">Loading...</div>
        <ul v-else>
          <li v-for="user of data.users" class="user">
            {{ user.name }}
          </li>
        </ul>
      </template>
    </ApolloQuery>
  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      users: [],
      user: null
    }
  },
  apollo: {
    user: gql`
      {
         user(id: 1) {
           name
           email
         }
      }
    `,
    users: gql`
      {
         users {
           name
           email
         }
      }
    `,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
}
</style>

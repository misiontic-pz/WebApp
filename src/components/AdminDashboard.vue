<template>
  <div id="AdminDashboard" class="container">
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Fecha</th>
          <th scope="col">Hora</th>
          <th scope="col">Origen</th>
          <th scope="col">Destino</th>
          <th scope="col">valor</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="transacction in transacctionByIdUser" :key="transacction.id">
          <td>{{ transacction.date.substring(0, 10) }}</td>
          <td>{{ transacction.date.substring(11, 19) }}</td>
          <td>{{ transacction.userIdOrigin }}</td>
          <td>{{ transacction.userIdDestiny }}</td>
          <td>${{ transacction.value }} COP</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import gql from "graphql-tag";

export default {
  name: "AdminDashboard",

  data: function () {
    return {
      username: "none",
      transacctionByIdUser: [],
    };
  },

  created: function () {
    this.username = this.$route.params.username;
  },

  apollo: {
    transacctionByIdUser: {
      query: gql`
        query ($transacctionByIdUserUserId: String!) {
          transacctionByIdUser(userId: $transacctionByIdUserUserId) {
            date
            id
            userIdDestiny
            userIdOrigin
            value
          }
        }
      `,
      variables() {
        return {
          transacctionByIdUserUserId: localStorage.getItem("user_id"),
        };
      },
    },
  },
};
</script>


<style>
#AdminDashboard {
  width: 100%;
  height: 120%;

  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

/* #AdminDashboard table {
  width: 50%;
  border-collapse: collapse;
  border: 1px solid rgba(0, 0, 0, 0.3);
  border-radius: 20px;
}

#AdminDashboard table td,
#AdminDashboard table th {
  border: 1px solid #ddd;
  padding: 8px;
}

#AdminDashboard table tr:nth-child(even) {
  background-color: #f2f2f2;
}

#AdminDashboard table tr:hover {
  background-color: #ddd;
}

#AdminDashboard table th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: left;
  background-color: crimson;
  color: white;
} */
</style>
<template>
   <div>
    <b-table striped hover :items="items" :fields="fields"></b-table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'breadcrumbs',
   mounted() {
       axios.get('http://localhost:3000/api/employees?filter=%7B%20%22where%22%3A%20%7B%20%22name%22%3A%20%7B%20%22inq%22%3A%5B%22saurav%22%2C%22utsav%22%5D%20%20%7D%20%7D%20%7D&access_token=123456')
       .then(response =>{
         console.log(response);
         this.items = response.data;
       })
       .catch(err =>{
         console.log(err);
       })
  },
  data () {
    return {
      fields: ['name', 'position', 'age'],
      items: []
    }
  }
}
</script>

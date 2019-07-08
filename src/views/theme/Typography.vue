<template>
  <div class="animated fadeIn">
    
   <b-row>
        <b-col md="6">
        <b-card>
          <div slot="header">
            <strong>Employee Form</strong>
          </div>

          <b-form>

          <b-form-group
            description="Let us know your full name."
            label="Enter your name"
            label-for="basicName"
            :label-cols="3"
            >
            <b-form-input id="basicName" type="text" autocomplete="name" v-model="name">{{name}}</b-form-input>
          </b-form-group>


           
        <b-form-group
            description="Let us know your position."
            label="Postion"
            label-for="position"
            :label-cols="3"
            >
            <b-form-input id="position" type="text" autocomplete="name" v-model="position">{{position}}</b-form-input>
          </b-form-group>


          <b-form-group
            description="Please enter your age"
            label="age Input"
            label-for="basicage"
            :label-cols="3"
            >
            <b-form-input id="basicAge" type="number" placeholder="Enter your age" autocomplete="age" v-model="age">{{age}}</b-form-input>
          </b-form-group>

        


          <div slot="footer">
            <b-button type="submit" size="sm" variant="primary" @click="save()"><i class="fa fa-dot-circle-o"></i> Submit</b-button>
            <b-button type="reset" size="sm" variant="danger"><i class="fa fa-ban"></i> Reset</b-button>
            <b-button type="reset" size="sm" variant="danger" @click="deleteData()"><i class="fa fa-dot"></i> Delete</b-button>
          </div>


          </b-form>
        </b-card>

      </b-col>
    </b-row>


  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'typography',

   mounted() {
       axios.get('http://localhost:3000/api/employees/5d1ebb6a807166135c4c2547?access_token=123456')
       .then(response =>{
         console.log(response);
         this.age  =  response.data.age;
         this.name = response.data.name;
         this.position = response.data.position;
         this.id_of_prevemp = response.data.id
       })
       .catch(err =>{
         console.log(err);
       })
  },
  data() {
            return {
               name : '',
               age : '',
               position: '',  
               id_of_prevemp : ''          
            }           
        },
  methods : {
       save() {
                 let name = this.name;
                 let age =  this.age;
                 let position = this.position;
                 console.log(this.name + this.age + this.position);
                  // e.preventDefault();
                let currentObj = this;
                axios.post('http://localhost:3000/api/employees?access_token=123456',
                 {
                    name: this.name,
                    age : this.age,
                    position :  this.position,
                })
                .then(function (response) {
                    console.log(response);
                })
                .catch(function (error) {
                    currentObj.output = error;
                });
             },

             deleteData: function() {
               console.log("id of prev emp is" + this.id_of_prevemp);
                axios.delete('http://localhost:3000/api/employees/deldata?id='+ this.id_of_prevemp + '&access_token=123456')
               .then(response => {
               console.log(response);
      });
    },
  }
  

  

}
</script>

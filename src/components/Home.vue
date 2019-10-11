<template>
  <v-container fluid>
   <v-row>
     <v-col>
<v-form :lazy-validation="lazy" ref="form" :v-model="valid">
  <v-row class="ml-2 mr-2">
 <v-text-field v-model="emailid" placeholder="Email ID" :rules="emailRules" outlined type="email" required>

    </v-text-field>
  </v-row>
    <v-row class="ml-2 mr-2">
    <v-text-field v-model="password" placeholder="Password" type="password" :rules="passwordRules" required
 outlined></v-text-field>

    </v-row>
    <v-row justify="center">
             <v-btn outlined @click="validate"> Start  </v-btn>


    </v-row>
     </v-form>
     </v-col>
     
   </v-row>
  </v-container>
</template>
<style scoped>

</style>
<script>
import axios from 'axios';
export default {
  data: () => ({
    valid : true,
    emailid  : "",
    password : "",
    show1 : false,
    emailRules : [
      v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
    ],
    passwordRules : [
      v => !!v || 'Password is required'
    ],
    lazy : false
   
    
}),
methods : {
  async validate (){
    if(this.$refs.form.validate())
    {
      
        axios.get("http://localhost:8000/home/?emailid="+this.emailid).then((response)=>{
          console.log(response.data);
        });
    }

  }
}
};
</script>

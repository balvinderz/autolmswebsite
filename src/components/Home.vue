<template>
  <v-container fluid>
    <v-row>
      <v-col>
        <v-dialog v-model="opendialog" width="500">
          <v-card dark>
            <v-card-title class="headline lighten-2" primary-title>Doing LMS</v-card-title>
            <v-card-text
              v-if="!gotresponse"
            >Waiting for response. Your Auto LMS will be done automatically. You can close this website if you want to .</v-card-text>
            <v-card-text v-if="id!=''">{{ id}}</v-card-text>

            <v-divider></v-divider>

            <v-card-actions>
              <div class="flex-grow-1"></div>
              <v-btn
                color="primary"
                text
                @click="()=> {opendialog = false;gotresponse=false;}"
              >Okay</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
        <v-form :lazy-validation="lazy" ref="form" :v-model="valid">
          <v-row class="ml-2 mr-2">
            <v-text-field
              v-model="emailid"
              placeholder="Email ID"
              :rules="emailRules"
              outlined
              type="email"
              required
            ></v-text-field>
          </v-row>
          <v-row class="ml-2 mr-2">
            <v-text-field
              v-model="password"
              placeholder="Password"
              type="password"
              :rules="passwordRules"
              required
              outlined
            ></v-text-field>
          </v-row>
          <v-row class="ml-2 mr-2">
            <v-checkbox v-model="doquiz" color="black" label="Do quiz ? "></v-checkbox>
          </v-row>
          <v-row class="ml-2 mr-2">
            <v-checkbox v-model="dodiscussionform" color="black" label="Do Discussion form ? "></v-checkbox>
          </v-row>
          <v-row justify="center">
            <v-btn outlined @click="validate" :disabled="justclicked">Start</v-btn>
          </v-row>
        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>
<style scoped>
</style>
<script>
import axios from "axios";
export default {
  data: () => ({
    valid: true,
    justclicked: false,
    gotresponse: false,
    emailid: "",
    password: "",
    doquiz: true,
    dodiscussionform: true,
    id: "",
    opendialog: false,
    show1: false,
    emailRules: [
      v => !!v || "E-mail is required",
      v => /.+@.+\..+/.test(v) || "E-mail must be valid",
      v => /.*@rait\.ac\.in$/gm.test(v) || "Email must end with rait.ac.in"
    ],
    passwordRules: [v => !!v || "Password is required"],
    lazy: false
  }),
  methods: {
    async validate() {
      if (this.$refs.form.validate()) {
        this.justclicked = true;
        this.opendialog = true;
        this.gotresponse = false;
        this.id = "";
        var doquiz = "0";
        var dodiscussionform = "0";
        if (this.doquiz) doquiz = "1";
        if (this.dodiscussionform) dodiscussionform = "1";
        let response = await axios.get(
          "/home/?emailid=" +
            this.emailid +
            "&password=" +
            this.password +
            "&doquiz=" +
            doquiz +
            "&dodiscussionform=" +
            dodiscussionform
        );
        //console.log(response.data);
        this.id = response.data;
        this.gotresponse = true;
        this.justclicked = false;
      }
    }
  }
};
</script>
 
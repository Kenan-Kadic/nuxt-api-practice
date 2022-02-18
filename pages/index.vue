<template>
  <v-container>
    <v-row>
      <v-col>
        <v-card :loading="thinking">
        <v-app-bar color="blue" elevation="0" dark>
          <span class="display-1">Customer Information</span>
          <v-spacer></v-spacer>
          <v-dialog>
            <template v-slot:activator="{attrs, on}">
              <v-btn icon v-bind="attrs" v:on="on"><v-icon>mdi-account</v-icon></v-btn>
            </template>
          <v-card>
          <v-card-title>Customer Popup</v-card-title>
          <v-card-text>I am the customer information</v-card-text>
          </v-card>
          </v-dialog>
        </v-app-bar>
          <v-card-title>Customer information</v-card-title>
        <v-card-text>
          <v-row>
          <v-col cols="6">
            <v-icon left>mdi-account</v-icon> {{ firstName }}, {{ lastName }}
          </v-col>
          <v-col cols="6">
            <v-icon left>mdi-email</v-icon> {{ email }}<br/>
            <template v-if="email2"><v-icon left>mdi-at</v-icon>{{ email2 }}</template>
          </v-col>
          <v-col cols="12">
            <img :src="picture"></img>
          </v-col>
            <v-col cols="6">
            <v-icon left>mdi-phone</v-icon> {{ phone }}
            </v-col>
            <v-col cols="6">
            <v-icon left>mdi-map-marker</v-icon> {{ city }}, {{ country }}
            </v-col>
          </v-row>
        </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>


<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      thinking: false,
      user: {},
      firstName:'',
      lastName: '',
      email: '',
      email2: '',
      picture: '',
      phone: '',
      city: '',
      country:''
    }
  },
  methods: {
    getData() {
      this.thinking = true;
      this.$axios.get('https://randomuser.me/api')
      .then(resp => {
        if (resp.status === 200) {
          this.user = resp.data;
          console.log(this.user)

          this.firstName = this.user.results[0].name.first
          this.lastName = this.user.results[0].name.last
          this.email = this.user.results[0].email
          this.picture = this.user.results[0].picture.large
          this.phone = this.user.results[0].phone
          this.city = this.user.results[0].location.city
          this.country = this.user.results[0].location.country
          this.thinking=false;
        }
      })
      .catch(err => {
        console.log(err)
        this.thinking=false;
      })
    }
  },
  mounted() {
    this.getData();
  }
}
</script>

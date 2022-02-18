<template>
  <v-container>
    <v-row>
      <v-col>
        <v-card :loading="thinking">
        <v-app-bar color="green" elevation="0" dark>
          <span class="display-1">Customer Information</span>
          <v-spacer></v-spacer>
          <v-icon>mdi-account</v-icon>
        </v-app-bar>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'IndexPage'
}
</script>

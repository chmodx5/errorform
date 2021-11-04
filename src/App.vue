<template>
  <v-app>
    <v-app-bar app light>
      <v-container>
        <div class="d-flex">
          <div class="d-flex align-center">
            <span class="text-uppercase text-h4 font-weight-black">knh</span>
          </div>

          <v-spacer></v-spacer>
          <v-btn text to="/reports"> reports </v-btn>
          <v-btn text to="/login"> login</v-btn>
        </div>
      </v-container>
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>

    <v-footer color="secondary darken-3 " dark class="pa-0">
      <v-container>
        <v-row no-gutters>
          <v-col md="4">
            <h5 class="text-h5 font-weight-bold text-capitalize">desc</h5>
            Lorem ipsum dolor sit amet consectetur adipisicing elit. Itaque
            beatae totam dicta magnam obcaecati. Fugiat delectus, quo in impedit
            ipsum, at ab obcaecati nihil doloremque saepe explicabo, officiis
            laborum sed!
          </v-col>
          <v-col
            class="primary lighten-2 py-4 text-center white--text"
            cols="12"
          >
            {{ new Date().getFullYear() }} — <strong>Vuetify</strong>
          </v-col>
        </v-row>
      </v-container>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    //
  }),
};
</script>

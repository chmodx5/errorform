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

    <v-footer color="secondary darken-4 " dark class="pa-0 py-10">
      <v-container>
        <v-row>
          <v-col md="6">
            <h5 class="text-h5 font-weight-bold text-capitalize">
              DISCLAIMER:
            </h5>
            The Hospital Management affirms that this is a blame free reporting
            tool. Any information provided is secure under Hospital policy and
            regulations and cannot be used against any staff for disciplinary
            action. The intent is to estimate the risk and evaluate patient
            safety for improved patient care.
          </v-col>
          <v-col md="3">
            <h5 class="text-h5 font-weight-bold text-capitalize">links</h5>
            <div>
              - <v-btn href="https://knh.or.ke/" text>khn homepage</v-btn>
            </div>
            <div v-for="(link, i) in links" :key="i">
              - <v-btn text>{{ link.title }}</v-btn>
            </div>
          </v-col>
          <v-col md="3">
            <h5 class="text-h5 font-weight-bold text-capitalize">
              social media
            </h5>
            <div v-for="(social, i) in social" :key="i">
              -
              <v-btn text
                ><v-icon>{{ social.icon }}</v-icon> {{ social.title }}</v-btn
              >
            </div>
          </v-col>
          <v-col md="12" class="mt-10 text-center text-capitalize">
            all rights reserved.
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
    links: [
      {
        title: "reports",
        link: "/reports",
      },
      {
        title: "login",
        link: "/login",
      },
    ],
    social: [
      {
        title: "twitter",
        link: "",
        icon: "",
      },
      {
        title: "facebook",
        link: "",
        icon: "",
      },
    ],
  }),
};
</script>

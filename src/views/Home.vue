<template>
  <v-container>
    <header-section />
    <form-section />
  </v-container>
</template>

<script>
import headerSection from "@/components/headerSection.vue";
import formSection from "@/components/formSection.vue";
export default {
  name: "Home",

  components: {
    headerSection,
    formSection,
  },
};
</script>

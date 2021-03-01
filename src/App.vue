<template>
  <v-app>
    <v-toolbar
      dark
      src="https://cdn.vuetifyjs.com/images/backgrounds/vbanner.jpg"
      max-height="60"
    >
      <v-toolbar-title>Youtube Curation</v-toolbar-title>
    </v-toolbar>
    <Top />
    <v-toolbar
      dark
      src="https://cdn.vuetifyjs.com/images/backgrounds/vbanner.jpg"
    >
      <v-space>
        <p>@QuestAcademia</p>
      </v-space>
    </v-toolbar>
  </v-app> 
</template>

<script>
  import Top from './components/Top.vue'

  export default {
    name: 'App',
    components: {
      Top
    }
  }
</script>
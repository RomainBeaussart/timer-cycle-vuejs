<template>
    <v-app>
        <v-content fluid>
            <router-view />
        </v-content>
    </v-app>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'App',

  data: () => ({
    //
  }),
});
</script>

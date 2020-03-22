<template>
  <v-app>
    

    <v-content>
      <spa/>
    </v-content>
  </v-app>
</template>

<script>
import spa from './components/spa';

export default {
  name: 'App',

  components: {
    spa,
  },

  data: () => ({
    //
  }),
};
</script>


<style>
.marginn-auto{
  margin: auto;
}
</style>
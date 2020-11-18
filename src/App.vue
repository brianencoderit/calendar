<template>
  <v-app>
    <v-main>
      <!-- <HelloWorld/> -->
      <Calendar/>
    </v-main>
  </v-app>
</template>

<script>
//import HelloWorld from './components/HelloWorld';
import Calendar from './components/calendar';

export default {
  name: 'App',

  components: { /*HelloWorld, */ Calendar },

  data: () => ({
    //
  }),
};
</script>

<template>
  <v-app>
    <ec-chat />
  </v-app>
</template>

<script>
import ECChat from './plugins/ECChat/ECChat'

export default {
  name: "App",
  components: {
    'ec-chat': ECChat
  },
  data: () => ({
    //
  })
};
</script>

<template>
  <v-container
    class="ma-0 pa-0 grey lighten-4"
    fluid
    fill-height
  >
    <v-layout>
      <v-flex>
        <v-layout
          align-center
          justify-center
          column
          fill-height
        >
          <v-flex
            style="width: 100%; height: 100%; max-height: calc(100% - 80px)"
          >
            <chat-messages
              :fetching-messages="fetchingMessages"
              :messages="messages"
              :get-user-by-id="getUserById"
            />
          </v-flex>
          <v-flex>
            <chat-footer
              :user="user"
              :send-message="sendMessage"
            />
          </v-flex>
        </v-layout>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import ChatFooter from "./components/ChatFooter.vue";
import ChatMessages from "./components/Messages.vue";

export default {
  data() {
    return {};
  },

  props: ["messages", "fetchingMessages", "user", "sendMessage", "getUserById"],

  components: {
    ChatFooter,
    ChatMessages
  }
};
</script>

<style scoped lang="scss">
</style>
<template>
  <v-container
    fluid
    fill-height
    class="messages-container grey lighten-4"
    ref="scrollable-element"
  >
    <v-layout
      :align-center="fetchingMessages || !messages.length"
      :justify-center="fetchingMessages || !messages.length"
    >
      <div class="pa-2">
        <v-progress-circular
          v-if="fetchingMessages"
          :size="50"
          color="primary"
          indeterminate
        ></v-progress-circular>
        <message
          v-else-if="messages.length"
          v-for="message in messages"
          :key="message._id"
          :message="message"
          :get-user-by-id="getUserById"
          :user="user"
        />
        <span v-else>No messages</span>
      </div>
    </v-layout>
    <v-snackbar
      v-model="newMessagesButton"
      :timeout="3000"
      color="white black--text"
    >
      There are new messages
      <v-btn
        color="primary"
        text
        @click="scrollToBottom"
      >
        Show
      </v-btn>
    </v-snackbar>
  </v-container>
</template>

<script>
import Message from "./Message.vue";
import { throttle } from "lodash";

export default {
  data() {
    return {
      offsetTop: 0,
      autoScroll: true,
      throttledOnScroll: null,
      isScrolledToBottom: true,
      scrollBottomBuffer: 50,
      newMessagesButton: false
    };
  },

  computed: {
    shouldAutoScroll() {
      return this.autoScroll && this.isScrolledToBottom;
    },
    scrollableElement() {
      return this.$refs["scrollable-element"];
    }
  },

  methods: {
    scrollToBottom() {
      this.$nextTick(() => {
        let chatContainer = this.scrollableElement;
        chatContainer.scrollTop = chatContainer.scrollHeight;
      });
    },
    onScroll() {
      let scrollBottom =
        this.scrollableElement.scrollHeight -
        (this.scrollableElement.scrollTop +
          this.scrollableElement.clientHeight);

      this.isScrolledToBottom = scrollBottom < this.scrollBottomBuffer;
      if (this.isScrolledToBottom) {
        this.newMessagesButton = false;
      }
    }
  },

  mounted() {
    this.throttledOnScroll = throttle(this.onScroll, 500);
    this.scrollableElement.addEventListener("scroll", this.throttledOnScroll);
  },

  beforeDestroy() {
    this.scrollableElement.removeEventListener(
      "scroll",
      this.throttledOnScroll
    );
  },

  watch: {
    messages: {
      handler: function() {
        if (this.shouldAutoScroll) {
          this.scrollToBottom();
        } else if (!this.isScrolledToBottom) {
          this.newMessagesButton = true;
        }
      },
      deep: true
    }
  },

  props: ["messages", "fetchingMessages", "user", "getUserById"],

  components: {
    Message
  }
};
</script>

<style scoped>
.messages-container {
  margin: 0;
  padding: 5px;
  overflow: scroll;
}
</style>
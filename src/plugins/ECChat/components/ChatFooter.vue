<template>
  <v-sheet class="chat-footer elevation-4 grey lighten-4">
    <v-text-field
      placeholder="Type your message..."
      v-model="text"
      solo
      hide-details
      rounded
      autocomplete="off"
      height="60"
      :disabled="sending"
    >
      <template v-slot:append-outer>
        <v-btn
          icon
          depressed
          @click="clickHandler"
          :disabled="!canSend"
          :loading="sending"
        >
          <v-icon>mdi-send</v-icon>
        </v-btn>
      </template>
    </v-text-field>
  </v-sheet>
</template>

<script>
export default {
  data() {
    return {
      text: null,
      sending: false
    };
  },

  computed: {
    canSend() {
      return !!this.text;
    }
  },

  methods: {
    clickHandler: function() {
      if (this.canSend) {
        let message = {
          user: this.user,
          text: this.text,
          created: new Date()
        };
        this.sending = true;
        this.sendMessage(message)
          .then(() => {
            this.text = "";
          })
          .catch(() => {
            // err
          })
          .finally(() => {
            this.sending = false;
          });
      }
    }
  },

  props: ["sendMessage", "user"]
};
</script>

<style scoped lang="scss">
.chat-footer {
  position: absolute;
  bottom: 0;
  right: 0;
  left: 0;
  padding: 10px;
  border-radius: 0;
}
</style>
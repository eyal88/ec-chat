<template>
  <v-container
    fluid
    class="message-container"
  >
    <v-row
      no-gutters
      style="flex-wrap: nowrap;"
    >
      <v-flex
        shrink
        class="d-none d-sm-flex"
      >
        <v-avatar
          size="35"
          class="mr-2"
        >
          <img
            :src="userAvatar"
            alt="avatar"
          >
        </v-avatar>
      </v-flex>
      <v-flex shrink>
        <v-card
          class="pa-3 pl-4 pr-4 message-card"
          flat
        >
          <h4>
            {{ messageUser.name }}
            <span class="grey--text font-weight-regular pl-1 pr-1">{{ createdString }}</span>
          </h4>
          <div
            v-html="message.text"
            class="subheading"
          ></div>
        </v-card>
      </v-flex>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data() {
    return {};
  },

  computed: {
    messageUser() {
      return this.getUserById(this.message.user);
    },
    isMyMessage() {
      return this.user === this.message.user;
    },
    userAvatar() {
      return `https://ui-avatars.com/api/?name=${this.userAvatarName}&background=${this.userAvatarColor}&size=80&color=ffffff&rounded=1&length=1`;
    },
    userAvatarName() {
      return this.messageUser ? this.messageUser.name : "Unknown";
    },
    userAvatarColor() {
      return this.messageUser ? this.messageUser.color : "336699";
    },
    createdString(showTime = true) {
      let options = { weekday: "long", month: "numeric", day: "numeric" };
      if (showTime) {
        options["hour"] = "numeric";
        options["minute"] = "numeric";
      }
      return new Intl.DateTimeFormat("en-US", options).format(
        this.message.created
      );
    }
  },

  props: ["message", "user", "getUserById"]
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.message-container {
  padding: 5px;
}

.message-card {
  border-radius: 10px !important;

  h4 {
    margin-right: 50px;
  }
}
</style>
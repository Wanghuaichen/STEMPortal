<template>
  <v-menu
    v-model="menu"
    :close-on-content-click="false"
    nudge-bottom="30"
  >
    <template v-slot:activator="{ on }">
      <a v-on="on">
        <v-avatar size="30" class="mr-1">
          <img
            src="https://cdn.vuetifyjs.com/images/john.jpg"
            alt="John"
          >
        </v-avatar>
        {{ user.username }}
      </a>
    </template>

    <v-card>
      <v-list>
        <v-list-item>
          <v-list-item-avatar>
            <img src="https://cdn.vuetifyjs.com/images/john.jpg" alt="John">
          </v-list-item-avatar>

          <v-list-item-content>
            <v-list-item-title>{{ user.fullname }}</v-list-item-title>
            <v-list-item-subtitle>Veteran {{ user.type }}</v-list-item-subtitle>
          </v-list-item-content>

          <v-list-item-action>
            <v-btn
              :class="fav ? 'red--text' : ''"
              icon
              @click="fav = !fav"
            >
              <v-icon>mdi-heart</v-icon>
            </v-btn>
          </v-list-item-action>
        </v-list-item>
      </v-list>

      <v-divider></v-divider>
      <v-card-text class="mb-n3">Quick settings</v-card-text>
      <v-list>
        <v-list-item>
          <v-list-item-action>
            <v-switch v-model="message"></v-switch>
          </v-list-item-action>
          <v-list-item-title>Enable messages</v-list-item-title>
        </v-list-item>
        <v-list-item>
          <v-list-item-action>
            <v-switch v-model="notification"></v-switch>
          </v-list-item-action>
          <v-list-item-title>Enable notifications</v-list-item-title>
        </v-list-item>
      </v-list>

      <v-card-actions>
        <v-btn text :to="{ name: 'UserProfile' }">More settings</v-btn>
        <div class="flex-grow-1"></div>
        <v-btn text color="primary" @click="$emit('logout')">Logout</v-btn>
      </v-card-actions>
    </v-card>
  </v-menu>
</template>

<script>
export default {
  computed: {
    user () { return this.$store.getters.user }
  },
  data: () => ({
    message: true,
    notification: false,
    fav: true,
    menu: false
  })
}
</script>

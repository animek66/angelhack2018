<template>
    <v-container>
        <v-card class="pa-3">
            <v-list>
                <v-subheader>Notifications</v-subheader>
                <v-divider></v-divider>
                <v-list-tile v-if="show">
                    <v-list-tile-title>Filip has created a document!</v-list-tile-title>

                    <v-btn color="green"
                           @click="addNotification">
                        <v-icon>check</v-icon>
                    </v-btn>
                    <v-btn color="red"
                           @click="addNotification">
                        <v-icon>clear</v-icon>
                    </v-btn>

                </v-list-tile>
            </v-list>
        </v-card>
    </v-container>
</template>

<script>
import gql from 'graphql-tag'
export default {
  data() {
    return {
      show: true
    }
  },
  layout: 'dashboard',
  methods: {
    async addNotification() {
      await this.$apollo.mutate({
        mutation: gql`
          mutation createNotif {
            createUserActionRequest(
              data: {
                type: NOTIFICATION,
                title: "Albert has created this document"
                content: "Please review this document."
                user: { connect: { id: "cjhdb68xd000a0826atfvzox3" } }
                workflowNode: { connect: { id: "cjhenfjey03990826x7dhfeaz" } }
                submission: { connect: { id: "cjhenfr8p03aq0826xbphswri" } }
              }
            ) {
              id
            }
          }
        `
      })
      this.show = false
    }
  }
}
</script>

<style>
</style>

<template>
    <v-card flat tile>
        <v-toolbar dense>

        <v-toolbar-title>Board App</v-toolbar-title>

        <v-spacer></v-spacer>

        <v-btn icon @click="onClickLogout">
            <v-icon>mdi-logout</v-icon>
        </v-btn>
        </v-toolbar>
    </v-card>
</template>

<script>
export default {
    data() {
        return {
            
        }
    },

    methods: {
        onClickLogout() {
            console.log('onClickLogout');
            this.$router.push('/');
        }
    },
}
</script>
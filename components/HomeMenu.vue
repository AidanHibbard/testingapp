<template>
    <v-col>
        <v-card
        width="75%"
        height="150px"
        >
        <v-card-title>
            Comparisons
        </v-card-title>
        <v-card-text>
            Compare payloads between two API calls
        </v-card-text>
        <v-spacer />
        <v-btn>
            <NuxtLink to="/comparetool">
            Open
            </NuxtLink>
        </v-btn>
        </v-card>
    </v-col>
</template>

<script>
export default {
    name: 'HomeMenu'
}
</script>

<style scoped>
.col {
    margin: 0 auto;
}
.v-card {
    margin: 0 auto;
}
</style>
<template>
    <v-main>
        <v-form ref="form">
            <v-text-field
                label="URL One"
                placeholder="URL One"
                v-model="UrlOne"
                outlined
            ></v-text-field>
            <v-spacer />
            <v-text-field
                label="URL Two"
                placeholder="URL Two"
                v-model="UrlTwo"
                outlined
            ></v-text-field>
                <v-btn
                @click="this.FetchAndCompare"
                >
                    Compare
                </v-btn>
        </v-form>
        <div v-if="this.PayloadDiff === null">
            Nothing to compare
        </div>
        <div v-else>
            {{this.PayloadDiff}}
        </div>
    </v-main>
</template>

<script>
import {diff} from 'jest-diff';
export default {
    data() {
        return {
            PayloadDiff: null,
            UrlOne: null,
            UrlTwo: null,
        }
    },
    methods: {
        async FetchAndCompare() {
            const a = await this.$axios.$get(
                this.UrlOne
            )
            const b = await this.$axios.$get(
                this.UrlTwo
            )
            this.PayloadDiff = diff(a,b)
        },
    },
}
</script>

<style scoped>

</style>
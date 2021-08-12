<template>
    <v-main>
        <v-form ref="form">
            <v-text-field
                label="URL One"
                placeholder="URL One"
                v-model="UrlOne"
                outlined
            ></v-text-field>
            <v-checkbox
                v-model="CboxOne"
                :label="`GraphQl ${CboxOne.toString()}`"
            ></v-checkbox>
            <p>Or enter a payload you'd like to compare <br /> (note: For graphQL requests please paste the request in here and select GraphQL)</p>
            <v-textarea
                outlined
                clearable
                clear-icon="mdi-close-circle"
                label="Box One"
                v-model="TextAreaOne"
            ></v-textarea>
            <v-spacer />
            <hr />
            <v-spacer />
            <v-text-field
                label="URL Two"
                placeholder="URL Two"
                v-model="UrlTwo"
                outlined
            ></v-text-field>
            <v-checkbox
                v-model="CboxTwo"
                :label="`GraphQl ${CboxTwo.toString()}`"
            ></v-checkbox>
            <p>Or enter a payload you'd like to compare <br /> (note: For graphQL requests please paste the request in here and select GraphQL)</p>
                <v-textarea
                outlined
                clearable
                clear-icon="mdi-close-circle"
                label="Box Two"
                v-model="TextAreaTwo"
            ></v-textarea>
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
//
import {diff} from 'jest-diff';
export default {
    data() {
        return {
            PayloadDiff: null,
            UrlOne: null,
            UrlTwo: null,
            CboxOne: false,
            CboxTwo: false,
            TextAreaOne: null,
            TextAreaTwo: null,
        }
    },
    methods: {
        async FetchAndCompare() {
            let a, b;
            // A
            if (this.CboxOne === true) {
                // Gql req
                a = await this.$axios({
                    BaseURL: `${this.UrlOne}`,
                    method: 'post',
                    data: {
                        query: `${this.TextAreaOne}`, // Add in text field value
                    }
                })
            } else if (this.TextAreaOne != null && this.CboxOne === false) {
                a = this.TextAreaOne
            } else {
                // Check for payload in text area then go for regular req
                a = await this.$axios.$get(`${this.UrlOne}`)
            }
            // B 
            if (this.CboxTwo === true) {
                // gql req
                b = await this.$axios({
                    BaseURL: `${this.UrlTwo}`,
                    method: 'post',
                    data: {
                        query: `${this.TextAreaTwo}`, // Add in text field value
                    }
                })
            } else if (this.TextAreaTwo != null && this.CboxTwo === false) {
                b = this.TextAreaTwo
            } else {
                // Check for payload in text area then go for regular req
                b = await this.$axios.$get(`${this.UrlTwo}`)
            } 
            this.PayloadDiff = diff(a,b)
        }
    },
}
</script>

<style scoped>

</style>
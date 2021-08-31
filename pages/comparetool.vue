<template>
    <v-main>
        <v-form ref="form">
            <v-text-field
                label="URL One"
                placeholder="URL One"
                v-model="UrlOne"
                outlined
            ></v-text-field>
            <p>Or enter a payload you'd like to compare <br /> (note: For graphQL requests please paste the request in here and select GraphQL)</p>
            <v-checkbox
                v-model="CboxOne"
                :label="`GraphQl ${CboxOne.toString()}`"
            ></v-checkbox>
            <v-textarea
                outlined
                clearable
                clear-icon="mdi-close-circle"
                label="Box One"
                v-model="TextAreaOne"
            ></v-textarea>
            <v-spacer />
            <v-spacer />
            <v-text-field
                label="URL Two"
                placeholder="URL Two"
                v-model="UrlTwo"
                outlined
            ></v-text-field>
            <p>Or enter a payload you'd like to compare <br /> (note: For graphQL requests please paste the request in here and select GraphQL)</p>
            <v-checkbox
                v-model="CboxTwo"
                :label="`GraphQl ${CboxTwo.toString()}`"
            ></v-checkbox>
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
        <br />
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
                // Checks if first checkbox is true
                a = await this.$axios({ // Basic axios graphql request
                    BaseURL: `${this.UrlOne}`,
                    method: 'post',
                    data: {
                        query: `${this.TextAreaOne}`, // Add in first text field value
                    }
                })
                // Check if the text area has a value and the first URL box is empty
            } else if (this.TextAreaOne != null && this.UrlOne === null) {
                a = this.TextAreaOne
            } else {
                // If nothing else hit the provided first URL
                a = await this.$axios.$get(`${this.UrlOne}`)
            }
            // B 
            if (this.CboxTwo === true) {
                // Checks if second checkbox is true
                b = await this.$axios({ // Basic axios graphql request
                    BaseURL: `${this.UrlTwo}`,
                    method: 'post',
                    data: {
                        query: `${this.TextAreaTwo}`, // Add in second text field value
                    }
                })
                // Check if the text area has a value and the second URL box is empty
            } else if (this.TextAreaTwo != null && this.UrlTwo === null) {
                b = this.TextAreaTwo
            } else {
                // If nothing else hit the provided second URL
                b = await this.$axios.$get(`${this.UrlTwo}`)
            } 
            this.PayloadDiff = diff(a,b)
        }
    },
}
</script>

<style scoped>

</style>
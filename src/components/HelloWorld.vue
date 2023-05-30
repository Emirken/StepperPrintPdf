<template>
    <v-container>
        <v-row class="text-center">
            <v-col cols="12">
                <v-stepper v-model="e1">
                    <v-stepper-header>
                        <v-stepper-step :complete="e1 > 1" step="1">
                            Name of step 1
                        </v-stepper-step>
                        <v-divider></v-divider>
                        <v-stepper-step :complete="e1 > 2" step="2">
                            Name of step 2
                        </v-stepper-step>
                        <v-divider></v-divider>
                        <v-stepper-step step="3">
                            Name of step 3
                        </v-stepper-step>
                    </v-stepper-header>

                    <v-stepper-items>
                        <v-stepper-content step="1">
                            <v-form v-model="valid">
                                <v-container>
                                    <v-row>
                                        <v-col cols="12" md="4">
                                            <v-text-field
                                                v-model="firstname"
                                                :rules="nameRules"
                                                label="First name"
                                                required
                                            ></v-text-field>
                                        </v-col>

                                        <v-col cols="12" md="4">
                                            <v-text-field
                                                v-model="lastname"
                                                :rules="nameRules"
                                                label="Last name"
                                                required
                                            ></v-text-field>
                                        </v-col>

                                        <v-col cols="12" md="4">
                                            <v-text-field
                                                v-model="tc"
                                                :rules="tcRules"
                                                :counter="11"
                                                label="Tc"
                                                required
                                            ></v-text-field>
                                        </v-col>
                                    </v-row>
                                </v-container>
                            </v-form>
                            <v-btn color="primary" @click="nextStep()">
                                Continue
                            </v-btn>
                            <v-btn text>
                                Cancel
                            </v-btn>
                        </v-stepper-content>

                        <v-stepper-content step="2">
                            <div id="element">
                                <v-card>
                                    <v-responsive :aspect-ratio="16/9">
                                        <v-card-text>

                                            <ul><b>First Name:</b> {{ firstname }}</ul>
                                            <ul><b>Last Name:</b> {{ lastname }}</ul>
                                            <ul><b>TC:</b> {{ tc }}</ul>

                                        </v-card-text>
                                    </v-responsive>
                                </v-card>
                            </div>
                            <v-btn color="primary" @click="nextStep()">
                                Continue
                            </v-btn>
                            <v-btn text>
                                Cancel
                            </v-btn>
                        </v-stepper-content>

                        <v-stepper-content step="3">

                            <v-btn color="primary" @click="print()" >
                                PDF
                            </v-btn>

                        </v-stepper-content>
                    </v-stepper-items>
                </v-stepper>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
import html2pdf from 'html2pdf.js';
export default {
    data() {
        return {
            e1: 1,
            valid: false,
            firstname: '',
            lastname: '',
            tc: '',
            nameRules: [
                (v) => !!v || 'First name is required',
            ],
            tcRules: [(v) => !!v || 'Tc is required'],
        };
    },
    methods: {
        nextStep() {
            this.e1 = this.e1+1; // Move to the next step
        },
        print(){
            var element = document.getElementById('element');
            html2pdf().from(element).set({ text: { mode: 'text' } }).save();
        }

    },
};
</script>

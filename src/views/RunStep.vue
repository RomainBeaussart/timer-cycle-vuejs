<template>
    <v-container fluid>
        <v-card
            outlined
            @click="dialogChrono = true"
        >
            <v-layout pa-3 wrap>
                <v-flex xs2 class="font-weight-black display-1" style="color: #1abc9c">
                    {{ index }}
                </v-flex>
                <v-flex xs10 class="font-weight-black display-1 d-flex justify-end" style="color: #1abc9c">
                    {{ step.type }}
                </v-flex>
                <v-flex xs10>
                    {{ step.text }}
                </v-flex>
                <v-flex xs2 class="d-flex align-center justify-end">
                    {{ formatChrono(step.chrono) }}
                </v-flex>
            </v-layout>
        </v-card>
        <v-dialog v-model="dialogChrono">
            <v-card>
                <v-toolbar dense dark color="#1abc9c">
                    <v-toolbar-title>Selectionnez le temps</v-toolbar-title>
                    <v-spacer></v-spacer>
                    <v-btn icon
                        @click="dialogChrono = false"
                    >
                        <v-icon>fa-times</v-icon>
                    </v-btn>
                </v-toolbar>
                <v-card-text class="pt-3">
                    <v-select
                        v-model="step.type"
                        :items="types"
                        label="Type"
                        item-text="text"
                        item-value="value"
                        color="#1abc9c"
                        outlined
                    ></v-select>
                    <v-text-field
                        v-model="step.text"
                        label="Description"
                        outlined
                        color="#1abc9c"
                    ></v-text-field>
                    <v-layout wrap>
                        <v-flex xs5 pr-1 mt-5 v-if="step.type === 'CHRONO'">
                            <v-select
                                v-model="step.chrono.min"
                                :items="min"
                                label="Min"
                                outlined
                            ></v-select>
                        </v-flex>
                        <v-flex xs7 pl-1 mt-5 v-if="step.type === 'CHRONO'">
                            <v-select
                                v-model="step.chrono.sec"
                                :items="sec"
                                label="Sec"
                                outlined
                            ></v-select>
                        </v-flex>
                        <v-flex xs12 class="d-flex justify-end">
                            <v-btn
                                rounded
                                color="#1abc9c"
                                dark
                                elevation = "0"
                                @click="dialogChrono = false"
                            > Valider <v-icon right small>fa-check</v-icon>
                            </v-btn>
                        </v-flex>
                    </v-layout>
                </v-card-text>
            </v-card>
        </v-dialog>
    </v-container>
</template>

<script lang="ts">
import { Component, Vue, Prop } from "vue-property-decorator"
import moment from 'moment'

@Component
export default class RunStep extends Vue{
    @Prop() step: any
    @Prop() index: number

    dialogChrono = false

    types = [
        { text: "Chrono", value: "CHRONO" },
        { text: "Pause", value: "PAUSE" }
    ]

    get min() {
        const min = []
        for(let i = 0; i <= 20; i++) {
            min.push(i)
        }
        return min
    }

    sec = [0, 15, 30, 45]

    formatChrono(time: any) {
        if(time.min === 0 && time.sec === 0) return "00:00"
        return moment(time.min + ":" + time.sec, "mm:ss").format("mm:ss");
    }
}
</script>

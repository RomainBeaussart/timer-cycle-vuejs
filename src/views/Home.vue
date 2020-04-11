<template>
    <v-container fluid>
        <v-layout wrap>
            <v-flex xs12 mb-3 class="d-flex justify-center display-2 font-weight-black">
                TB RUN Hein ?
            </v-flex>
            <v-flex xs12 my-2 v-for="(step, index) in steps" :key="index">
                <RunStep
                    :step="step"
                    :index="index"
                ></RunStep>
            </v-flex>
            <v-flex xs12 class="d-flex justify-center">
                <v-btn
                    rounded
                    elevation="0"
                    color="#1abc9c"
                    dark
                    @click="addStep()"
                >Ajouter une étape<v-icon right>fa-plus</v-icon></v-btn>
            </v-flex>
            <v-flex xs12 my-3 class="d-flex justify-center">
                <v-btn
                    rounded
                    elevation="0"
                    color="#1abc9c"
                    dark
                    @click="dialogPlay = true"
                >Lancer ma Run<v-icon right>fa-play</v-icon></v-btn>
            </v-flex>
        </v-layout>
        <v-dialog fullscreen v-model="dialogPlay">
            <Run
                :steps="steps"
                v-bind:play="dialogPlay"
            ></Run>
        </v-dialog>
    </v-container>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator"
import moment from 'moment'

import RunStep from './RunStep.vue'
import Run from './Run.vue'

@Component({
    components: {
        RunStep,
        Run
    }
})
export default class Home extends Vue{
    steps = [{"type":"CHRONO","chrono":{"min":5,"sec":0},"text":"105 - 120"},{"type":"CHRONO","chrono":{"min":1,"sec":0},"text":"120 - 140"},{"type":"CHRONO","chrono":{"min":1,"sec":0},"text":"140 - 155"},{"type":"CHRONO","chrono":{"min":1,"sec":0},"text":"120 - 140"},{"type":"CHRONO","chrono":{"min":2,"sec":0},"text":"105 - 120"},{"type":"CHRONO","chrono":{"min":10,"sec":0},"text":"120 - 140"},{"type":"PAUSE","chrono":{"min":0,"sec":0},"text":"110"},{"type":"CHRONO","chrono":{"min":4,"sec":0},"text":"140 - 155"},{"type":"PAUSE","chrono":{"min":0,"sec":0},"text":"110"},{"type":"CHRONO","chrono":{"min":1,"sec":0},"text":"150"},{"type":"PAUSE","chrono":{"min":0,"sec":0},"text":"110"},{"type":"CHRONO","chrono":{"min":10,"sec":0},"text":"120 - 140"},{"type":"PAUSE","chrono":{"min":0,"sec":0},"text":"110"},{"type":"CHRONO","chrono":{"min":4,"sec":0},"text":"140 - 155"},{"type":"PAUSE","chrono":{"min":0,"sec":0},"text":"110"},{"type":"CHRONO","chrono":{"min":1,"sec":0},"text":"150"},{"type":"CHRONO","chrono":{"min":5,"sec":0},"text":"105 - 120"}]

    dialogPlay = false

    addStep() {
        this.steps.push({
            type: "CHRONO",
            chrono: {
                min: 0,
                sec: 0
            },
            text: "",
        })
    }

    deleteStep(index: any) {
        this.steps.splice(index, 1)
    }

    test() {
        console.log(JSON.stringify(this.steps))
    }
}
</script>



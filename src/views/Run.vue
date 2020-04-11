<template>
    <v-card>
        <v-layout wrap>
            <v-flex xs12 my-3 class="display-2 d-flex justify-center" style="height: 100vh" :key="currentStep" v-if="!finish && steps[currentStep] && steps[currentStep].type === 'CHRONO'">
                <countdown :leftTime="getTimer(steps[currentStep])" :pauseCountdown="true">
                    <span
                        slot="process"
                        slot-scope="timer"
                    >
                        <v-layout wrap>
                            <v-flex xs12 my-2 class="d-flex justify-center display-4 align-center" style="height: 12vh">
                                {{ `${timer.timeObj.ceil.s % 60 === 0 ? timer.timeObj.ceil.m :timer.timeObj.ceil.m - 1} : ${timer.timeObj.ceil.s % 60}` }}
                            </v-flex>
                            <v-flex xs12 my-2 class="d-flex justify-center align-center" style="height: 12vh">
                                {{ steps[currentStep].text }}
                            </v-flex>
                            <v-flex xs12 my-2 class="d-flex justify-center align-center" style="height: 50vh"
                                @click="() => { timer.state === 'process' ? timer.pauseCountdown() : timer.startCountdown() }"
                            >
                                <v-btn
                                    icon
                                    x-large
                                >
                                    <v-icon large>{{ timer.state === 'process' ? 'fa-pause' : 'fa-play'}}</v-icon>
                                </v-btn>
                            </v-flex>
                        </v-layout>
                    </span>
                    <span slot="finish">
                        <v-layout wrap>
                            <v-flex xs12 my-2 class="d-flex justify-center display-4 align-center" style="height: 100vh"
                                @click="nextStep()"
                            >
                                <v-btn 
                                    outlined
                                    rounded
                                    x-large
                                >
                                    Next Step
                                </v-btn>
                            </v-flex>
                        </v-layout>
                    </span>
                </countdown>
            </v-flex>
            <v-flex xs12 my-3 class="display-2 d-flex justify-center align-center" style="height: 100vh" :key="currentStep" v-if="!finish && steps[currentStep] && steps[currentStep].type === 'PAUSE'">
                <v-layout wrap>
                    <v-flex xs12 style="height: 20vh" class="display-4">
                        PAUSE
                    </v-flex>
                    <v-flex xs12 style="height: 20vh" class="display-2">
                        {{ steps[currentStep].text }}
                    </v-flex>
                    <v-flex xs12 style="height: 60vh" @click="nextStep()">
                        <v-btn 
                            outlined
                            rounded
                            x-large
                        >
                            Next Step
                        </v-btn>
                    </v-flex>
                </v-layout>
            </v-flex>
            <v-flex style="height: 100vh" xs12 v-if="finish">
                <span class="display-2 d-flex justify-center align-center" style="height: 100vh">
                    Finish
                </span>
            </v-flex>
        </v-layout>
    </v-card>
</template>

<script lang="ts">
import { Component, Vue, Prop, Watch } from "vue-property-decorator"
// import moment from 'moment'

@Component
export default class Run extends Vue{
    @Prop({default: []}) steps

    pause = true

    key = 0

    currentStep = 0

    update = 0

    finish = false

    getTimer(step: any){
        return (step.chrono.min * 60 + step.chrono.sec) * 1000
    }

    nextStep() {
        if(this.steps.length - 1 > this.currentStep ){
            this.currentStep ++
        } else {
            debugger
            this.finish = true
        }
    }

}
</script>

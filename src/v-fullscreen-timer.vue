<template>
    <v-overlay opacity=".9">
        <div class="d-flex flex-column">
            <div class="text-h3 mx-auto" v-if="title">
                {{ title }}
            </div>
            <v-divider class="my-4" color="white" v-if="title" />
            <div class="text-h2 mx-auto">{{ elapsedTimeString }}</div>
            <v-btn @click="stop" class="mx-auto mt-6" icon>
                <v-icon class="text-h3">mdi-stop-circle-outline</v-icon>
            </v-btn>
        </div>
    </v-overlay>
</template>

<script>
import { VOverlay, VIcon, VBtn } from 'vuetify/lib'


import moment from 'moment';

const STANDARD_DATE_FORMAT = 'YYYY-MM-DDTHH:mm:ss';
export default {
    components: {
        VOverlay,
        VIcon,
        VBtn
    },
    computed: {
        momentStartPoint() {
            return moment(this.startPoint, STANDARD_DATE_FORMAT);
        },
    },
    data() {
        return {
            timer: null,
            elapsedTimeString: "00:00:00",
            elapsedTimeUnit: 0
        }
    },
    methods: {
        stop() {
            clearInterval(this.timer);
            this.$emit('stop', this.elapsedTimeUnit);
        }
    },
    mounted() {
        this.$nextTick(() => {
            this.timer = setInterval(() => {
                let nowFotmatted = moment(Date.now()).format(STANDARD_DATE_FORMAT);
                let momentNow = moment(nowFotmatted, STANDARD_DATE_FORMAT);
                let diff = momentNow.diff(this.momentStartPoint);
                const hours = moment.utc(diff).format('HH');
                const minutes = moment.utc(diff).format('mm');
                const seconds = moment.utc(diff).format('ss');
                this.elapsedTimeString = `${hours}:${minutes}:${seconds}`;
                this.elapsedTimeUnit = momentNow.diff(this.momentStartPoint, this.outputMode);
            }, 1);
        })
    },
    name: 'v-fullscreen-timer',
    props: {
        outputMode: {
            type: String,
            default: 'minutes'
        },
        startPoint: {
            type: Date,
            required: true
        },
        title: String
    }
}
</script>

<style>

</style>
<template>
    <div class="wrapper">
        <div class="box header">
            <img src="./assets/mrover.png" 
                 title="MRover"
                 width="48" height="48"/>
            <h1>Dashboard</h1>
            <div class="spacer"></div>
            <div class="comms">
                <comm-indicator name="WS"
                                :state="websocket_connected"/>
                <comm-indicator name="LCM"
                                :state="connected"/>
            </div>
        </div>
        <div class="box video">
            Video goes here
        </div>
        <div class="box odom">
            Current odometry reading:
            {{ odom.latitude_deg }} by {{ odom.longitude_deg }}
            bearing {{ odom.bearing_deg }}
        </div>
        <div class="box diags">
            Diagnostics and sensor output go here
        </div>
    </div>
</template>

<script>
import CommIndicator from './CommIndicator.vue'
import { mapState } from 'vuex'

export default {
    computed: mapState([
        'websocket_connected',
        'connected', 
        'odom'
    ]),
    components: {
        CommIndicator
    }
}
</script>

<style scoped>
.wrapper {
    display: grid;
    grid-gap: 10px;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 60px 3fr 2fr;
    grid-template-areas:
        "header header"
        "video odom"
        "diags diags";

    font-family: Cantarell sans;
    height: 100%;
}

.box {
    border-radius: 5px;
    padding: 10px;
    border: 1px solid black;
}

img {
    border: none;
    border-radius: 0px;
}

.header {
    grid-area: header;
    display: flex;
    align-items: center;
}

.header h1 {
    margin-left: 5px;
}

.spacer {
    flex-grow: 1;
}

.comms {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
}

.comms * {
    margin-top: 2px;
    margin-bottom: 2px;
}

.video {
    grid-area: video;
}

.odom {
    grid-area: odom;
}

.diags {
    grid-area: diags;
}
</style>

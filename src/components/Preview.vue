<template>
    <div>
        <ul class="list-group" v-for="(u,i) in user" :key="u">
            <li class="list-group-item text-left"><span>{{i}} - </span>{{u}}</li>
        </ul>
        <button class="btn btn-primary" @click.prevent="sendData">Submit</button>
    </div>
</template>

<script>
import { EVENTBUS } from '../main';

export default {
    data: function() {
        return {
            user: []
        }
    },
    created() {
        EVENTBUS.$on('userData', (arg) => {
            this.user = arg;
        })
    },
    methods: {
        sendData() {
            console.log('send data to backend');
            console.log(this.user);
        }
    }
}
</script>

<style scoped>
    div {
        width: 50%;
        margin: 0 auto;
    }
    li {
        padding-left: 4rem;
    }
    span {
        padding-right: 2rem;
    }
    button {
        margin: 2rem auto;
    }
</style>
<template>
    <form>
        <div class="form-group">
            <label for="username">Username</label>
            <input type="text" class="form-control" id="username" v-model.lazy="username">
        </div>
        <div class="form-group">
            <label for="password">Password</label>
            <input type="password" class="form-control" id="password" v-model.lazy="password">
        </div>
        <div class="form-group">
            <label for="gender">Gender</label>
            <select class="form-control" id="gender" v-model="gender">
                <option v-for="(g) in genderProp" :key="g" >{{g}}</option>
            </select>
        </div>
        <div class="form-group form-check">
            <input type="checkbox" class="form-check-input" id="term" value="agree" v-model="term">
            <label class="form-check-label" for="term">Agree term</label>
        </div>
        <appWarning v-if="showWarning"></appWarning>
        <button class="btn btn-primary mt-3 mb-3" @click.prevent="sendUserInputs">Preview</button>
    </form>
</template>

<script>
import { EVENTBUS } from '../main';
import Warning from './Warning';

export default {
    data: function() {
        return {
            username: '',
            password: '',
            gender: '',
            term: [],
            showWarning: true
        }
    },
    components: {
        appWarning: Warning
    },
    props: ['genderProp'],
    methods: {
        checkAllFilled() {
            if(this.username.length > 0 && this.password.length > 0 && this.gender.length > 0 && this.term.length > 0) {
                this.showWarning = false;
            } else {
                this.showWarning = true;
            }
        },
        sendUserInputs() {
            this.$emit('inputsFilled', !this.showWarning);
            EVENTBUS.$emit('userData', [this.username, this.password, this.gender, this.term[0]]);
        }
    },
    watch: {
        username: function() {
            this.checkAllFilled();
        },
        password: function() {
            this.checkAllFilled();
        },
        gender: function() {
            this.checkAllFilled();
        },
        term: function() {
            this.checkAllFilled();
        }
    }
}
</script>

<style scoped>
    .form-group {
        width: 80%;
        margin: 2rem auto;
    }
</style>
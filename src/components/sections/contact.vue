<template>
    <div class="section-child">
        <div class="vertical-align contact">
            <h6 class="headers">Contact</h6>
            <b-form name="contact" @submit="onSubmit" method="post" netlify>
                <b-alert variant="success" :show="success">Thanks! Your message has been sent.</b-alert>
                <b-alert variant="danger" :show="failure">Your message was not sent!</b-alert>

                    <b-form-group id="name" label="Name:" label-for="name">
                        <b-form-input name="name" id="name" type="text" v-model="form.name" placeholder="Name" required></b-form-input>
                    </b-form-group>

                    <b-form-group id="email" label="Email:" label-for="email">
                        <b-form-input name="email" id="email" type="email" v-model="form.email" placeholder="Email" required></b-form-input>
                    </b-form-group>

                    <b-form-group id="message" label="Message:" label-for="message">
                        <b-form-textarea name="message" id="message" v-model="form.message" placeholder="Message" required no-resize></b-form-textarea>
                    </b-form-group>

                    <div data-netlify-recaptcha></div>

                    <b-button type="submit" variant="primary">Send</b-button>
            </b-form>
            
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'contact',

    data () {
        return {
            form: {
                name: '',
                email: '',
                message: ''
            },
            success: false,
            failure: false
        }
    },

    methods: {
        onSubmit (event) {
            event.preventDefault();

            axios({
                url: "https://bbj8ce8dr7.execute-api.eu-west-1.amazonaws.com/prod/send",
                method: "POST",
                headers: { 
                    "Content-Type": "application/json"
                },
                data: JSON.stringify({
                    name: this.form.name,
                    email: this.form.email,
                    desc: this.form.message
                })
            })
            
            this.success = 10;
        }
    }
}
</script>

<style>
.contact {
    overflow: auto;
}

form {
    margin: 0 auto;
}

label {
    float: left;
}

textarea {
    min-height: 200px;
    height: 200px;
    max-height: 200px;
}

button {
    float: right;
    margin-bottom: 10px;
}

@media (min-width: 768px) {
    form {
        width: 50%;
    }

    .left {
        width: 48%;
        float: left;
    }

    .right {
        width: 48%;
        float: right;
    }

    textarea {
        min-height: 250px;
        height: 250px;
        max-height: 250px;
    }
}
</style>
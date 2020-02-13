<template>
    <div class="home">
        <b-row>
            <b-col cols="12">
                <iframe width="1120" height="630"
                        src="https://www.youtube.com/embed/45uM53OYD9c?controls=0&disablekb=1&loop=1&playlist=45uM53OYD9c&autoplay=1&modestbranding=1"
                        frameborder="0" allow="autoplay; encrypted-media; picture-in-picture"></iframe>
            </b-col>
            <b-col cols="12">
                <b-button squared variant="outline-secondary" href="#map" class="mt-4 pr-5 pl-5">MAP</b-button>
            </b-col>
        </b-row>
        <b-row class="justify-content-around" id="cards">
                <b-card
                        title="Cupola"
                        img-src="https://images.fastcompany.net/image/upload/w_1280,f_auto,q_auto,fl_lossy/wp-cms/uploads/2017/07/p-1-inside-iss-1.jpg"
                        img-alt="ISS-Cupola"
                        img-top
                        tag="article"
                        style="max-width: 20rem;"
                        class="mb-2 mt-5"
                >
                    <b-card-text>
                        Its seven windows are used to conduct experiments, dockings and observations of Earth.
                    </b-card-text>
                </b-card>
                <b-card
                        title="Leonardo"
                        img-src="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcRpFVnDbM5_yO6C5sF5bJYtVoD6E7W2e3gksJgWHvidWVl0KuuG"
                        img-alt="ISS-Leonardo"
                        img-top
                        tag="article"
                        style="max-width: 20rem;"
                        class="mb-2 mt-5"
                >
                    <b-card-text>
                        Its seven windows are used to conduct experiments, dockings and observations of Earth.
                    </b-card-text>
                </b-card>
        </b-row>
        <b-row>
            <b-col id="map">
                <iframe width="600" height="450" frameborder="0" style="border:0"
                        src="https://www.google.com/maps/embed/v1/place?q=paris&key=AIzaSyBD_ZqxJbzgqk50VaGWoWZDojNirkqmMJM" allowfullscreen></iframe>
            </b-col>
        </b-row>
        <b-row class="mt-5 justify-content-center">
            <b-col align="center" cols="8">
                <b-form-group
                        id="fieldset-1"
                        description="Let us know your email."
                        label="Register"
                        label-for="input-1"
                        :invalid-feedback="invalidFeedback"
                        :valid-feedback="validFeedback"
                        :state="state"
                        align="left"
                >
                    <b-form-input id="input-1" v-model="name" :state="state" trim></b-form-input>
                </b-form-group>
                <b-button @click="validate" squared variant="outline-primary" href="#map" class="mb-5 pr-5 pl-5">VALIDER</b-button>
            </b-col>
        </b-row>
    </div>
</template>

<script>

    // @ is an alias to /src
    export default {
        name: 'Home',

        computed: {
            state() {
                return this.name.length >= 4 ? true : false
            },
            invalidFeedback() {
                if (this.name.length > 4) {
                    return ''
                } else if (this.name.length > 0) {
                    return 'Enter a valid adress'
                } else {
                    return 'Please enter something'
                }
            },
            validFeedback() {
                return this.state === true ? 'Thank you' : ''
            }
        },
        data() {
            return {
                name: ''
            }
        },


        methods:{
            validate: function(){
                fetch("https://mailcheck.p.rapidapi.com/?disable_test_connection=false&domain="+this.name+"", {
                    "method": "GET",
                    "headers": {
                        "x-rapidapi-host": "mailcheck.p.rapidapi.com",
                        "x-rapidapi-key": "650499af09mshdaa27d7fcb79e32p114649jsn28455458fe22"
                    }
                })
                    .then(function (response) {
                        response.json()
                            .then(function (value) {
                                console.log(value);
                                let valid = value.valid;
                                if(valid == false){
                                    alert("Email invalide");
                                }else{
                                    alert("Email enregistré")
                                }

                            });

                    });
            }
            }
        }





</script>
<style>

    *{
        scroll-behavior: smooth;
    }

    #cards{
        margin-top: 50px;
    }

    #map{
        margin-top: 100px;
    }

    @media (max-width: 1199.98px) {
        iframe {
            margin: auto;
            width: 80%;
            height: 430px;
        }
    }


</style>
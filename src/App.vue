<script>
import axios from "axios"

export default {
    data() {
        return {
            city: '',
            error: '',
            info: null

        }
    },
    methods: {
        getWeather() {
            if (this.city.trim().length < 2) {
                this.error = "Немає таких міст"
                return false;
            }
            this.error = ""

            axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=cbd1a4ee007f3f3c2a7e8adaabe58c5a`)
                .then(res => (this.info = res.data))

        },
        isLetter(e) {
            let char = String.fromCharCode(e.keyCode); // Get the character
            if (/^[A-Za-z]+$/.test(char)) return true; // Match with regex 
            else e.preventDefault(); // If not match, don't add to input text
        }

    }

}
</script> 

<template>
<div class="wrapper">

    <h1>Weather app</h1>
    <h2>Дізнатись погоду в <span>{{ city== '' ? "вашому місті" : city }}</span></h2>
    <input v-model="city" v-on:keypress="isLetter($event)" type="text">
    <button @click="getWeather" class="submit" v-if="city!=''">Отримати погоду</button>
    <button disabled class="dis" v-else>Введіть місто</button>

    <p class="error"> {{ error }}</p>
    <p class="info" v-if="info != null">{{ info.main.temp }} ° </p>

</div>
</template>

<style scoped>
.error {
    color: red
}

body {
    font-family: Tilt Prism;
}

.info {
    margin-top: 70px;
    font-size: 50px;
}

span {
    color: rgb(0, 238, 255);
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
    letter-spacing: 2px;
}

.wrapper {
    padding: 20px;
    background: #062b44;
    width: 700px;
    height: 350px;
    border-radius: 40px;
    text-align: center;
    color: #fff;
    margin: 0 auto;
    opacity: 0.8;

}

.wrapper h1 {
    margin-top: 20px;
    font-size: 40px;

}

.wrapper h2 {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    margin-top: 20px;
    font-size: 14px;

}

.wrapper input {
    margin-top: 50px;
    background: transparent;
    border: 0;
    border-bottom: 2px solid #110813;
    font-size: 14px;
    padding: 5px 8px;
    outline: none;
}

input {

    color: #fff
}

.wrapper span {
    font-size: 20px;
}

.wrapper input:focus {
    border-bottom-color: #a07008;
}

.wrapper button {
    background: #e3bc4b;
    color: #fff;
    border-radius: 10px;
    border: 2px solid #b99935;
    padding: 10px 15px;
    margin-left: 20px;
    cursor: pointer;
    transition: transform 500ms ease;
}

.wrapper button:hover {
    transform: scale(1.1) translateY(-5px);
}

.wrapper button:disabled {
    background: #746027;
    cursor: not-allowed;
}

@media screen and (max-width: 600px) {
    .wrapper {
        width: 80%;
        height: 300px;
        font-size: 10px;
    }

    .submit {
        margin-top: 30px;
    }

    .dis {
        margin-top: 30px;
    }
}

@media screen and (min-width: 1500px) {
    .wrapper {
        scale: 1.5;
    }
}
</style>

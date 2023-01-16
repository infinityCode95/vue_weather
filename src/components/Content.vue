<template>
    <div class="content-wrap">
        <p class="content-title">Узнать погоду в  {{ textInput === '' ? 'вашем городе' : cityName}}</p>
        <input
            class="content-input" 
            type="text" 
            placeholder="Введите город"
            v-model="textInput"
        >
        <button class="content-btn" v-if="textInput" @click="getWeather">Узнать</button>

        <div class="error-wrap">
            <p class="error-text">{{ error }}</p>
        </div>

        <div class="info-wrap" v-if="info != null">
            <div class="info-temp">{{ showTemp }}</div>
            <ul class="info-list">
               <li class="info-item">Ощущается как: {{ showTFeelsLike }}</li>
               <li class="info-item">Минимальная температура: {{ showMinTemp }}</li>
               <li class="info-item">Максимальная температура: {{ showMaxTemp }}</li>
            </ul>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: 'Query',
    data: () => ({
        textInput: '',
        error: '',
        info: null
    }),
    watch: {
        textInput: 'clearInfo'
    },
    computed: {
        cityName() {
            return `«${this.textInput}»`;
        },
        showTemp() {
            return `${this.info.main.temp.toFixed()} ℃`;
        },
        showTFeelsLike() {
            return `${this.info.main.feels_like.toFixed()} ℃`;
        },  
        showMinTemp() {
            return `${this.info.main.temp_min.toFixed()} ℃`;
        },  
        showMaxTemp() {
            return `${this.info.main.temp_max.toFixed()} ℃`;
        },  
    },
    methods: {
        getWeather() {
            if (this.textInput.trim().length < 3) {
                this.error = 'Введите корректное название города';
            } else {
                this.error = '';
            }
                        
            axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.textInput}&units=metric&appid=e25d14c5ed65b96b30bd913f49888f1d`)
            .then(res => (this.info = res.data))
        },
        clearInfo() {
            if (this.textInput == '') {
                this.info = null
            }
        }
    }    
}
</script>

<style scoped>
.content-wrap {
    margin: 0 auto;
    padding: 1rem;
    max-width: 500px;
}
.content-title {
    margin: 0px 0px 40px 0px;
    font-size: 1.8rem;
    font-weight: 500;
}
.content-input {
    margin: 0px 20px 40px 0px;
    background: transparent;
    border: 0;
    border-bottom: 2px solid #000;
    height: 35px;
    font-size: 14px;
    padding: 5px 10px;
    outline: none;
}
.content-btn {
    padding: 9px;
    background-image: linear-gradient(to right, #f78ca0 0%, #f9748f 19%, #fd868c 60%, #fe9a8b 100%);
    font-weight: 500;
    border-radius: 7px;
    font-size: 14px;    
}

.content-btn:hover {
    transform: scale(1.1);
    transition: all 0.5s ease;
}

.info-wrap {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
}

.info-temp {
    background-image: linear-gradient(120deg, #fdfbfb 0%, #ebedee 100%);
    padding: 20px;
    width: 200px;
    margin:  0 auto;
    font-size: 30px;
    border-radius: 10px;
}
.info-item {
    margin: 0px 0px 13px 0px;
    text-align: left;
    font-size: 15px;
    background-color: #000;
    background-image: linear-gradient(to right, #f78ca0 0%, #f9748f 19%, #fd868c 60%, #fe9a8b 100%);
    color: #000;
    padding: 5px;
    border-radius: 10px;
    cursor: pointer;
}
.info-item:hover {
    transform: translateY(3px);
    transition: all 0.2s ease;
}
</style>
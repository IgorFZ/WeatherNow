<template>
    <section class="vh-100">
        <div class="container py-5 h-100">
          <Message :msg="msg"  v-show="msg"/>
          <div class="row d-flex justify-content-center align-items-center h-100">
            <div class="col-md-8 col-lg-6 col-xl-4">
      
              <h3 class="mb-4 pb-2 fw-normal">Check the weather forecast</h3>
      
              <div class="input-group rounded mb-3">
                <input v-model="adressSearch" type="search" class="form-control rounded" placeholder="City" aria-label="Search"
                  aria-describedby="search-addon" />
                <a href="#!" type="button" @click="updateAdress()" >
                  <span class="input-group-text border-0 fw-bold" id="search-addon">
                    Check!
                  </span>
                </a>
              </div>
      
              <div class="mb-4 pb-2">
                <div class="form-check form-check-inline" @click="setAdress()" >
                  <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio1"
                    value="option1" checked />
                  <label class="form-check-label" for="inlineRadio1">Celsius</label>
                </div>
      
                <div class="form-check form-check-inline" @click="setAdress()" >
                  <input class="form-check-input" type="radio" name="inlineRadioOptions" id="inlineRadio2"
                    value="option2" />
                  <label class="form-check-label" for="inlineRadio2">Farenheit</label>
                </div>
              </div>
      
              <div class="card shadow-0 border">
                <div class="card-body p-4">
      
                  <h4 id="city" class="mb-1 sfw-normal"> {{ location }} </h4>
                  <div class="details-weather">
                    <p class="mb-2rem">Current temperature: <strong id="current_temperature"> {{ current_temperature }} </strong></p>
                    <p class="mb-2rem">Feels Like: <strong id="feels_like"> {{ feels_like }} </strong></p>
                    <p class="mb-2rem">Wind(km/h): <strong id="wind"> {{ wind }} </strong></p>
                    <p class="mb-2rem">Humidity: <strong id="humidity"> {{ humidity }} </strong></p>
                    <p class="mb-3m">Local Time: <strong> {{ local_time }} </strong></p>
                    <div class="d-flex flex-row align-items-center">
                      <p id="condition" class="mb-0 me-4"> {{ condition }} </p>
                      <i class="weather-icon" style="color: #eee;"> <img :src="iconUrl"> </i>
                    </div>
                  </div>
      
                </div>
              </div>
      
            </div>
          </div>
      
        </div>
      </section>

</template>

<script>
import Message from './Message.vue';
export default {
  components: { Message },
    name: "CardWeather",
    data() {
        return {
            adressSearch: null,
            adress: 'auto:ip',
            location: null,
            res: {},
            current_temperature: null,
            feels_like: null,
            wind: null,
            humidity: null,
            condition: null,
            iconUrl: null,
            local_time: null,
            msg: null,
        }
    },
    methods: {
        async setAdress() {
            const options = {
                method: 'GET',
                url: 'https://weatherapi-com.p.rapidapi.com/current.json',
                params: {q: this.adress },
                headers: {
                    'X-RapidAPI-Key': 'dfb66a193fmshd7f636136140725p1d66e2jsnc813e6368d1e',
                    'X-RapidAPI-Host': 'weatherapi-com.p.rapidapi.com'
                }
            };

            var vm = this;

            axios.request(options).then(function (response) {
                vm.location =  `${response.data.location.name}, ${response.data.location.country}`;
                if (checkbox[0].checked == true) {
                    vm.current_temperature =`${response.data.current.temp_c}°C`;
                    vm.feels_like = `${response.data.current.feelslike_c}°C`;
                } else {
                    vm.current_temperature = `${response.data.current.temp_f}°F`;
                    vm.feels_like = `${response.data.current.feelslike_f}°F`;
                }
                
                vm.wind = `${response.data.current.wind_kph}km/h`;
                vm.humidity = `${response.data.current.humidity}%`;
                vm.condition = `${response.data.current.condition.text}`;

                //var iconUrl = `${response.data.current.condition.icon}`;
                vm.iconUrl = `${response.data.current.condition.icon}`;

                vm.local_time = `${(response.data.location.localtime).substr(10)}`
            });
            

            //this.adress = `${this.res.data.location.name}`;

            
        },
        async updateAdress() {
            const options = {
                method: 'GET',
                url: 'https://weatherapi-com.p.rapidapi.com/current.json',
                params: {q: this.adressSearch },
                headers: {
                    'X-RapidAPI-Key': 'dfb66a193fmshd7f636136140725p1d66e2jsnc813e6368d1e',
                    'X-RapidAPI-Host': 'weatherapi-com.p.rapidapi.com'
                }
            };

            var vm = this;

            axios.request(options).then(function (response) {
              vm.location =  `${response.data.location.name}, ${response.data.location.country}`;
              if (checkbox[0].checked == true) {
                  vm.current_temperature =`${response.data.current.temp_c}°C`;
                  vm.feels_like = `${response.data.current.feelslike_c}°C`;
              } else {
                  vm.current_temperature = `${response.data.current.temp_f}°F`;
                  vm.feels_like = `${response.data.current.feelslike_f}°F`;
              }
              
              vm.wind = `${response.data.current.wind_kph}km/h`;
              vm.humidity = `${response.data.current.humidity}%`;
              vm.condition = `${response.data.current.condition.text}`;

              //var iconUrl = `${response.data.current.condition.icon}`;
              vm.iconUrl = `${response.data.current.condition.icon}`;

              // Save Adress in Local Storage
              localStorage.adress = vm.adressSearch;
              // Save Adress Session
              vm.adress = vm.adressSearch;

            }).catch(function (error) {
              vm.msg = "Not Found!"
              // clear message
              setTimeout(() => vm.msg = "", 3000)
            });
        }
    },
    created() {
        if (localStorage.adress) {
            this.adress = localStorage.adress;
        } else {
            this.adress = 'auto:ip';
        }
        this.setAdress();
    }
}

let checkbox = document.getElementsByName('inlineRadioOptions');

</script>
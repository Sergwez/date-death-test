<template>
  <div class="wrapper">
     <div class="load" v-if="showLoading == true">
      <img class="load__img" src="@/assets/load.svg"/>
      <div class="load__text">Loading</div>
    </div>
    <div class="content" v-else>
    <div v-if="$route.query.step == 1" class="step1">
      <div class="step1__text">
        Мы расскажем Вам не только подробности<br> 
        вашей смерти, но также поможем Вам<br>
        избежать этой ужасной даты и продлить<br>
        вашу жизнь на многие годы.
      </div>
      <div class="step1__title">
        Когда Вы чувствуете себя наиболее комфортно?
      </div>
      <div class="step1__button-group">
        <router-link tag="button" to="?step=2" class="step1__button">Утро</router-link>
        <router-link tag="button" to="?step=2" class="step1__button">День</router-link>
        <router-link tag="button" to="?step=2" class="step1__button">Вечер</router-link>
        <router-link tag="button" to="?step=2" class="step1__button">Ночь</router-link>
      </div>
      <div class="step1__info">
        Вопрос 2-5
      </div>
    </div>
    <!-- -->
    <div class="step2" v-if="$route.query.step == 2">
      <div class="step2__text">
        Уже совсем скоро Вы узнаете много<br>
        интересного о своем будущем!
      </div>
      <div class="step2__title">
        Укажите свою дату рождения:
      </div>
      <div class="step2__button-group">
        <select @change="checkForm()" :class="{'step2__select-error': check.day == false}" class="step2__select" v-model="selectedDay">
          <option disabled selected>День</option>
          <option v-for="day in 31" :key="day">&nbsp;{{day}}</option>
        </select>
        <select @change="checkForm()" :class="{'step2__select-error': check.month == false}" class="step2__select" v-model="selectedMonth">
          <option disabled selected>Месяц</option>
          <option v-for="month of months" :key="month">{{month}}</option>
        </select>
        <select @change="checkForm()" :class="{'step2__select-error': check.year == false}" class="step2__select" v-model="selectedYear">
          <option disabled selected>Год</option>
          <option v-for="year of years" :key="year">{{year}}</option>
        </select>
        <div @click.capture="checkForm()">
        <router-link tag="button" to="?step=3" class="step2__button" :disabled="check.year==false||check.month==false||check.year==false">Далее</router-link>
        </div>
        <!-- Проверка на существование даты, например 30.02.2020 -  не существует -->
        <!--<div v-if="!checkDate">Такой даты не существует!</div>-->
      </div>
      <div class="step2__info">
        Вопрос 3-5
      </div>
    </div>
    <!-- -->
     <div v-if="$route.query.step == 3" class="step1">
      <div class="step3__text">
        Смерть родного человека – одно из<br>
        тяжелейших испытаний в жизни каждого<br>
        из нас!
      </div>
      <div class="step3__title">
        Снятся ли Вам умершие<br> люди?
      </div>
      <div class="step3__button-group">
        <router-link tag="button" to="?step=4" class="step3__button">Да</router-link>
        <router-link tag="button" to="?step=4" class="step3__button">Нет</router-link>
        <router-link tag="button" to="?step=4" class="step3__button">Иногда</router-link>
      </div>
      <div class="step3__info">
        Вопрос 4-5
      </div>
    </div>
    <!-- -->
    
    <div v-if="$route.query.step == 4" class="step1">
      <div class="step4__text">
        <div class="step4__text-quote" v-if="age() >= 18 && age() <= 35">
          По вам скучает очень близкий человек,<br>
          которого больше нет в мире живых.
        </div>
        <div class="step4__text-quote" v-if="age() >= 36 && age() <= 45">
          По вам скучает очень близкий человек,<br>
          которого больше нет в мире живых. <br>
          Возможно это дедушка или бабушка.
        </div>
        <div class="step4__text-quote" v-if="age() >= 45">
          По вам скучает очень близкий человек,<br>
          которого больше нет в мире живых.<br>
          Возможно это кто-то из Ваших родителей.
        </div>
        <div class="step4__text-quote" v-else>
          По вам скучает очень близкий человек,<br>
          которого больше нет в мире живых.
        </div>
      </div>
      <div class="step4__title">
        Запись, которую Вы услышите,<br>
        может шокировать людей с<br>
        неокрепшей психикой. Вы готовы<br>
        узнать, что ждет именно Вас?<br>
      </div>
      <div class="step4__button-group">
        <router-link tag="button" to="?step=5" class="step4__button">Да</router-link>
        <router-link tag="button" to="?step=5" class="step4__button">Затрудняюсь ответить</router-link>
      </div>
      <div class="step4__info">
        Вопрос 5-5
      </div>
    </div>
    <!-- -->
    <div class="recording" v-if="$route.query.step == 5">
      <img class="recording__img" src="@/assets/recording.svg">
      <div class="recording__indicator-full"></div>
      <div class="recording__indicator" v-bind:style="{width:currentTime * 2.6 + 'px'}"></div>
      <div class="recording__title">{{currentTime }}%</div>
      <div class="recording__text">Запись сообщения</div>
    </div>
    <!-- -->
    <div v-if="$route.query.step == 6" class="step1">
      <div class="step5__text">
        <div class="step5__text-quote">
          Спасибо за Ваши ответы!<br>
          <strong>
            Мы подготовили для Вас<br> 
            персональную аудио запись с <br>
            Вашим прогнозом.
          </strong>

        </div>
   
      </div>
      <div class="step5__subtitle">
        Вы можете узнать, как повлиять<br>
        на события, которые ожидают<br>
        вас в ближайшем будущем. 
      </div>
      <div class="step5__title">
        <span class="step5__title--uppercase">
        Первое значимое<br>
        событие может<br>
        произойти уже {{tomorrowDate}},<br>
        </span>
        Вам надо быть готовым, что<br>
        бы последствия не оказались<br>
        необратимыми.

      </div>
      <div class="step5__subtitle">
        Нажмите на кнопку ниже прямо<br>
        сейчас и наберите наш номер<br>
        телефона. Прослушайте важную<br>
        информацию!
      </div>
      <div class="step4__button-group">
         <button @click="req()"  class="step5__button">Позвонить и прослушать</button>
      </div>

    <!-- -->
       <div class="swapi" v-if="swapi">
       <div class="elem__row" v-for="(value, name) in swapi.data" :key="name">
         <div class="elem__name">{{name}}</div>
         <div class="elem__value">{{value}}</div>
       </div>
       </div>
    </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios'
export default {
  data(){
    return{
      months:['Январь',"Февраль","Март","Апрель","Май","Июнь","Июль","Август","Сентябрь","Октябрь","Ноябрь","Декабрь"],
      selectedDay:'День',
      selectedMonth:'Месяц',
      selectedYear:'Год',
      check:{
        day:true,
        month:true,
        year:true
      },
      showLoading:false,
      currentTime: 100,
      timer: null,
      swapi: null,
      urlApi:'https://swapi.dev/api/people/1/?format=json'
    }
  }, 
  computed:{
    years(){
      const curDate = new Date()
      const curYear = curDate.getFullYear()
      let arr = []
      for(let i = 0; i < 120; i++){
        arr[i] = curYear - i
      }
      return arr
    },
    checkDate(){
      let date = new Date(this.selectedYear, this.months.indexOf(this.selectedMonth), this.selectedDay);
      if (date.getFullYear() == this.selectedYear && date.getMonth() == this.months.indexOf(this.selectedMonth) && date.getDate() == this.selectedDay) {
        return true
      } else {
        return false
      }
    },
    tomorrowDate(){
      const date = new Date()
      date.setDate(date.getDate() + 1)
      return date.getDate() + "." + ('0'+ (date.getMonth() + 1)).slice(-2) + "." + date.getFullYear()
      
    }
  },
  methods:{
     checkForm(){
       if(this.selectedDay == 'День'){
         this.check.day = false
       } else{
         this.check.day = true
       }
       if(this.selectedMonth == 'Месяц'){
         this.check.month = false
       } else {
         this.check.month = true
       }
       if(this.selectedYear == 'Год'){
         this.check.year = false
       } else {
         this.check.year = true
       }
     },
     disableLoading(){
      this.showLoading = false
     },
     age(){
       const curDate = new Date()
       const curYear = curDate.getFullYear()
       if(curDate.getMonth() > this.months.indexOf(this.selectedMonth)){
         return curYear - this.selectedYear
       } else if(curDate.getMonth() == this.months.indexOf(this.selectedMonth)){
          if(curDate.getDate() >= this.selectedDay){
          return curYear - this.selectedYear
          } else{
            return curYear - this.selectedYear - +1
          }
       } else {
         return curYear - this.selectedYear - +1
       }
     },
     startRecording() {
       this.currentTime = 0
        this.timer = setInterval(() => {        
        this.currentTime++       
        if(this.currentTime == 100){
          clearTimeout(this.timer)
        }
      }, 40)
    },
    req(){
       axios
      .get(this.urlApi)
      .then(response => (this.swapi = response));
    }

       
  },
  watch:{
    $route: function () {
      if(this.$route.query.step != 5){
        this.showLoading = true
        setTimeout(this.disableLoading, 2000)
        this.age()
        console.log(this.age())
      } else{
        this.startRecording()
      }
    },
    currentTime: function(){
      if(this.currentTime == 100){
        this.$router.push('?step=6')
      }
     
    }
  },
  filters:{
  },
 
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .wrapper{
    width:320px;
    min-height:100vh;
    background: #202024;
    color: #ffffff;
    font-family: 'Roboto', sans-serif;
    text-align: center;
   
  }
  .step1__text, 
  .step2__text,
  .step3__text,
  .step4__text,
  .step5__text{
    height:102px;
    border-bottom:1px solid rgba(255,255,255, 0.2);
    font-family: 'Bad Script', cursive;
    font-size: 14px;
    line-height: 20px;
    padding:20px 0 0 0; 
    color:rgba(255,255,255, 0.6);
  }
  .step4__text-quote,
  .step5__text-quote{
    height:66px;
    border-bottom:1px solid rgba(255,255,255, 0.2);
    font-family: 'Bad Script', cursive;
    font-size: 14px;
    line-height: 20px;
    padding:20px 0 0 0;
    margin: 0px 30px 0 30px; 
    color:#202024;
    background: #ffffff;
    border-radius:5px;
  }
   .step5__text-quote{
     padding:5px 0 9px 0;
     font-family: 'Roboto', sans-serif;
    line-height: 18px;
    top:20px;
    border:none;
   }
   .step5__title{
     border:1px solid #ffffff;
     margin:20px 30px 18px 30px;
     border-radius: 5px; 
     padding:14px 0 8px 0;
     font-size: 16px;
    line-height: 25px;
    color: #F6C866;
   }
   .step5__title--uppercase{
     text-transform: uppercase;
     font-weight: bold;
   }
   .step5__subtitle{
    margin:8px 0 0 0;
    font-size: 14px;
    line-height: 16px;
   }
   .step3__text{
    height:87px;
    padding:9px 0 0px 0;
  }
  .step4__text::after{
    content: ''; 
    position: absolute; 
    margin:-1px 0 0 98px;
    border: 6px solid transparent; 
    border-top: 12px solid white; 
  }
  .step5__text::after{
    content: ''; 
    position: absolute; 
    margin:-1px 0 0 98px;
    border: 6px solid transparent; 
    border-top: 12px solid white; 
  }
  .step1__text::before, 
  .step2__text::before,
  .step3__text::before,
  .step4__text::before{
  content:"";
  width:63px;
  height: 70px;
  position: absolute;
  background: url("~@/assets/fifth-img-eye1.svg") no-repeat;
  margin:45px 0 0 192px;
  opacity: 0.2;
  }
   .step4__text::before{
      margin:45px 0 0 96px;
   }
  .step3__text::before{
    margin:30px 0 0 190px;
  }
  .step1__title, 
  .step2__title,
  .step3__title,
  .step4__title{
    text-transform: uppercase;
    margin:36px 0 0 0;
    color: #F6C866;
    font-size: 16px;
    line-height: 25px;
  }
  /* .step4__title{
    margin:50px 0 0 0;
    letter-spacing: -0.03em;
  } */
  .step1__button-group, 
  .step2__button-group,
  .step3__button-group,
  .step4__button-group{
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top:40px;
  }
  .step3__button-group{
    height:237px;
  }
  .step1__button, 
  .step2__button,
  .step3__button,
  .step4__button{
    width:180px;
    height:40px;
    outline: none;
    margin:0 0 20px 0;
    border-radius:20px;
    border: none;
    color:#ffffff;
    background-color: #e7a138;
    font-size: 14px;
    cursor:pointer;
  }
   .step5__button{
    width:238px;
    height:48px;
    outline: none;
    margin:-20px 0 20px 0;
    border-radius:30px;
    border: none;
    color:#ffffff;
    background: rgba(50, 185, 73, 0.9);
    font-size: 14px;
    cursor:pointer;
  }
  .step1__button:before, 
  .step2__button:before,
  .step3__button:before,
  .step3__button:before{
  content: "";
  width:87px;
  height: 40px;
  display: block;
  margin: -12px 0 0 -6px;
  position: absolute;
  background:linear-gradient(248.67deg, rgba(255, 255, 255, 0) 30.84%, rgba(255, 255, 255, 0.29) 46.06%, rgba(255, 255, 255, 0) 64.04%);
}
 .step5__button:before{
  content: "";
  width:87px;
  height: 48px;
  display: block;
  margin: -16px 0 0 -6px;
  position: absolute;
  background:linear-gradient(248.67deg, rgba(255, 255, 255, 0) 30.84%, rgba(255, 255, 255, 0.29) 46.06%, rgba(255, 255, 255, 0) 64.04%);
}
.step1__button:nth-of-type(2):before,
.step3__button:nth-of-type(2):before,
.step4__button:nth-of-type(2):before{
  margin: -12px 0 0 28px;
}
.step1__button:nth-of-type(3):before,
.step3__button:nth-of-type(3):before{
  margin: -12px 0 0 59px;
}
.step1__button:nth-of-type(4):before,
.step2__button:nth-of-type(1):before{
  margin: -12px 0 0 93px;
}
.step1__info,
.step2__info,
.step3__info,
.step4__info{
  margin:17px 0 0 0;
  height: 62px;
  font-size: 12px;
  line-height: 14px;
  color:rgba(255,255,255, 0.6);
  letter-spacing: 0.1em;
}
.step4__info{
  margin:87px 0 0 0;
}
.step1__info::before,
.step2__info::before,
.step3__info::before,
.step4__info::before{
  content:"";
  width:70px;
  height: 70px;
  position: absolute;
  background: url("~@/assets/fifth-img-eye2.svg") no-repeat;
  margin:-24px 0 0 -135px;
  opacity: 0.2;
}
.step2__select{
   width:180px;
    height:40px;
    outline: none;
    margin:0 0 20px 0;
    border-radius:20px;
    border: none;
    color: #202024;
    font-size: 14px;
    cursor:pointer;
    text-align: center;
    text-align-last: center; 
    appearance: none;
    background: url('~@/assets/arrow.svg') no-repeat 92% 50%, linear-gradient(90deg, rgba(228, 228, 228, 0.9) -6.2%, rgba(203, 203, 203, 0.9) 100%);
    box-shadow: inset 0px 4px 4px rgba(0, 0, 0, 0.25);
    appearance: none;
    padding: 0 10px;
}
.step2__select option{
  color: #202024;
  font-size: 14px;
}

.step2__select:focus option:disabled{
 display:none
}
.step2__select-error{
  border: 1px solid #EE5353;
}
.load{
  min-height:100vh;
  width:100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.load__text{
  margin:27px 0 0 0;
  font-size: 12px;
  letter-spacing: 0.1em;
  color: rgba(255, 255, 255, 0.6);
}
.load__img{
  width:73px;
  height:73px;
  animation-name: rotation;
  animation-duration: 1s;
  animation-iteration-count: infinite;
  animation-timing-function: steps(12, end);
}
.recording{
  min-height:100vh;
  width:100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.recording__title{
  margin:20px 0 0 0;
  font-weight:300;
  font-size: 20px;
  letter-spacing: 0.1em;
  color: rgba(255, 255, 255, 0.6);
}
.recording__text{
  font-size: 12px;
  margin:10px 0 0 0;
  letter-spacing: 0.1em;
   color: rgba(255, 255, 255, 0.6);
   font-weight:300;
}
.recording__indicator-full{
  background: #ffffff;
  height:4px;
  width:260px;
  align-self: start;
  margin:38px 0 0 30px;
}
.recording__indicator{
  background: #F6C866;
  align-self: start;
  margin:-4px 0 0 30px;
  height:4px;
}

/*Swapi*/
.elem__row{
  display: flex;
  text-align: start;
  padding:10px 5px;

}
.elem__row:nth-of-type(2n){
  background: #333333;
}
.elem__name{
  width: 30%;
}
.elem__value{
  width: 70%;
  font-size: 14px;;
  
}
@keyframes rotation {
    0% {
        transform:rotate(0deg);
    }
    100% {
        transform:rotate(360deg);
    }
}
</style>

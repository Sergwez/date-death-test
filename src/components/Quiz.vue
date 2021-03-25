<template>
  <div class="wrapper">
    <div class="load" v-if="showLoading == true">
      <img class="load__img" src="@/assets/load.svg" />
      <div class="load__text">Loading</div>
    </div>
    <div class="content" v-else>
      <div v-if="$route.query.step == 1" class="step1">
        <div class="step1__text">
          Мы расскажем Вам не только подробности вашей смерти, но также поможем
          Вам избежать этой ужасной даты и продлить вашу жизнь на многие годы.
        </div>
        <div class="step1__title">
          Когда Вы чувствуете себя наиболее комфортно?
        </div>
        <div class="step1__button-group">
          <router-link tag="button" to="?step=2" class="step1__button"
            >Утро</router-link
          >
          <router-link tag="button" to="?step=2" class="step1__button"
            >День</router-link
          >
          <router-link tag="button" to="?step=2" class="step1__button"
            >Вечер</router-link
          >
          <router-link tag="button" to="?step=2" class="step1__button"
            >Ночь</router-link
          >
        </div>
        <div class="step1__info">Вопрос 2-5</div>
      </div>
      <!-- -->
      <div class="step2" v-if="$route.query.step == 2">
        <div class="step2__text">
          Уже совсем скоро Вы узнаете много интересного о своем будущем!
        </div>
        <div class="step2__title">Укажите свою дату рождения:</div>
        <div class="step2__button-group">
          <select
            @change="checkForm()"
            :class="{ 'step2__select-error': check.day == false }"
            class="step2__select"
            v-model="selectedDay"
          >
            <option disabled selected>День</option>
            <option v-for="day in 31" :key="day">&nbsp;{{ day }}</option>
          </select>
          <select
            @change="checkForm()"
            :class="{ 'step2__select-error': check.month == false }"
            class="step2__select"
            v-model="selectedMonth"
          >
            <option disabled selected>Месяц</option>
            <option v-for="month of months" :key="month">{{ month }}</option>
          </select>
          <select
            @change="checkForm()"
            :class="{ 'step2__select-error': check.year == false }"
            class="step2__select"
            v-model="selectedYear"
          >
            <option disabled selected>Год</option>
            <option v-for="year of years" :key="year">{{ year }}</option>
          </select>
          <div @click.capture="checkForm()">
            <router-link
              tag="button"
              to="?step=3"
              class="step2__button"
              :disabled="
                check.year == false ||
                check.month == false ||
                check.year == false
              "
              >Далее</router-link
            >
          </div>
        </div>
        <div class="step2__info">Вопрос 3-5</div>
      </div>
      <!-- -->
      <div v-if="$route.query.step == 3" class="step1">
        <div class="step3__text">
          Смерть родного человека – одно из тяжелейших испытаний в жизни каждого
          из нас!
        </div>
        <div class="step3__title">Снятся ли Вам умершие люди?</div>
        <div class="step3__button-group">
          <router-link tag="button" to="?step=4" class="step3__button"
            >Да</router-link
          >
          <router-link tag="button" to="?step=4" class="step3__button"
            >Нет</router-link
          >
          <router-link tag="button" to="?step=4" class="step3__button"
            >Иногда</router-link
          >
        </div>
        <div class="step3__info">Вопрос 4-5</div>
      </div>
      <!-- -->

      <div v-if="$route.query.step == 4" class="step4">
        <div class="step4__text">
          <div class="step4__text-quote" v-if="age() <= 17 || !age()">
            По вам скучает очень близкий человек, которого больше нет в мире
            живых.
          </div>
          <div class="step4__text-quote" v-if="age() >= 18 && age() <= 35">
            По вам скучает очень близкий человек, которого больше нет в мире
            живых.
          </div>
          <div class="step4__text-quote2" v-if="age() >= 36 && age() <= 45">
            По вам скучает очень близкий человек, которого больше нет в мире
            живых. Возможно это дедушка или бабушка.
          </div>
          <div class="step4__text-quote2" v-if="age() >= 45">
            По вам скучает очень близкий человек, которого больше нет в мире
            живых. Возможно это кто-то из Ваших родителей.
          </div>
        </div>
        <div class="step4__title">
          Запись, которую Вы услышите, может шокировать людей с неокрепшей
          психикой. Вы готовы узнать, что ждет именно Вас?
        </div>
        <div class="step4__button-group">
          <router-link tag="button" to="?step=5" class="step4__button"
            >Да</router-link
          >
          <router-link tag="button" to="?step=5" class="step4__button"
            >Затрудняюсь ответить</router-link
          >
        </div>
        <div class="step4__info">Вопрос 5-5</div>
      </div>
      <!-- -->
      <div class="recording" v-if="$route.query.step == 5">
        <img class="recording__img" src="@/assets/recording.svg" />
        <div class="recording__indicator-full"></div>
        <div
          class="recording__indicator"
          v-bind:style="{ width: currentTime * 2.6 + 'px' }"
        ></div>
        <div class="recording__title">{{ currentTime }}%</div>
        <div class="recording__text">Запись сообщения</div>
      </div>
      <!-- -->
      <div v-if="$route.query.step == 6" class="step5">
        <div class="step5__text">
          <div class="step5__text-quote">
            Спасибо за Ваши ответы!<br>
            <span class="step5__text-quote--bold">
              Мы подготовили для Вас персональную аудио запись с Вашим
              прогнозом.
            </span>
          </div>
        </div>
        <div class="step5__subtitle">
          Вы можете узнать, как повлиять на события, которые ожидают вас в
          ближайшем будущем.
        </div>
        <div class="step5__title">
          <span class="step5__title--uppercase">
            Первое значимое событие может произойти уже {{ tomorrowDate }},
          </span>
          Вам надо быть готовым, что бы последствия не оказались необратимыми.
        </div>
        <div class="step5__subtitle">
          Нажмите на кнопку ниже прямо сейчас и наберите наш номер телефона.
          Прослушайте важную информацию!
        </div>
        <div class="step5__button-group">
          <button @click="req()" class="step5__button">
            Позвонить и прослушать
          </button>
        </div>

        <!-- -->
        <div class="swapi" v-if="swapi">
          <div
            class="elem__row"
            v-for="(value, name) in swapi.data"
            :key="name"
          >
            <div class="elem__name">{{ name }}</div>
            <div class="elem__value">{{ value }}</div>
          </div>
        </div>
        <!-- -->
        <div class="footer" @click="changeHeightFooter()" v-bind:style="{ height: heightFooter}">
          TERMENI SI CONDITII: ACESTA ESTE UN SERVICIU DE DIVERTISMENT. PRIN FOLOSIREA LUI DECLARATI CA AVETI 18 ANI IMPLINITI, 
          </div>
        <!-- -->
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      months: [
        "Январь",
        "Февраль",
        "Март",
        "Апрель",
        "Май",
        "Июнь",
        "Июль",
        "Август",
        "Сентябрь",
        "Октябрь",
        "Ноябрь",
        "Декабрь",
      ],
      selectedDay: "День",
      selectedMonth: "Месяц",
      selectedYear: "Год",
      check: {
        day: true,
        month: true,
        year: true,
      },
      showLoading: false,
      currentTime: 100,
      timer: null,
      swapi: null,
      urlApi: "https://swapi.dev/api/people/1/?format=json",
      heightFooter: '2.58em'
    };
  },
  computed: {
    years() {
      const curDate = new Date();
      const curYear = curDate.getFullYear();
      let arr = [];
      for (let i = 0; i < 120; i++) {
        arr[i] = curYear - i;
      }
      return arr;
    },
    tomorrowDate() {
      const date = new Date();
      date.setDate(date.getDate() + 1);
      return (
        date.getDate() +
        "." +
        ("0" + (date.getMonth() + 1)).slice(-2) +
        "." +
        date.getFullYear()
      );
    },
  },
  methods: {
    checkForm() {
      if (this.selectedDay == "День") {
        this.check.day = false;
      } else {
        this.check.day = true;
      }
      if (this.selectedMonth == "Месяц") {
        this.check.month = false;
      } else {
        this.check.month = true;
      }
      if (this.selectedYear == "Год") {
        this.check.year = false;
      } else {
        this.check.year = true;
      }
    },
    disableLoading() {
      this.showLoading = false;
    },
    age() {
      const curDate = new Date();
      const curYear = curDate.getFullYear();
      if (curDate.getMonth() > this.months.indexOf(this.selectedMonth)) {
        return curYear - this.selectedYear;
      } else if (
        curDate.getMonth() == this.months.indexOf(this.selectedMonth)
      ) {
        if (curDate.getDate() >= this.selectedDay) {
          return curYear - this.selectedYear;
        } else {
          return curYear - this.selectedYear - +1;
        }
      } else {
        return curYear - this.selectedYear - +1;
      }
    },
    startRecording() {
      this.currentTime = 0;
      this.timer = setInterval(() => {
        this.currentTime++;
        if (this.currentTime == 100) {
          clearTimeout(this.timer);
        }
      }, 40);
    },
    req() {
      axios.get(this.urlApi).then((response) => (this.swapi = response));
    },
    changeHeightFooter(){
      if(this.heightFooter == '2.58em'){
        this.heightFooter = 'auto'
      } else{
        this.heightFooter = '2.58em'
      }
    }
  },
  watch: {
    $route: function () {
      if (this.$route.query.step != 5) {
        this.showLoading = true;
        setTimeout(this.disableLoading, 2000);
        this.age();
        //console.log(this.age());
      } else {
        this.startRecording();
      }
    },
    currentTime: function () {
      if (this.currentTime == 100) {
        this.$router.push("?step=6");
      }
    },
  },
  filters: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wrapper {
  width: 320px;
  min-height: 100vh;
  background: #202024;
  color: #ffffff;
  font-family: "Roboto", sans-serif;
  text-align: center;
}

/*-----step1------*/
.step1{
  background: url("~@/assets/fifth-img-eye1.svg") no-repeat, url("~@/assets/fifth-img-eye2.svg") no-repeat;
  background-position: 110% 14%, -5% 93%;
}
.step1__text {
  height: 102px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  font-family: "Bad Script", cursive;
  font-size: 14px;
  line-height: 20px;
  padding: 20px 43px 0 43px;
  color: rgba(255, 255, 255, 0.6);
  letter-spacing: -0.01em;
}
.step1__title {
  text-transform: uppercase;
  margin: 36px 0 0 0;
  color: #f6c866;
  font-size: 16px;
  line-height: 25px;
  padding: 0 15px 0 15px;
}
.step1__button-group {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 40px;
}
.step1__button {
  width: 180px;
  height: 40px;
  outline: none;
  margin: 0 0 20px 0;
  border-radius: 20px;
  border: none;
  color: #ffffff;
  background-color: #e7a138;
  font-size: 14px;
  cursor: pointer;
}
.step1__button:before {
  content: "";
  width: 87px;
  height: 40px;
  display: block;
  margin: -12px 0 0 -6px;
  position: absolute;
  background: linear-gradient(
    248.67deg,
    rgba(255, 255, 255, 0) 30.84%,
    rgba(255, 255, 255, 0.29) 46.06%,
    rgba(255, 255, 255, 0) 64.04%
  );
}
.step1__button:nth-of-type(2):before {
  margin: -12px 0 0 28px;
}
.step1__button:nth-of-type(3):before {
  margin: -12px 0 0 59px;
}
.step1__button:nth-of-type(4):before {
  margin: -12px 0 0 93px;
}
.step1__info {
  margin: 17px 0 0 0;
  height: 62px;
  font-size: 12px;
  line-height: 14px;
  color: rgba(255, 255, 255, 0.6);
  letter-spacing: 0.1em;
}
/*-----step2------*/
 .step2{
  background: url("~@/assets/fifth-img-eye1.svg") no-repeat, url("~@/assets/fifth-img-eye2.svg") no-repeat;
  background-position: 110% 14%, -5% 93%;
}
.step2__text {
  height: 77px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  font-family: "Bad Script", cursive;
  font-size: 14px;
  line-height: 20px;
  padding: 46px 43px 0 43px;
  color: rgba(255, 255, 255, 0.6);
  letter-spacing: -0.01em;
}
.step2__title {
  text-transform: uppercase;
  margin: 36px 0 0 0;
  color: #f6c866;
  font-size: 16px;
  line-height: 25px;
  padding: 0 43px 0 43px;
}
.step2__button-group {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 40px;
}
.step2__button {
  width: 180px;
  height: 40px;
  outline: none;
  margin: 0 0 20px 0;
  border-radius: 20px;
  border: none;
  color: #ffffff;
  background-color: #e7a138;
  font-size: 14px;
  cursor: pointer;
}
.step2__button:before {
  content: "";
  width: 87px;
  height: 40px;
  display: block;
  margin: -12px 0 0 -6px;
  position: absolute;
  background: linear-gradient(
    248.67deg,
    rgba(255, 255, 255, 0) 30.84%,
    rgba(255, 255, 255, 0.29) 46.06%,
    rgba(255, 255, 255, 0) 64.04%
  );
}
.step2__button:nth-of-type(1):before {
  margin: -12px 0 0 93px;
}
.step2__info {
  margin: 17px 0 0 0;
  height: 62px;
  font-size: 12px;
  line-height: 14px;
  color: rgba(255, 255, 255, 0.6);
  letter-spacing: 0.1em;
}
.step2__select {
  width: 180px;
  height: 40px;
  outline: none;
  margin: 0 0 20px 0;
  border-radius: 20px;
  border: none;
  color: #202024;
  font-size: 14px;
  cursor: pointer;
  text-align: center;
  text-align-last: center;
  appearance: none;
  background: url("~@/assets/arrow.svg") no-repeat 92% 50%,
    linear-gradient(
      90deg,
      rgba(228, 228, 228, 0.9) -6.2%,
      rgba(203, 203, 203, 0.9) 100%
    );
  box-shadow: inset 0px 4px 4px rgba(0, 0, 0, 0.25);
  appearance: none;
  padding: 0 10px;
}
.step2__select option {
  color: #202024;
  font-size: 14px;
}
.step2__select:focus option:disabled {
  display: none;
}
.step2__select-error {
  border: 1px solid #ee5353;
}
/*-----step3------*/
.step3{
  background: url("~@/assets/fifth-img-eye1.svg") no-repeat, url("~@/assets/fifth-img-eye2.svg") no-repeat;
  background-position: 110% 14%, -5% 93%;
}
.step3__text {
  height: 88px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  font-family: "Bad Script", cursive;
  font-size: 14px;
  line-height: 20px;
  padding: 34px 43px 0 43px;
  color: rgba(255, 255, 255, 0.6);
  letter-spacing: -0.00em;
}
.step3__title {
  text-transform: uppercase;
  margin: 36px 0 0 0;
  color: #f6c866;
  font-size: 16px;
  line-height: 25px;
  padding: 0 31px 0 31px;
}
.step3__button-group {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 40px;
  height: 237px;
}
.step3__button {
  width: 180px;
  height: 40px;
  outline: none;
  margin: 0 0 20px 0;
  border-radius: 20px;
  border: none;
  color: #ffffff;
  background-color: #e7a138;
  font-size: 14px;
  cursor: pointer;
}
.step3__button:before {
  content: "";
  width: 87px;
  height: 40px;
  display: block;
  margin: -12px 0 0 -6px;
  position: absolute;
  background: linear-gradient(
    248.67deg,
    rgba(255, 255, 255, 0) 30.84%,
    rgba(255, 255, 255, 0.29) 46.06%,
    rgba(255, 255, 255, 0) 64.04%
  );
}
.step3__button:nth-of-type(2):before {
  margin: -12px 0 0 28px;
}
.step3__button:nth-of-type(3):before {
  margin: -12px 0 0 59px;
}
.step3__info {
  margin: 19px 0 0 0;
  height: 62px;
  font-size: 12px;
  line-height: 14px;
  color: rgba(255, 255, 255, 0.6);
  letter-spacing: 0.1em;
}

/*-----step4------*/
.step4{
  background: url("~@/assets/fifth-img-eye1.svg") no-repeat, url("~@/assets/fifth-img-eye2.svg") no-repeat;
  background-position: 110% 14%, -5% 93%;
}
.step4__text {
  height: 100px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  font-family: "Bad Script", cursive;
  font-size: 14px;
  line-height: 20px;
  padding: 22px 30px 0 30px;
  color: rgba(255, 255, 255, 0.6);
}
.step4__text-quote {
  height: 62px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  font-family: "Bad Script", cursive;
  font-size: 14px;
  line-height: 20px;
  padding: 23px 12px 0 12px;
  letter-spacing: -0.01em;;
  color: #202024;
  opacity: 0;
  background: #ffffff;
  border-radius: 5px;
  animation-name: show;
  animation-duration: 1s;
  animation-delay: 1s;
  animation-fill-mode: forwards;
}
.step4__text-quote2{
  height: 72px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  font-family: "Bad Script", cursive;
  font-size: 14px;
  line-height: 20px;
  padding: 13px 12px 0 12px;
  letter-spacing: -0.01em;;
  color: #202024;
  background: #ffffff;
  border-radius: 5px;
  opacity: 0;
  animation-name: show;
  animation-duration: 1s;
  animation-delay: 1s;
  animation-fill-mode: forwards;
}
.step4__text::after {
  content: "";
  position: absolute;
  margin: -1px 0 0 98px;
  border: 6px solid transparent;
  border-top: 12px solid white;
  opacity: 0;
  animation-name: show;
  animation-duration: 1s;
  animation-delay: 1s;
  animation-fill-mode: forwards;
}
.step4__title {
  text-transform: uppercase;
  margin: 36px 0 0 0;
  color: #f6c866;
  font-size: 16px;
  line-height: 25px;
  padding: 0 9px 0 9px;
}
.step4__button-group {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 37px;
}
.step4__button {
  width: 180px;
  height: 40px;
  outline: none;
  margin: 0 0 20px 0;
  border-radius: 20px;
  border: none;
  color: #ffffff;
  background-color: #e7a138;
  font-size: 14px;
  cursor: pointer;
}
.step4__button:before {
  content: "";
  width: 87px;
  height: 40px;
  display: block;
  margin: -12px 0 0 -6px;
  position: absolute;
  background: linear-gradient(
    248.67deg,
    rgba(255, 255, 255, 0) 30.84%,
    rgba(255, 255, 255, 0.29) 46.06%,
    rgba(255, 255, 255, 0) 64.04%
  );
}
.step4__button:nth-of-type(2):before {
  margin: -12px 0 0 78px;
}
.step4__info {
  margin: 87px 0 0 0;
  height: 62px;
  font-size: 12px;
  line-height: 14px;
  color: rgba(255, 255, 255, 0.6);
  letter-spacing: 0.1em;
}
/*-----step5------*/
.step5__text {
  height: 102px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
  font-family: "Bad Script", cursive;
  font-size: 14px;
  line-height: 20px;
  padding: 24px 30px 0 30px;
  color: rgba(255, 255, 255, 0.6);
}
.step5__text-quote {
  height: 68px;
  font-family: "Roboto", sans-serif;
  font-size: 14px;
  line-height: 18px;
  padding: 7px 13px 9px 14px;
  color: #202024;
  background: #ffffff;
  border-radius: 5px;
  top: 20px;
  opacity: 0;
  animation-name: show;
  animation-duration: 1s;
  animation-delay: 1s;
  animation-fill-mode: forwards;
}
.step5__text-quote--bold{
  font-weight: bold;
}
.step5__title {
  border: 1px solid #ffffff;
  margin: 20px 30px 20px 30px;
  border-radius: 5px;
  padding: 13px 15px 8px 15px;
  font-size: 16px;
  line-height: 25px;
  color: #f6c866;
}
.step5__title--uppercase {
  text-transform: uppercase;
  font-weight: bold;
}
.step5__subtitle {
  margin: 11px 0 0 0;
  padding:0 51px 0 51px;
  font-size: 14px;
  line-height: 16px;
  font-weight: 300;
}
.step5__text::after {
  content: "";
  position: absolute;
  margin: -1px 0 0 98px;
  border: 6px solid transparent;
  border-top: 12px solid white;
  opacity: 0;
  animation-name: show;
  animation-duration: 1s;
  animation-delay: 1s;
  animation-fill-mode: forwards;
}
.step5__button {
  width: 238px;
  height: 48px;
  outline: none;
  margin: 20px 0 20px 0;
  border-radius: 30px;
  border: none;
  color: #ffffff;
  background: rgba(50, 185, 73, 0.9);
  font-size: 14px;
  cursor: pointer;
}
.step5__button:before {
  content: "";
  width: 87px;
  height: 48px;
  display: block;
  margin: -16px 0 0 -6px;
  position: absolute;
  background: linear-gradient(
    248.67deg,
    rgba(255, 255, 255, 0) 30.84%,
    rgba(255, 255, 255, 0.29) 46.06%,
    rgba(255, 255, 255, 0) 64.04%
  );
}
/*-----load------*/
.load {
  min-height: 100vh;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.load__text {
  margin: 27px 0 0 0;
  font-size: 12px;
  letter-spacing: 0.1em;
  color: rgba(255, 255, 255, 0.6);
}
.load__img {
  width: 73px;
  height: 73px;
  animation-name: rotation;
  animation-duration: 1s;
  animation-iteration-count: infinite;
  animation-timing-function: steps(12, end);
}
/*-----recoding------*/
.recording {
  min-height: 100vh;
  width: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.recording__title {
  margin: 20px 0 0 0;
  font-weight: 300;
  font-size: 20px;
  letter-spacing: 0.1em;
  color: rgba(255, 255, 255, 0.6);
}
.recording__text {
  font-size: 12px;
  margin: 10px 0 0 0;
  letter-spacing: 0.1em;
  color: rgba(255, 255, 255, 0.6);
  font-weight: 300;
}
.recording__indicator-full {
  background: #ffffff;
  height: 4px;
  width: 260px;
  align-self: start;
  margin: 38px 0 0 30px;
}
.recording__indicator {
  background: #f6c866;
  align-self: start;
  margin: -4px 0 0 30px;
  height: 4px;
}
/*-----swapi------*/
.elem__row {
  display: flex;
  text-align: start;
  padding: 10px 5px;
}
.elem__row:nth-of-type(2n) {
  background: #333333;
}
.elem__name {
  width: 30%;
}
.elem__value {
  width: 70%;
  font-size: 14px;
}
/*-----footer------*/
.footer{
  font-size: 7px;
  line-height: 1.29em;
  letter-spacing: 3px;
  margin: 0 13px 50px 13px;
  overflow: hidden;
}
@media (min-width:1440px) {
 .wrapper{
   width: 1420px;
 } 
 .step1{
  background: url("~@/assets/fifth-img-eye1.svg") no-repeat, url("~@/assets/fifth-img-eye2.svg") no-repeat;
  background-position: 90% 10%, 15% 100%;
  background-size: 150px 80px, 80px 80px;
}
 .step1__text {
  height: 122px;
  font-size: 20px;
  line-height: 35px;
  padding: 40px 243px 0 243px;
  letter-spacing: -0.01em;
}
.step1__text::before{
  width:150px;
  height:80px;
  background-size: contain;
  margin:20px 0 0 900px;
}
.step1__title{
  margin: 36px 0 0 0;
  font-size: 25px;
  line-height: 35px;
}
 .step1__button{
   width:315px;
   height:70px;
   border-radius:35px;
   font-size:20px;
   margin: 20px 0 20px 0;
 }
 .step1__button:before {
  width: 130px;
  height: 70px;
  margin: -24px 0 0 8px;
}
.step1__button:nth-of-type(2):before {
  margin: -24px 0 0 58px;
}
.step1__button:nth-of-type(3):before {
  margin: -24px 0 0 108px;
}
.step1__button:nth-of-type(4):before {
  margin: -24px 0 0 158px;
}
.step1__info{
  font-size: 16px;
  font-weight: 300;
}
.step1__info::before {
  width: 80px;
  height: 80px;
  margin: -24px 0 0 -425px;
  background-size: contain;
}
/**/
.step2{
  background: url("~@/assets/fifth-img-eye1.svg") no-repeat, url("~@/assets/fifth-img-eye2.svg") no-repeat;
  background-position: 90% 10%, 15% 100%;
  background-size: 150px 80px, 80px 80px;
}
 .step2__text {
  height: 102px;
  font-size: 20px;
  line-height: 35px;
  padding: 40px 243px 0 243px;
  letter-spacing: -0.01em;
}
.step2__title{
  margin: 36px 0 0 0;
  font-size: 25px;
  line-height: 35px;
}
 .step2__button{
   width:315px;
   height:70px;
   border-radius:35px;
   font-size:20px;
 }
 .step2__button:before {
  width: 130px;
  height: 70px;
}
.step2__button:nth-of-type(1):before {
  margin: -24px 0 0 163px;
}
.step2__select {
  width: 315px;
  height: 70px;
  margin: 20px 0 20px 0;
  border-radius: 35px;
  font-size: 20px;
  padding: 0 10px;
}
.step2__select:last-of-type{
  margin:20px 0 40px 0;
}
.step2__select option {
  color: #202024;
  font-size: 20px;
}
.step2__select:focus option:disabled {
  display: none;
}
.step2__select-error {
  border: 1px solid #ee5353;
}
.step2__info{
  font-size: 16px;
  font-weight: 300;
}
/*  */
.step3{
  background: url("~@/assets/fifth-img-eye1.svg") no-repeat, url("~@/assets/fifth-img-eye2.svg") no-repeat;
  background-position: 90% 10%, 15% 100%;
  background-size: 150px 80px, 80px 80px;
}
.step3__text {
  height: 88px;
  font-size: 20px;
  line-height: 35px;
}
.step3__title {
  margin: 36px 0 0 0;
  font-size: 25px;
  line-height: 35px;
}
.step3__button-group {
  margin-top: 40px;
}
.step3__button {
  width: 315px;
  height: 70px;
  outline: none;
  margin: 20px 0 20px 0;
  padding:20px 0 20px 0;
  border-radius: 35px;
  font-size: 20px;
}
.step3__button:before {
  width: 130px;
  height: 60px;
  margin: -19px 0 0 30px;
  position: absolute;
}
.step3__button:nth-of-type(2):before {
  margin: -19px 0 0 90px;
}
.step3__button:nth-of-type(3):before {
  margin: -19px 0 0 140px;
}
.step3__info {
  font-size: 16px;
  font-weight:300;
  margin:100px 0 0 0;
}
/*  */
.step4{
  background: url("~@/assets/fifth-img-eye1.svg") no-repeat, url("~@/assets/fifth-img-eye2.svg") no-repeat;
  background-position: 90% 10%, 15% 100%;
  background-size: 150px 80px, 80px 80px;
}
.step4__text {
  height: 140px;
  padding: 22px 430px 0 430px;
}
.step4__text-quote {
  height: 82px;
  line-height: 25px;
  font-size: 20px;
  padding: 33px 12px 0 12px;
  letter-spacing: -0.01em;
}
.step4__text-quote2{
  height: 82px;
  font-size: 20px;
  line-height: 25px;
  padding: 33px 12px 0 12px;
  letter-spacing: -0.01em;
}
.step4__text::after {
  margin: -1px 0 0 198px;
}
.step4__title {
  font-size: 25px;
  line-height: 35px;
  padding: 0 200px 0 200px;
}
.step4__button {
  width: 315px;
  height: 70px;
  margin: 20px 0 20px 0;
  border-radius: 35px;
  font-size: 20px;
}
.step4__button:before {
  width: 130px;
  height: 70px;
  margin: -24px 0 0 -6px;
}
.step4__button:nth-of-type(2):before {
  margin: -24px 0 0 148px;
}
.step4__info {
  font-size: 16px;
  font-weight:300;
}
/*  */
.step5{
  display:flex;
  flex-direction: column;
  align-items: center;
}
.step5__text{
  border:none;
}
.step5__text-quote {
  height: 100px;
  width:446px;
  font-size: 25px;
  line-height: 35px;
  padding: 11px 17px 53px 17px;
}
.step5__text-quote--bold{
  font-weight: bold;
}
.step5__title {
  width:378px;
  border-radius: 5px;
  padding: 63px 50px 46px 50px;
  font-size: 25px;
  line-height: 35px;
  color: #f6c866;
  margin:20px 0 -65px 0;
}
.step5__title--uppercase {
  text-transform: uppercase;
  font-weight: 400;
}
.step5__subtitle {
  margin: 97px 0 17px 0;
  width:422px;
  font-size: 25px;
  line-height: 35px;
  font-weight: 300;
}
.step5__subtitle:nth-of-type(4) {
  width:470px;
  margin:97px 0 18px 0;
}

.step5__text::after {
  content: "";
  position: absolute;
  margin: -1px 0 0 180px;
  border: 12px solid transparent;
  border-top: 20px solid white;
}
.step5__button {
  width: 390px;
  height: 80px;
  outline: none;
  margin: 18px 0 40px 0;
  border-radius: 40px;
  border: none;
  color: #ffffff;
  background: rgba(50, 185, 73, 0.9);
  font-size: 25px;
  cursor: pointer;
}
.step5__button:before {
  content: "";
  width: 150px;
  height: 80px;
  display: block;
  margin: -26px 0 0 -6px;
  position: absolute;
  background: linear-gradient(
    248.67deg,
    rgba(255, 255, 255, 0) 30.84%,
    rgba(255, 255, 255, 0.29) 46.06%,
    rgba(255, 255, 255, 0) 64.04%
  );
}
/*  */
.recording__indicator-full {
  margin: 38px 0 0 580px;
}
.recording__indicator {
  margin: -4px 0 0 580px;
}
/*  */
.footer{
  width:488px;
  font-size: 12px;
  line-height: 18px;
  color: #9D9D9D;
  margin: 0 0 5px 0;
}
}
@keyframes rotation {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
@keyframes show{
0%{
opacity:0;
}
100% {
opacity:1;
}
}

</style>

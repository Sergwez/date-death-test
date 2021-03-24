<template>
  <div class="wrapper">
    <div class="first-screen">
      <div class="first-screen__title">
        Лучшие астрологи и экстрасенсы Румынии
      </div>
      <div class="first-screen__subtitle">Точность прогноза: 97%</div>
      <div class="first-screen__img"></div>
      <div class="first-screen__question">
        Вас беспокоит вопрос о том, <br />
        <span class="first-screen__question--uppercase">
          когда Вы покинете этот Мир и <br> при каких обстоятельствах?
        </span>
      </div>
    
      <router-link tag="button" to="?step=1" class="first-screen__button">Да</router-link>
      <router-link tag="button" to="?step=1" class="first-screen__button">Нет</router-link>
      
      <div class="first-screen__text">Онлайн предсказание</div>
    </div>
    <!-- -->
    <div class="second-screen">
      <div class="second-screen__img">
      </div>
      <div class="second-screen__text">
        Позвольте нам раскрыть<br>
         эту волнующую тайну и <br>
        <span class="second-screen__text--bold">
          с точностью <br> определить дату и <br> время вашей смерти,<br>
        </span> 
        а также предшествующую <br> этому событию причину
      </div>
    </div>
    <!-- -->
    <div class="third-screen">
      <div class="third-screen__text">
        Многие не верят<br>предсказаниям и мы<br>решили доказать каждому,<br>
        <span class="third-screen__text--bold">что прогноз может<br>изменить жизнь<br>любого человека!</span>
      </div>
    </div>
    <!-- -->
    <div class="fourth-screen">
      <div class="fourth-screen__title">
        Боитесь ли вы умереть?
      </div>
      <router-link tag="button" class="fourth-screen__button" to="?step=1">Да</router-link>
      <router-link tag="button" class="fourth-screen__button" to="?step=1">Нет</router-link>

      <div class="fourth-screen__text">Вопрос 1-5</div>
    </div>
    <!-- -->
    <div class="fifth-screen">
      <img class="fifth-screen__img-top" src="@/assets/fifth-img1.svg">
      <div class="fifth-screen__text">
        Вы, конечно, умрете. <br>
        И все, с кем вы знакомы, <br>
        тоже однажды умрут.<br>
      </div>
      <img class="fifth-screen__img-bottom" src="@/assets/fifth-img2.svg">
    </div>
    <!-- -->
    <div class="footer">
      <div class="footer__text">
        TERMENI SI CONDITII: ACESTA ESTE UN SERVICIU DE DIVERTISMENT. PRIN FOLOSIREA LUI DECLARATI CA AVETI 18 ANI IMPLINITI, 
      </div>
    </div>
  </div>
</template>
<script>

export default {


}
</script>
<style scoped>

.wrapper {
  background: #202024;
  color: #ffffff;
  width:320px;
  font-family: 'Roboto', sans-serif;
  text-align: center;
}
.first-screen{
  background-image: url('~@/assets/main-bg.png');
  background-repeat: no-repeat;
  background-position: 0% -5%;
}
.first-screen__title{
  color:rgba(255, 255, 255, 0.6);
  font-size: 12px;
  letter-spacing: 0.1em;
  padding: 15px 0 7px 0;
  border-bottom:1px solid rgba(255, 255, 255, 0.2);
}
.first-screen__subtitle{
  font-size: 20px;
  color: rgba(255, 255, 255, 0.6);
  letter-spacing: 0.1em;
  font-weight: 300;
  line-height: 23px;
  margin: 7px 0 0 0;
}
.first-screen__img{
  margin:18px 0 -24px 47px;
  width:225px;
  height:225px;
  background-image: url('~@/assets/woman.png');
  
}

.first-screen__question{
  font-size: 16px;
  color:#F6C866;
  margin: 19px 0 0 0;
  line-height: 25px;
}

.first-screen__question--uppercase {
  text-transform: uppercase;
}
.first-screen__button{
  width:180px;
  height: 40px;
  margin: 23px 0 0 0;
  border-radius: 20px;
  border: none;
  background-color: #e7a138;
  color:#ffffff;
  font-size: 14px;
  cursor:pointer;
  outline: none;
  }
.first-screen__button:before{
  content: "";
  width:87px;
  height: 40px;
  display: block;
  margin: -12px 0 0 -6px;
  position: absolute;
  background:linear-gradient(248.67deg, rgba(255, 255, 255, 0) 30.84%, rgba(255, 255, 255, 0.29) 46.06%, rgba(255, 255, 255, 0) 64.04%);
}
.first-screen__button:last-of-type:before{
  margin: -12px 0 0 93px;
}
.first-screen__button:last-of-type{
  margin: 20px 0 0 0;
}
.first-screen__text{
  font-size: 12px;
  color: rgba(255, 255, 255, 0.6);
  font-weight: 300;
  line-height: 14px;
  margin: 20px 0 0 0;
  letter-spacing: 0.1em;
}
.second-screen{
  display:flex;
  flex-direction: column;
  align-items: center;
}
.second-screen__img{
  background-image: url('~@/assets/second-screen-bg.png');
  width:78px;
  height: 78px;
  background-position-x: 54%;
  border-radius: 39px;
  margin:38px 0 0 0;
  z-index: 1;
}
.second-screen__text{
  width:254px;
  border: 1px solid #FFFFFF;
  margin:-38px 33px 0 33px;
  border-radius: 3px;
  padding:47px 0 28px 0;
  font-size: 16px;
  line-height: 25px;
}
.second-screen__text--bold{
  font-size: 20px;
  line-height: 23px;
  color: #F6C866;
  font-weight: 600;
}
.third-screen{
  width:320px;
  height: 331px;
  margin:40px 0 0 0;
}
.third-screen__text::before{
  content: '';
  position: absolute;
  margin:-108px 0 0 -99px;
  width:321px;
  height: 331px;
  background-image: url('~@/assets/third-screen-bg.png');
  background-position: 50%;
  opacity: 0.2;
}
.third-screen__text{
  width:100%;
  height:100%;
  margin: 148px 0 0 0;
  line-height: 25px;
  font-size: 16px;
}
.third-screen__text--bold{
  font-size: 20px;
  line-height: 23px;
  color:#F6C866;
}
.fourth-screen__title{
  font-size: 16px;
  line-height: 19px;
  margin: -54px 0 0 0;
  text-transform: uppercase;
  color: #F6C866;
}
.fourth-screen__button{
  width:180px;
  height: 40px;
  margin: 26px 0 0 0;
  border-radius: 20px;
  border: none;
  background-color: #e7a138;
  color:#ffffff;
  font-size: 14px;
  cursor:pointer;
  outline: none;
  }
.fourth-screen__button:before{
  content: "";
  width:87px;
  height: 40px;
  display: block;
  margin: -12px 0 0 -6px;
  position: absolute;
  background:linear-gradient(248.67deg, rgba(255, 255, 255, 0) 30.84%, rgba(255, 255, 255, 0.29) 46.06%, rgba(255, 255, 255, 0) 64.04%);
}
.fourth-screen__button:last-of-type:before{
  margin: -12px 0 0 93px;
}
.fourth-screen__button:last-of-type{
  margin: 20px 0 0 0;
}
.fourth-screen__text{
  font-size: 12px;
  color: rgba(255, 255, 255, 0.6);
  font-weight: 300;
  line-height: 14px;
  margin: 20px 0 0 0;
  letter-spacing: 0.1em;
}

.fifth-screen__img-top{
  margin:64px 0 0 0;
}
.fifth-screen::after{
  content:'';
  width:100px;
  height:60px;
  margin:-30px 0 0 -15px;
  position: absolute;
  display: block;
  background-image: url("~@/assets/fifth-img-eye2.svg");
  opacity: 0.2;
  background-repeat: no-repeat;
}
.fifth-screen::before{
  content:'';
  width:60px;
  height:50px;
  margin:35px 0 0 260px;
  position: absolute;
  display: block;
  background-image: url("~@/assets/fifth-img-eye1.svg");
  opacity: 0.2;
  background-repeat: no-repeat;
}
.fifth-screen__text{
  font-family: 'Bad Script', cursive;
  font-size: 20px;
  line-height: 28px;
  margin:34px 0 0 0;
  letter-spacing: 0.01em;
}
.fifth-screen__img-bottom{
  margin:31px 0 0 0;
}
.footer{
  margin:65px 0 0 0;
}
.footer__text{

font-size: 7px;
line-height: 9px;
letter-spacing: 3px;
text-transform: uppercase;
color: #9D9D9D;
}
@media (min-width:1440px) {
.wrapper {
  width:1420px;
}
.first-screen{
  background-image: url('~@/assets/main-bg-1440.png');
  display: flex;
  flex-direction: column;
  align-items: center;
}
.first-screen__title{
  font-size: 16px;
  line-height: 19px;
}
.first-screen__subtitle{
  font-size: 25px;
  line-height: 29px;
  margin:23px 0 0 0;
}
.first-screen__img{
  margin:42px 0 -24px 0;
  width:392px;
  height:392px;
  background-image: url('~@/assets/woman-1440.png'); 
}
.first-screen__question{
  font-size: 25px;
  margin: 24px 0 0 0;
  line-height: 35px;
}
.first-screen__button{
  width:316px;
  height: 70px;
  margin: 65px 0 0 0;
  border-radius: 35px;
  font-size: 20px;
  }
.first-screen__button:before{
  content: "";
  width:130px;
  height: 70px;
  margin: -24px 0 0 -6px;
  background:linear-gradient(248.67deg, rgba(255, 255, 255, 0) 30.84%, rgba(255, 255, 255, 0.29) 46.06%, rgba(255, 255, 255, 0) 64.04%);
}
.first-screen__button:last-of-type:before{
  margin: -24px 0 0 173px;
}
.first-screen__button:last-of-type{
  margin: 34px 0 0 0;
}
.first-screen__text{
  font-size: 16px;
  line-height: 19px;
  margin: 35px 0 0 0;
}
.second-screen__img{
  background-image: url('~@/assets/second-screen-bg-1440.png');
  width:136px;
  height: 136px;
  border-radius: 75px;
  margin:75px 0 0 0;
}
.second-screen__text{
  width:440px;
  border: 1px solid #FFFFFF;
  margin:-68px 33px 0 33px;
  border-radius: 3px;
  padding:127px 0 62px 0;
  font-size: 25px;
  line-height: 35px;
}
.second-screen__text--bold{
  font-size: 25px;
  line-height: 35px;
}
.third-screen{
  width:1420px;
  height: 600px;
  margin:-78px 0 0 0;
  background-image: url('~@/assets/third-screen-bg-1440.png');
}
.third-screen__text::before{
  display: none;
}
.third-screen__text{
  padding:238px 0 0 0;
  font-size: 25px;
  line-height: 35px;
}
.third-screen__text--bold{
  font-size: 25px;
  line-height: 35px;
}
.fourth-screen{
  display: flex;
  flex-direction: column;
  align-items: center;
}
.fourth-screen__title{
  font-size: 25px;
  line-height: 35px;
  margin: 130px 0 0 0;
}
.fourth-screen__button{
  width:316px;
  height: 70px;
  margin: 46px 0 0 0;
  font-size: 20px;
  border-radius: 35px;
  }
  .fourth-screen__button:before{
  width:130px;
  height: 70px;
  margin: -24px 0 0 -6px;
  }
  .fourth-screen__button:last-of-type:before{
  margin: -24px 0 0 153px;
}
.fourth-screen__button:last-of-type{
  margin: 37px 0 0 0;
}
.fourth-screen__text{
  font-size: 16px;
  line-height: 19px;
  margin: 34px 0 0 0;
  letter-spacing: 0.1em;
}
.fifth-screen__img-top{
  margin:114px 0 0 0;
  width:58px;
}
.fifth-screen::after{
  width:300px;
  height:150px;
  margin:-64px 0 0 -35px;
  background-size: contain;
}
.fifth-screen::before{
  width:161px;
  height:190px;
  margin:15px 0 0 1260px;
  opacity: 0.2;
  background-size: auto 190px;
  background-repeat: no-repeat;
}
.fifth-screen__text{
  font-size: 25px;
  line-height: 35px;
  margin:74px 0 0 0;
}
.fifth-screen__img-bottom{
  margin:83px 0 0 0;
  width:58px;
}
.footer{
  height:50px;
  margin: 100px 0 0 0;
}
}
@media (min-width:1920px) {
.wrapper {
  width:1900px;
}
.first-screen{
  background-image: url('~@/assets/main-bg-1920.png');
}
.third-screen{
  margin:-78px 0 0 240px;
}
.fifth-screen::after{
  width:300px;
  height:160px;
  margin:-64px 0 0 190px;

}
.fifth-screen::before{
  width:300px;
  height:190px;
  margin:15px 0 0 1360px;
}

}
</style>
<template>
  <article>
    <section class="wrap">
      <div class="first-row">
        <h1>Manage and track all your Work Inside one app</h1>
        <p class="para">
          Single Page Applications are web apps or sites that interact with the
          user by dynamically rewriting the current page rather than loading
          entire new pages from the server.
        </p>
        <button class="herobtn" @click="Toggle">Learn More</button>
      </div>
      <div>
        <img class="heroImg" src="@/assets/HeroImage.png" />
      </div>

      <transition name="fade">
        <div class="displayMessage" v-show="display">
          Thanks for clicking, Awesome
        </div>
      </transition>
    </section>

    <div class="wrapper">
      <h2>
        Create timelines, Track progress, assign work and talk with your clients
        inside one web app!
      </h2>

      <!-- <video src="" controls>   </video> -->

      <div class="vid">
        <video class="youtubevideo" width="900" height="" ref="videoPlayer">
          <source src="@/assets/sunset-153976.mp4" type="video/mp4" :class="{ 'hidden': !playing }"/>
          Your browser does not support the video tag.
        </video>

        <button class="playericon "   @click="togglePlayPause">
          <i v-show="!playing"  class="fas fa-play"></i>
          <i v-show="playing" class="fas fa-pause"></i>
        </button>

    </div>
    

   
    </div>
    <!-- start of the content box -->
    <div class="contentboxWrapper">
      <ul class="boxcontent" v-for="content in contents" :key="content.id">
        <img class="icon" :src="require(`@/assets/${content.image}`)" />

        <div>
          <li class="titleBox">{{ content.title }}</li>
          <li class="contentboxpara">{{ content.description }}</li>
        </div>
      </ul>
    </div>
    <button class="trybtn" @toggle-fav="toggleStatus">I want to try!</button>

    <!-- start of competition section -->
    <div class="competitorWrap">
      <div><img src="@/assets/lady.png" /></div>

      <div class="growth">
        <h2>Grow faster than your competitors</h2>
        <p>
          Single Page Applications are web apps or sites that interact with the
          user by dynamically rewriting the current page rather than loading
          entire new pages from the server.
        </p>

        <!-- start of icon text -->
        <div class="iconText">
          <div class="first">
            <div>
              <img class="firstImg" src="@/assets/Manage-Icon.svg" />
            </div>
            <div>
              <h3>Manage all your work</h3>
              <p>
                Single Page Applications are web apps or sites that interact
                with Single Page Applications are web apps or sites that
                interact with
              </p>
            </div>
          </div>
          <div class="first">
            <div>
              <img class="firstImg" src="@/assets/Scale-Icon.svg" />
            </div>
            <div>
              <h3>Manage all your work</h3>
              <p>
                Single Page Applications are web apps or sites that interact
                with Single Page Applications are web apps or sites that
                interact with
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- start of carousel -->
    <div class="carousel">
      <TheCarousel v-slot="{ currentSlide }">
        <TheSlider v-for="(slide, index) in carouselSlides" :key="index">
          <div v-show="currentSlide === index + 1" class="slide-info">
            <!-- <img class="slideImg" :src="require(`../assets/${slide}`)" /> -->

            <h2 class="slide-text">{{ slide.description }}</h2>
            <div class="info">
              <div>
                <img :src="require(`../assets/${slide.image}`)" />
              </div>
              <p class="slide-name">{{ slide.name }}</p>
              <p class="slide-role">{{ slide.role }}</p>
            </div>
          </div>
        </TheSlider>
      </TheCarousel>
    </div>
    <!-- start of form section -->
    <div class="start-of-form">
      <div>
        <h2>Signup for early access offer!</h2>
        <p>
          Vestibulum ac diam sit amet quam vehicula elementum sed sit amet dui.
          Nulla quis lorem ut libero malesuada feugiat. Quisque velit nisi,
          pretium ut lacinia in, elementum id enim
        </p>

        <form @submit.prevent="onSubmit">
          <input v-model="username" type="text" placeholder="Rose" />
          <!-- <label>{{ username }}</label> -->
          <input
            v-model="email"
            type="email"
            placeholder="rossmartin@gmail.com"
          />
          <button class="formBtn" @click="submitForm">Submit</button>
        </form>
      </div>
      <div>
        <img class="signupImg" src="@/assets/Signup-Image.png" />
      </div>
    </div>
    <!-- end of form section -->

    <!-- start of FAQs section -->
    <AccordionSection></AccordionSection>
  </article>
</template>
<script>
import TheCarousel from '@/components/TheCarousel.vue';
import TheSlider from '@/components/TheSlider.vue';
import carouselContent from "@/carouselContent";
import AccordionSection from "@/Views/AccordionSection.vue"

// import TestimonialView from '@/Testimonial/TestimonialView.vue'
export default{

       components:{TheCarousel,TheSlider, AccordionSection},
       data(){
              return{
                     display:false,
                     contents: carouselContent.contents ,
                      slides:[

                              "https://www.collinsdictionary.com/images/full/teacher_81762259.jpg",
                              "https://media.istockphoto.com/id/1348229043/photo/business-accountant-accountant-and-bookkeeper.jpg?b=1&s=170667a&w=0&k=20&c=augRvCO7cjzN58g8yvwsM0w9zXjw8hDjLN_5TwXYcc8="
                            ],
                      username:'',
                      email:''  ,
                      playing: false,
                      
      isPaused: true

              }
       },

              setup(){
              const carouselSlides = [
                     {description:'This app is amazing Now im able to manage all my freelancing and agency work under one place. it make my life easy',
                      role:'freelancer',
                      name:'ASHUTOSH MEHTA',
                      image:'lady.jpeg'},
                      {description:'This app is amazing Now im able to manage This app is amazing Now im able to manage',
                      role:'Developer',
                      name:'DUNNI',
                      image:'lady-2.jpeg'}
                  ]

              return{carouselSlides}
       },

       methods:{
         Toggle(){
              this.display = !this.display
         },
         submitForm(){
           const ans= this.username + " " +this.email
             console.log(ans)
         },

         togglePlayPause() {
            this.playing = !this.playing;
            setTimeout(() => {
           this.hidePlayPauseBtn();
        }, 2000);
        if (this.playing) {
                // code to play video
              this.$refs.videoPlayer.play();
          } else {
         // code to pause video
      this.$refs.videoPlayer.pause();
    }
  },
  hidePlayPauseBtn() {
      const playPauseBtn = document.querySelector('.playericon');
      playPauseBtn.classList.add('hide');
    }
}


  }
      
      
</script>

<style scoped>
p {
  font-family: "Inter", sans-serif;
}
.pink {
  height: 100vh;
  width: 100%;
}
section {
  background: #140d2d;
  width: 100%;
  height: 100vh;
  color: #fff;
  position: relative;
  margin-top: -2rem;

  /* top:-4rem; */
}

body {
  margin: 0;
  padding: 0;
}
.wrap {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  /* max-width:fit-content; */
}
.heroImg {
  max-width: 750px;
  height: auto;
  position: relative;
  left: 0;
  right: 0;
  top: 110px;
}
.first-row {
  position: relative;
  top: 150px;
  left: 5rem;
  max-width: 801px;
  margin: 0 auto;
}
h1 {
  font-size: 50px;
  line-height: 65px;
  font-weight: 300;
  padding-left: 2rem;
  text-transform: capitalize;
  font-family: "Krona One", sans-serif;
}
.para {
  font-size: 17px;
  line-height: 25px;
  padding-right: 10rem;
  padding-left: 2rem;
  position: relative;
  top: -30px;
}
.displayMessage {
  position: absolute;
  background: white;
  color: black;
  width: 100%;
  text-align: center;
  margin-top: 30px;
  margin-bottom: 30px;
  z-index: 10;
}
/* this is the transition style */
.fade-enter-active {
  transition: all 0.3s ease-out;
}
.fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}
.fade-enter-from,
.fade-leave-to {
  transform: translateX(20px);
  opacity: 0;
}

button {
  background: #e0ff00;
  font-size: 17px;
  line-height: 20px;
  padding: 10px;
  margin-left: 2rem;
  font-family: "Inter", sans-serif;
  border-radius: 5px;
  width: 10rem;
  border: none;
  transition: all 0.3s linear;
}
button:hover {
  background: #c1da08;
  transform: scaleX(1.1);
}
.wrapper {
  padding: 10rem 2rem;
}

.wrapper h2 {
  width: 880px;
}
h2 {
  font-size: 50px;
  line-height: 60px;
  margin: auto;
  width: 840px;
  text-align: left;
  /* padding-left:-130px; */
}
div .youtubevideo {
  display: block;
  margin: 50px auto 10px auto;
  border-radius: 20px;
}
/* start of the content box style */
.contentboxWrapper {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  gap: 50px;
  margin: 0px 90px;
}
ul {
  padding: 80px 50px;
  height: auto;
  border-radius: 10px;
}

/* style for the first box */
ul:first-child {
  background: #000000;
  color: #ffffff;

  transition: all 0.6s ease-in;
}

ul:first-child:hover {
  background: #252525;
  -webkit-transform: scale(0.9);
  -ms-transform: scale(0.9);
  transform: scale(0.9);
}
/* style for the second box */
ul:nth-child(2) {
  background: #f2f0f0;
  transition: all 0.3s linear;
}
.contentboxpara:nth-child(2) {
  padding-top: 20px;
}
ul:nth-child(2):hover {
  background: #000000;
  color: #ffffff;
  -webkit-transform: scale(0.9);
  -ms-transform: scale(0.9);
  transform: scale(0.9);
}

/* style for the box */
ul {
  background: #e4cdcd;
  list-style-type: none;
  transition: all 0.3s linear;
}
ul:hover {
  background: #f2f0f0;
  -webkit-transform: scale(0.9);
  -ms-transform: scale(0.9);
  transform: scale(0.9);
}
.titleBox {
  font-size: 20px;
  line-height: 25px;
  padding: 20px 0px 0px 0px;
}
.contentboxpara {
  font-family: "Inter", sans-serif;
  font-size: 17px;
}
/* end of the content box  */

.trybtn {
  font-size: 17px;
  text-transform: capitalize;
  margin: 20px auto;
  display: block;
  background: #e0ff00;
  border: none;
  border-radius: 5px;
  padding: 15px 24px;
  transition: all 0.3s linear;
}
button:hover {
  background: #c1da08;
  transform: scaleX(1.1);
}
.competitorWrap {
  display: flex;
  flex-direction: row;
  gap: 100px;
  flex-wrap: nowrap;
  justify-content: center;
  align-items: center;
  padding: 65px 150px 65px 100px;
}
/* .first{
       display: flex;
       flex-direction: row;
       justify-content: flex-start;
} */
.growth {
  padding-top: 4rem;
  width: 34rem;
}
.growth h2 {
  font-size: 35px;
  width: 620px;
}

.first {
  display: flex;
  flex-direction: row;
  gap: 25px;
}
.firstImg {
  margin-top: 30px;
  width: 50px;
}
.first h3 {
  font-size: 25px;
  padding: 0px;
}
.carousel {
  position: relative;
  overflow: hidden;
  max-height: 100vh;
  padding: 40px 0px;
  height: 60vh;
  background: #140d2d;
}
.carousel img {
  position: absolute;
  /* border-radius:70%; */
  height: 12vh;
  object-fit: cover;
  top: 299px;
  left: 19rem;
  width: 80px;
}
.slide-info {
  position: absolute;
  width: 100%;
  height: 80%;
  top: 40;
  left: 0;
}
.slide-text {
  /* min-width: 100%;
  height: 40vh; */
  font-size: 38px;
  padding-top: 30px;
  color: #fff;
}
/* .slideView{
       font-size: 50px;
} */
.slide-name {
  position: absolute;
  top: 300px;
  left: 401px;
  color: #fff;
}
.slide-role {
  position: absolute;
  top: 330px;
  left: 401px;
  color: #8f85b2;
}

.start-of-form {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  max-width: 1400px;
  margin: 0 auto;
  padding: 120px 0px;
}
.start-of-form h2 {
  font-size: 40px;
  color: #000000;
  text-transform: capitalize;
  padding: 10px 26px;
  width: 32rem;
}
.formBtn {
  margin-left: 23px;
}
.start-of-form p {
  color: #000000;
  font-size: 18px;
  margin-left: 25px;
}
.start-of-form div:nth-child(1) {
  max-width: 545px;
  display: block;
}
/* .start-of-form div:nth-child(2){
 
  width:40%;
} */
.signupImg {
  width: 516px;
  max-width: 1500px;
  text-align: left;
}
input {
  padding: 15px;
  width: 430px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  margin-bottom: 20px;
  margin-left: 23px;
  border: none;
  background: #f2f0f0;
  outline-color: #c1da08;
}

.carousel {
  /* max-width: fit-content; */
  margin: 0 auto;
}
.playericon {
  position: relative;
   width: 100px; /* or any other fixed value */
  max-width: 100px; /* prevent button from expanding */
  min-width: 100px; /* prevent button from shrinking */
  left: 23rem;
  /* top: 88rem; */
  bottom: 18rem;
  /* width: 100px; */
  height: 8vh;
  padding: 10px;
  cursor: pointer;
  transition: opacity 0.5s ease;
  text-align: center;
  border-radius:10px;
}

i{
  font-size: 30px;
}
.hidden {
  display: none;
}
.vid{
  width:900px;
  min-width: 900px;
  max-width:900px;
  margin:auto;
}
@media screen and (min-width:993px) and (max-width:1024px){
  .para{
    padding-right: 0px;
  }
  section{
    height:80vh;
  }
  .first-row {
    left:2rem;
  }
  h1 {
    font-size: 30px;
    line-height: 35px;
   
 padding-left: 2rem;
    text-transform: capitalize;
    font-family: "Krona One", sans-serif;
    width: 100%;
}
.wrapper{
    padding: 5rem 2rem 0rem 2rem;
}
  .growth{
    width:50%;
  }
  .competitorWrap{
    padding:0px;
    width:100%;
    gap:0px;
  }
  .signupImg{
    width: 370px;
  }
}

@media screen and (min-width:769px) and (max-width:992px){
 
 .heroImg {
   max-width: 428px;
 }
 .para{
   padding-right:0px;
 
 }
 .contentboxWrapper{
   gap:10px;
   margin:0px 10px;
 }
 section{
   height:auto;
   padding-bottom: 14rem;

 }
 div .youtubevideo{
   display: block;
   margin: 50px auto 50px 0px;
   /* margin: 50px auto 10px auto; */
   
   width: 80%;
 }

}
@media screen and (min-width:577px) and (max-width:768px){
  section{
    height:auto;
  }
.wrap{
  padding-bottom:4rem;
  /* background: #c1da08; */
   /* flex-wrap:wrap; */
}
h1 {
    font-size: 30px;
    line-height: 35px;
    font-weight: 300;
     padding-left: 0rem;
    }
    .para{
      padding-left:0px;
      padding-right:0px;
    }
    button{
      margin-left:0px;
    }
    .heroImg{
    max-width: 500px;
     }
     .first-row{
      left:3rem;
     }

/* CREATE TIMELINE */
.wrapper{
  padding:5rem 2rem;
}
.wrapper h2{
  font-size:35px;
  line-height:40px;
  width:auto;
}
div .youtubevideo{
  margin:1rem 0rem;
  width:70%;
  
}
.playericon{
  left:16rem;
  bottom:15rem;
}
/* CONTENT BOXES */
.contentboxWrapper{
  flex-wrap:wrap;
  gap:0px;
}
/* GROW FASTER SECTION */
.competitorWrap{
  flex-wrap:wrap;
  gap:0px;
}
.growth h2{
  line-height:40px;
}
.start-of-form {
    display: flex;
    flex-direction: row;
    /* justify-content: center; */
    flex-wrap: wrap;
    max-width: 100%;
    padding:50px 0px;
}
.slide-text {
              font-size:20px;
              line-height: 22px;
              width:70%;
       }


}
@media screen and (max-width:576px){
  .wrapper{
    padding:3rem;
  }
  section{
    height: auto;
    padding-bottom:12rem;
  }
  .playericon{
   
    left: 5.5rem;
    bottom: 7rem;
  }
.wrap{
  /* background: red; */
  max-width:576px;
}
.heroImg{
  display:none;
}
h1{
  font-size:25px;
  line-height: 26px;
}

.wrapper h2 {
 
    width: auto;
    font-size: 25px;
    line-height: 28px;
}
.youtubevideo{
  width:305px;
  max-width:350px;


}
div .youtubevideo{
  margin-left:1px;
  /* margin:0px;
  margin-top: 25px; */
}

/* form section */
.start-of-form{
  flex-direction: column;
  margin:0px;
  width:auto;
  max-width:auto;
  padding:80px 0px;
}
.start-of-form h2{
  font-size:20px;
  line-height: 25px;
  width:auto;
}
input{
  width:80%;
}
.signupImg{
  width:300px;
}
.contentboxWrapper{
  flex-direction: column;
  margin: 0px 20px;
  gap:5px;
}
/* START OF GROW FASTER SECTION */
.competitorWrap{
  flex-direction: column;
  gap:0px;
  padding:50px 0px;
}
.competitorWrap img{
  width:300px;
}
.growth h2{
  width:auto;
  font-size: 25px;
  line-height: 25px;
}
.growth{
  width:auto;
  padding:20px 25px;
}
.first{
  flex-wrap: wrap;
  gap:0px;
}
.first .firstImg{
  width:50px;
}
.first h3{
  font-size:20px;
  line-height: 25px;
}
.first-row{
  left:0px;
  top:6rem;
  padding-right: 3rem;
}
h1{
  width:auto;
  line-height:27px;
  padding-bottom: 10px;
}
h2{
  font-size:30px;
}
.para{
 padding-right: 0px;
}
i{
  left: 30rem!important;;
}
.slide-text{
font-size: 20px;
    line-height: 25px;
    padding-top: 30px;
    color: #fff;
    width: 80%;
}
.carousel img{
    position: inherit;
    margin-top:2rem;
    margin-left:2rem;
}
.slide-name{
  position:inherit;
  margin-left:2rem;
}
.slide-role{
  position:inherit;
  margin-left:2rem;
}
.playericon{
  position: relative;
   width: 70px; /* or any other fixed value */
  max-width: 70px; /* prevent button from expanding */
  min-width: 70px; /* prevent button from shrinking */
  left:6rem;
  bottom:8rem;
}
}
@media screen and (max-width:360px){
  section{
   height:auto;
   padding: 06rem 1.5rem;
  }
  .wrapper{
    padding:2rem 0px;
    padding-left: 10px;
  }
  .first-row{
    top:0px;
    left:0px;
    padding-right:0px;
  }
  .para{
    padding-right:2rem;
    padding-left: 0px;
    top:-5px;
  }
  h1{
    padding-left: 0px;
    padding-right:2rem;
  }
  h2{
    font-size:25px;
  }
button{
  margin-left:0px;

}
 
.wrap{
  /* background: red; */
  max-width:576px;
}
.heroImg{
  display:none;
}
h1{
  font-size:25px;
  line-height: 26px;
}
.wrapper h2 {
 
    width: auto;
    font-size: 25px;
    line-height: 28px;
    padding:02rem 1rem;
}

.playericon{
  bottom:8rem;
  left:9rem;
  position: relative;
    width: 12px;
    max-width: 45px;
    min-width:60px;
  
}

/* i{
  font-size:20px;
 
} */
div .youtubevideo{
  width:340px;
   margin-top: 20px;
   
}

/* form section */
.start-of-form{
  padding:90px 0px;
  flex-direction: column;
  margin:0px;
  width:auto;
  max-width:auto;
}
.start-of-form h2{
  font-size:20px;
  line-height: 25px;
  width:auto;
}
input{
  width:80%;
}
.signupImg{
  width:300px;
}
.contentboxWrapper{
  flex-direction: column;
  margin: 0px 20px;
}
/* START OF GROW FASTER SECTION */
.competitorWrap{
  flex-direction: column;
  gap:0px;
  padding:50px 0px;
}
.competitorWrap img{
  width:300px;
}
.growth h2{
  width:auto;
  font-size: 25px;
  line-height: 25px;
}
.growth{
  width:auto;
  padding:20px 25px;
}
.first{
  flex-wrap: wrap;
  gap:0px;
}
.first .firstImg{
  width:50px;
}
.first h3{
  font-size:20px;
  line-height: 25px;
}
ul{
  padding:40px 50px;
}
.contentboxWrapper{
  gap:5px;
}

/* sliders */
.slide-text{
  font-size:16px;
  line-height:20px;
  width:auto;
}

.carousel{
  height:48vh;
  /* padding:40px; */
  overflow:visible;
}
.togglePage{
  display:none;
}
.pagination{
 top:0px;
}
.carousel img{
  top:150px;
  left:0px;
  width:80px;
}
div{
  gap:0px;
}
.slide-name{
  position:inherit;
  margin-left:2rem;
}
.slide-text{
  max-width:80%;
}
.carousel img{
    position: inherit;
    margin-left:2rem;
}
  .info{
    padding-top:20px;
  }
 
}





</style>

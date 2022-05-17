<template>
  <div id="app">
  
    <h1 class>{{ title }}</h1>
    <h2>{{ currentDate() }}</h2>
    <p>{{entries}}</p>
  
      
      <ul class="ul">
          <li>
    <span style="color:red"> 14:00 Uhr </span> <br>
    <span style="color:orange"> Basisbeschäftigung Besuch</span> <br>
    <span style="color:orange"> Interessierte für den zweiten Kurs werden uns besuchen</span>
          </li>
        </ul>


       <ul class="ul">
          <li>
    <span style="color:red"> 14:00 Uhr </span> <br>
    <span style="color:orange"> Basisbeschäftigung Besuch</span> <br>
    <span style="color:orange"> Interessierte für den zweiten Kurs werden uns besuchen</span>
          </li>
        </ul> 

        <ul class="ul">
          <li>
    <span style="color:red"> 14:00 Uhr </span> <br>
    <span style="color:orange"> Basisbeschäftigung Besuch</span> <br>
    <span style="color:orange"> Interessierte für den zweiten Kurs werden uns besuchen</span>
          </li>
        </ul>

    <footer class="footer">
      <img class="img-footer" alt="SEB Logo" src="./assets/STZH_SEB_Logo.png">
      <img class="img-footer" alt="SAG Logo" src="./assets/SAG_Logo_De.png">
      <img class="img-footer" alt="Opportunity" src="./assets/Opportunity.png">
    </footer>

  </div> 


</template>

<script>

import axios from "axios";

export default {
  name: 'App',
  data() {
    return {
    title: "Welcome to Opportunity",
    sheet_id: "spreadsheets/d/1a81aI0Y8ViZO0tI92h2YSMqVQJ8hmNNMyMylXgvwiU4",
    api_token: "AIzaSyA-qeDXOhEeQDA0vQf7LgkF7DQtGnAtmAU",
    entries: [],
    
    }

  },

  // computed properties are like data properties, but with a method combined and it gets executed automatically, instead of calling a function explicitly
  computed: {
    gsheet_url() {
  return `https://sheets.googleapis.com/v4/spreadsheets/${this.sheet_id}/values:batchGet?ranges=A2%3AE100&valueRenderOption=FORMATTED_VALUE&key=${this.api_token}`;
  }
},



  methods: {
    getData () {
      axios.get (this.gsheet_url).then ((response) => {
          this.entries = response.data.valueRanges [0].values;

      });

    },

    updateCurrentDate() {

    },
    
    refreshData () {

    },

    currentDate() {
        const current = new Date();
        const day = current.getDate();
        const month = (current.getMonth()+1);
        const year = current.getFullYear();
        const dateTime = day + "." + month + "." + year;
        if (month < 10) {
          return day + "." + "0" + month + "." + year;
        }
        return dateTime;
      }

  },

    mounted() {
    this.getData();
    }
  };

</script>

<style>

body {background-color: 
#E8EFF4;}

h1 {
font-family: 'Inter';
font-style: normal;
font-weight: 900;
font-size: 62px;
line-height: 75px;
}

h2 {

font-family: 'Inter';
font-style: normal;
font-weight: 500;
font-size: 62px;
line-height: 75px;
color: #9AA7B1;

}

.footer { 
 position: fixed;
 display: flex;
 justify-content: space-between;
 box-sizing: border-box;
 left: 0px;
 bottom: 0px;
 width: 100%;
}

.footer img {
 height: 50px;

}

@import url('https://fonts.googleapis.com/css2?family=Inter:wght@500;900&display=swap');
#app {
  
  font-family: "Inter", Medium, Black;
  margin: 60px;
}

 .ul {
  margin-top: 60px;
  margin-bottom: 85px;
  margin-right: 12px;
  margin-left: 10px;
  left: 0px;
  right: 0px;
  top: 70px;
  border-radius: 5px;
  padding: 3rem;
  background: #0F05A0;
  
}

 .li {
  margin-top: 10px;
  margin-bottom: 80px;
  margin-right: 150px;
  margin-left: 20px;
  font-family: 'Inter';
  font-style: bold;
  font-weight: 900;
  font-size: 20px;
  line-height: 86px;
  color: #EB5E00;
}

.unlist{
list-style-type: none;

}



</style>

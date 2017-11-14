<template>
  <div>
    <div class="search">
      <div class="container">
        <form class="search-form">
          <input type="text" class="form-control input-visible" placeholder="Search job title" />
          <button type="button" class="btn btn-search" >Search</button>
        </form>  
      </div>
    </div>

    <div class="main container">
      <div class="row">
        <div class="col-md-4 filter">
          <h4>FILTERS</h4>
          <hr/>
          <div class="filter-box">
            <h5>Location</h5>
            <input type="text" class="form-control input-visible" placeholder="Search location" />
          </div>
          <div class="filter-box">
            <h5>Sort by</h5>
            <select class="form-control">
              <option>Date</option>
              <option>Distance</option>
            </select>
          </div>
          <div class="filter-box">
            <h5>Availability</h5>
            <div class="checkbox">
              <label>
                <input type="checkbox" id="checkbox_1" class="filled-in"/>
                <span><i class="fa fa-check" aria-hidden="true"></i></span>
                Part time
              </label>
              <label>
                <input type="checkbox" id="checkbox_1" class="filled-in"/>
                <span><i class="fa fa-check" aria-hidden="true"></i></span>
                Full time
              </label>
            </div>
          </div>
        </div>
        <div class="col-md-8 result">
          <h4>RESULTS</h4>
          <hr/>
          
          <div class="result-item">
            <div class="header">
              <h3>Kokki, Day Shine, Joensuu</h3>
              <div class="working-hour">Part time</div>
            </div>
            <div class="info">
              <span class="company"><i class="fa fa-building-o" aria-hidden="true"></i> Day Shine</span>
              <span class="location"><i class="fa fa-map-marker" aria-hidden="true"></i> Joensuu</span>
            </div>
            <p>
              We are looing for permanent Finnish waiter/waitress ( English &Finnish speaking) working at the best Chinese restaurant Da Zhong Hua in Rovaniemi,pls send us your CV by mail to suurkiina@gmail.com if you are interested. We are also looking for Chinese cuisine chef.
            </p>
            <div class="btn-wrapper">
              <div class="social">
                <i class="fa fa-twitter" aria-hidden="true"></i>
                <i class="fa fa-facebook" aria-hidden="true"></i>
                <i class="fa fa-linkedin" aria-hidden="true"></i>
              </div>
              <button class="btn btn-apply ">Apply</button>
            </div>
            <hr>
          </div>
          
          <div class="result-item">
            <div class="header">
              <h3>Ravintolan tarjoilija, 5 paikkaa, Suur-Kiina Ravintola Oy, Rovaniemi</h3>
              <span class="working-hour">Part time</span>
            </div>
            <div class="info">
              <span class="company"><i class="fa fa-building-o" aria-hidden="true"></i> Ravintolan tarjoilija</span>
              <span class="location"><i class="fa fa-map-marker" aria-hidden="true"></i> Rovaniemi</span>
            </div>
            <p>
              Haetaan autokuskia asiakkaillemme, pääasiassa kiinalaisille turisteille. Englannin kielen taito ehdoton, kiina plussaa. Tehtäviin kuuluu autolla kuljettaminen Lapin alueella asiakkaan mukaan. Kiertoajelut, revontulien metsästysajot yöllä , nähtävyydet, lentokenttä noudot ym. Työ aika osa-aikaista, kausittain saattaa olla runsaamminkin  ajoa. Vaihtelevat ajo ajat.  Odotamme sinulta joustavuutta,  hyvää ajokokemusta ja asiakaspalvelu henkisyyttä. Otathan yhteyttä mikäli uskot olevasi sopivan hommaan!\r\n\r\nLooking for a driver who's main area in this job  will be Lapland. Airport pick-ups, customer sihtseeing and Aurora hunting in the night possibly. Part time and changing working time. Depending on tourism situation, can be more driving some days. Be flexible, customer servant and have a good driving experience with english language skills and the job might be yours! Chinese language is plus!
            </p>
            <div class="btn-wrapper">
              <div class="social">
                <i class="fa fa-twitter" aria-hidden="true"></i>
                <i class="fa fa-facebook" aria-hidden="true"></i>
                <i class="fa fa-linkedin" aria-hidden="true"></i>
              </div>
              <button class="btn btn-apply ">Apply</button>
            </div>
            <hr>
          </div>
          
          <div class="page">
            <div class="previous button"><i class="fa fa-chevron-left" aria-hidden="true"></i></div>
            <div class="number">1</div>
            <div class="next button"><i class="fa fa-chevron-right" aria-hidden="true"></i></div>
          </div>
        </div>
      </div>
    </div>
    <hr>
  </div>
</template>

<script>
import Vue from 'vue';
import VueResource from 'vue-resource';

Vue.use(VueResource);

export default {
  name: 'MainApp',

  data() {

  },
  methods: {
    getData() {
      this.$http
        .get('https://paikat.te-palvelut.fi/tpt-api/tyopaikat?englanti=true')
        .then((response) => {
          console.log(response.data.response.docs);
        })
        .catch((response) => {
          console.log(response.data);
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">

</style>

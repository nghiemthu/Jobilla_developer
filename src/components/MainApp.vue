<template>
  <div>
  <!-- Search bar -->
    <div class="search">
      <div class="container">
        <form class="search-form">
          <input v-model="keyword" class="form-control input-visible" placeholder="Search by keyword" />
          <button type="button" class="btn btn-search" >Search</button>
        </form>  
      </div>
    </div>

    <div class="main container">
      <div class="row">
        <div class="col-md-4 filter">
          <h4>FILTERS</h4>
          <hr/>
            
          <!-- Filter By Location -->
          <div class="filter-box">
            <h5>Location</h5>
            <input v-model="location" class="form-control input-visible" placeholder="Search location" />
          </div>
 
          <!-- Filter By Date -->
          <div class="filter-box">
            <h5>Sort by</h5>
            <select class="form-control" v-model="sortDate">
              <option>Date Newest</option>
              <option>Date Oldest</option>
            </select>
          </div>
          <!-- Filter By Working Time -->
          <div class="filter-box">
            <h5>Working Time</h5>
            <div class="checkbox">
              <label>
                <input type="checkbox" id="checkbox_1" class="filled-in" value="osapäivätyö" v-model="workingTime"/>
                <span><i class="fa fa-check" aria-hidden="true"></i></span>
                Part time
              </label>
              <label>
                <input type="checkbox" id="checkbox_1" class="filled-in" value="kokoaikatyö" v-model="workingTime"/>
                <span><i class="fa fa-check" aria-hidden="true"></i></span>
                Full time
              </label>
            </div>
          </div>
        </div>

        <!-- Result Section -->
        <div class="col-md-8 result">
          <h4>RESULTS</h4>
          <hr/>

          <!-- Loading bar -->
          <div class="loading" v-if="loadingData">
            <div class="fill"></div>
          </div>
          
          <result-item v-for="item in filterData().filter(sortDataByPage(pageNumber))" :job="item"></result-item>

          <!-- Pages -->
          <div class="page">
            <div  
              class="previous button" 
              v-if="pageNumber > 0"
              v-on:click="decreasePageNumber()"><i class="fa fa-chevron-left" aria-hidden="true"></i></div>
            <div class="number">{{ pageNumber + 1 }}</div>
            <div 
              class="next button" 
              v-if="pageNumber < filterData().length / 10"
              v-on:click="increasePageNumber()"><i class="fa fa-chevron-right" aria-hidden="true"></i></div>
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
import ResultItem from './ResultItem';

Vue.use(VueResource);

export default {
  name: 'MainApp',
  components: { ResultItem },
  data() {
    return {
      data: [],
      loadingData: true,
      err: 'err',
      pageNumber: 0,
      location: '',
      keyword: '',
      sortDate: 'Date Newest',
      workingTime: [],
    };
  },

  mounted() {
    this.getData();
  },

  methods: {
    getData() {
      this.$http
        .get('https://paikat.te-palvelut.fi/tpt-api/tyopaikat?englanti=true')
        .then((response) => {
          this.loadingData = false;
          this.data = response.data.response.docs;
        })
        .catch((response) => {
          this.err = response.data;
        });
    },
    increasePageNumber() {
      if (this.pageNumber < this.data.length / 10) this.pageNumber = this.pageNumber + 1;
    },
    decreasePageNumber() {
      if (this.pageNumber > 0) this.pageNumber = this.pageNumber - 1;
    },
    sortDataByPage: pageNumber => (val, index) =>
      pageNumber * 10 < index && index < (pageNumber + 1) * 10,

    // Filter data by an array - working time
    sortDataByWorkingTime: workingTime => val =>
      workingTime.length === 0 ? true : workingTime.indexOf(val.tyoaika) >= 0,
    sortDataByLocation: location => val =>
      (val.kunta) ? val.kunta.includes(location) : false,
    sortDataByKeyword: keyWord => val =>
      (val.otsikko) ? val.otsikko.includes(keyWord) || val.kuvausteksti.includes(keyWord) : false,
    sortDataByDate() {
      if (this.data && this.sortDate === 'Date Newest') {
        return (a, b) => new Date(b.ilmoituspaivamaara) - new Date(a.ilmoituspaivamaara);
      }

      return (a, b) => new Date(a.ilmoituspaivamaara) - new Date(b.ilmoituspaivamaara);
    },
    filterData() {
      return this.data
            ? this.data
              .filter(this.sortDataByKeyword(this.keyword))
              .filter(this.sortDataByLocation(this.location))
              .sort(this.sortDataByDate())
              .filter(this.sortDataByWorkingTime(this.workingTime))
            : [];
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">

</style>

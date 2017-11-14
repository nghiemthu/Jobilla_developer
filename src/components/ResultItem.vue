<template>
  <div class="result-item">
  	<div class="date">{{ job.ilmoituspaivamaara.slice(0,10) }}</div>
    <div class="header">
      <h3>{{ job.otsikko }}</h3>
      <div class="working-hour">{{ 
      	(job.tyoaika == 'kokoaikatyö') ? 'Full Time' 
      	: (job.tyoaika == 'osapäivätyö') ? 'Part Time' : job.tyoaika
      }}</div>
    </div>
    <div class="info">
      <span class="company"><i class="fa fa-building-o" aria-hidden="true"></i> {{ job.tyonantajanNimi }}</span>
      <span class="location"><i class="fa fa-map-marker" aria-hidden="true"></i> {{ job.kunta }}</span>
    </div>
    <p>
      {{ (seeMore) ? job.kuvausteksti : job.kuvausteksti.slice(0, 150) }}
      <span v-if="!seeMore && job.kuvausteksti.length > 150">...<span class="more" v-on:click="getMoreInfo()">More</span></span>
      <span v-if="seeMore && job.kuvausteksti.length > 150" class="more" v-on:click="getLessInfo()"> Less</span>
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
</template>

<script>
export default {
  name: 'ResultItem',
  props: ['job'],

  data() {
    return { seeMore: false,
    };
  },
  methods: {
    getMoreInfo() {
      this.seeMore = true;
    },
    getLessInfo() {
      this.seeMore = false;
    },
  },
};
</script>
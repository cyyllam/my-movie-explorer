<template>
 
  <div class="m-4">

    <b-tabs content-class="m-3">
      <!-- <div class="mx-auto"> -->
        <!-- first tab -->
      <b-tab title="Trending Now" active>
      <b-row>
        <!-- radio form using FilterForm component-->
        <b-col class="col-sm-12 col-md-3">
          <FilterForm :formlabel="firstFormLabel">
             <b-form-radio v-model="selected" name="trend-period" value="week" @change="getTrendingResults">Week</b-form-radio>
                  <b-form-radio v-model="selected" name="trend-period" value="day" @change="getTrendingResults">Day</b-form-radio>
          </FilterForm>         
        </b-col>
        <!-- trending content -->
        <b-col class="col-sm-12 col-md-9">
          <intro v-if="selected === null">
            <p slot="title" class="lead text-center">Select a Trending Period to see results</p>
          </intro>

          <intro v-else>
            <p slot="title" class="lead">Trending {{trendPeriodText}}</p>
            <p slot="content">
              Here are {{ trendingResultsLength }} movies trending {{trendPeriodText}} according to 
              <a href="https://developers.themoviedb.org/3/trending/get-trending"
              target="_blank">tMDB</a>. 
              {{ trendPeriodDefinition }}
              </p>
          </intro>

          <b-card-group deck>
            <!-- Loop with CardDeck component -->
            <CardDeck 
            v-for="result in trendingResults" 
            :key="result.id" 
            :result="result" />
            </b-card-group> 
          
          </b-col>
        </b-row>
      </b-tab>

        <!-- discover content -->
      <b-tab title="Discover">
        <b-row>
          <!-- Select criteria using FilterForm component -->
           <b-col class="col-sm-12 col-md-3">
             <FilterForm>
                 <label>Year: </label>
                 <b-form-input v-model="selYearDiscover" placeholder="Enter 4-digit year"></b-form-input>
                 <label class="mt-3">Language (original): </label>
                 <b-form-select v-model="selLangDiscover" :options="optLangDiscover"></b-form-select>
                 <b-button class="mt-3" @click="getDiscoverResults(); discoverLang(); discoverYear();">Enter</b-button>
             </FilterForm>
           </b-col>
           <b-col class="col-sm-12 col-md-9">

            <intro v-if="discoverResults === null">
              <p slot="title" class="lead text-center">Discover non-English language films. Select criteria to see results</p>
            </intro>
            
            <intro v-else>
              <p slot="title" class="lead">Discover non-English Language Films by Year</p>
              <p slot="content">
                Here are {{ discoverResultsLength }} movies in {{ enteredLangDiscover }} from {{ enteredYearDiscover }} with high vote averages and more than 10 vote counts according to 
                <a href="https://themoviedb.org"
                target="_blank">tMDB</a>. 
                </p>
            </intro>

             <b-card-group deck>
               <!-- Loop with CardDeck component -->
              <CardDeck 
              v-for="result in discoverResults" 
              :key="result.id" 
              :result="result" />
            </b-card-group> 

           </b-col>
        </b-row>
        </b-tab>
        <!-- </div> -->
    </b-tabs>

  </div>

</template>

<script>
import Intro from '~/components/intro.vue';
import FilterForm from '~/components/FilterForm.vue';
import CardDeck from '~/components/CardDeck.vue';
import axios from 'axios';

export default {
    head () {
    return {
      title: this.title,
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        { hid: 'description', name: 'description', content: 'View a list of trending movies for the week or for the day. You can also explore non-English language films by year and language.' }
      ]
    }
    },
    components: {
      Intro,
      FilterForm,
      CardDeck
    },
    data() {
        return {
          title: 'Explore: Discover trending or highly rated movies',
          firstFormLabel: 'Trending Period',
          selected: null,
          // btnDiscoverState: false,
          selYearDiscover: null,
          optLangDiscover: [
            {value: null, text: 'Please select an option' },
            {value: 'zh', text: 'Chinese'},
            {value: 'fr', text: 'French'},
            {value: 'de', text: 'German'},
            {value: 'hi', text: 'Hindi'},
            {value: 'ja', text: 'Japanese'},
            {value: 'ko', text: 'Korean'},
            {value: 'ru', text: 'Russian'},
            {value: 'es', text: 'Spanish'},
            {value: 'sw', text: 'Swahili'},
            {value: 'ta', text: 'Tamil'}
            ],
          selLangDiscover: null,
          enteredLangDiscover: null,
          enteredYearDiscover: null,
          loading: true,
          trendingResults: null,
          discoverResults: null,
          errored: false,
          discoverResultsLength: null,
          trendingResultsLength: null,
        }
    },
    computed: {
      trendPeriodText() {
        // depending on radio button selected in Trending tab, will return appropriate text to fit in page header
        let leadingText;
        if (this.selected === 'day') {
          return leadingText = 'today';
        } else {
          return `this ${this.selected}`;
        }; 
      },
      trendPeriodDefinition() {
        // depending on radio button selected in Trending tab, will return appropriate statement about content update
        let definition;
        if (this.selected === 'day') {
          definition = 'The daily trending list tracks items over the period of a day while items have a 24 hour half life.';
        } else {
          definition = 'The weekly list tracks items over a 7 day period, with a 7 day half life.';
        };
        return definition; 
      }    
    },
    methods: {
         getTrendingResults(event) {
           // api call for retrieving tmdb trending data
          let apicall = 'https://api.themoviedb.org/3/trending/movie/' + event + '?api_key=890f4b3dccb1250594537c39d4d51fd9';
           axios.get(apicall).then(response => { let res = response.data.results; this.trendingResultsLength = res.length; this.trendingResults = res })
          .catch(error => {console.log(error)
          this.errored = true})
          .finally(() => this.loading = false);
        },
        getDiscoverResults() {
          // api call for retrieving tmdb customized discover data
          let apicall = 'https://api.themoviedb.org/3/discover/movie?api_key=890f4b3dccb1250594537c39d4d51fd9&language=en-US&sort_by=vote_average.desc&include_adult=false&include_video=false&page=1&primary_release_year=' + this.selYearDiscover + '&vote_count.gte=10&with_original_language=' + this.selLangDiscover
          axios.get(apicall)
          .then(response => { let res = response.data.results; this.discoverResultsLength = res.length; this.discoverResults = res })
          .catch(error => {console.log(error)
          this.errored = true})
          .finally(() => this.loading = false);
        },
        discoverLang() {
          // return the text of the select value for Language selection on Discover tab
          let langText = this.optLangDiscover.filter(obj => {return obj.value === this.selLangDiscover})[0];
          return this.enteredLangDiscover = langText.text;
        },
        discoverYear() {
          // return the year submitted from year input on Discover tab
          return this.enteredYearDiscover = this.selYearDiscover; 
        }
    },
    mounted () {
    }  
}
</script>

<style>

</style>
<template>
  <section class="m-5">

    <b-card no-body>
      <b-tabs pills card vertical nav-wrapper-class="w-25">
        <b-tab title="About" active>
          <b-card-text>
            <p>Thanks for visiting!</p>
            <p>
              This site was built using nuxt.js and BootstrapVue as an individual course project for the 
              third quarter of the Front-end Development Certificate Program at the University of Washington. 
            </p>
            <p>
              Movie Explorer was created with the intention of having a tool where I could better query or
              view movie trends, statistics, or trivia that interested me. 
            </p>
          </b-card-text>
          </b-tab>
        <b-tab title="FAQ">
          <b-card-text>

            <!-- insert accordian  -->
            <div role="tablist">
              <!-- for each item in the items object, add it as a section in the accordian-->
              <!-- declare index so that it can be used for the toggle ids and reference -->
              <b-card no-body class="mb-1" v-for="(item, index) in items" :key="item.id">
                <b-card-header header-tag="header" class="p-1" role="tab">
                  <b-button block v-b-toggle="'accordion-'+index" variant="light">{{item.header}}</b-button>
                </b-card-header>
                <b-collapse :id="'accordion-'+index" visible accordion="my-accordion" role="tabpanel">
                  <b-card-body>              
                    <b-card-text>{{item.text}}</b-card-text>
                  </b-card-body>
                </b-collapse>
              </b-card>
            </div>

          </b-card-text>
        </b-tab>
      </b-tabs>
    </b-card>
  
  </section>
</template>

<script>

export default {
  components: {

  },
  data () {
    return {
      title: 'About: Movie Explorer',
      items: [
        {header: 'Data Sources', 
        text: `Data and trends are pulled from The Movie Database (TMDb). Visit https://www.themoviedb.org/ to 
        see their API documentation for more details.`},
        {header: 'Contact', text: 'C. Lam'}
        ]
    }
  },
   head () {
    return {
      title: this.title,
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        { hid: 'description', name: 'description', content: 'Movie Explorer was created as a student project using the tMDB API.' }
      ]
    }
  }
}

</script>

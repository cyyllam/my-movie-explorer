<template>
<!-- this is the header component and consists of the site header and navigation bar -->
  <section>
    <!-- insert jumbotron -->
    <b-jumbotron class="my-0"> 
      <h1 class="display-3 mb-2">Movie Explorer</h1>
      <p class="lead">Your one stop to find movie trends and stats.</p>
    </b-jumbotron>
  
    <div id="nav">
      <b-navbar toggleable="lg" type="dark" variant="dark">
        <!-- include a bootstrap icon -->
        <b-navbar-brand><b-icon-film></b-icon-film></b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav>
            <!-- embed nuxt-links to -->
            <b-nav-item to="/">Home</b-nav-item>
            <b-nav-item to="/trends">Explore</b-nav-item>
            <b-nav-item to="/about">About</b-nav-item>

          </b-navbar-nav>
        </b-collapse>
      </b-navbar>
    </div>

  </section>
</template>

<script>
import { BIconFilm } from 'bootstrap-vue'

export default {
  components: {
    BIconFilm
  }
}
</script>
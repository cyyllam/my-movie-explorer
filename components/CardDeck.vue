<template>
<!-- this card deck returns space for an image, title, 2 paragraphs, and a footer -->
  <div>
    <b-card  
    style="max-width: 13rem;" 
    class="mb-3" 
    :title="result.title" 
    v-bind:img-src="'http://image.tmdb.org/t/p/w500/' + result.poster_path" 
    v-bind:img-alt="'Poster image of ' + result.title + ' from tMDB'" 
    img-top>
        <b-card-text>
          <p>User rating: {{ result.vote_average }}</p> 
          <p style="font-size: .9rem;">{{ result.overview }}</p>             
        </b-card-text>
        <template v-slot:footer>
            <small class="text-muted">Release Date: {{ result.release_date }}</small>
        </template>
    </b-card>
  </div>
</template>

<script>
export default {
	props: {
    // result: Object
    result: {
      type: Object,
      required: true
    }
    }
}
</script>

<style>


</style>
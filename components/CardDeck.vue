<template>
<!-- this card deck returns space for an image, title, 2 paragraphs, and a footer -->
  <div>
    <b-card  
    style="max-width: 13rem;" 
    class="mb-3" 
    :title="result.title" 
    v-bind:img-src="renderImg(result.poster_path)" 
    v-bind:img-alt="renderImgAlt(result.poster_path, result.title) "
    img-top>
        <b-card-text>
          <slot name="original_title"></slot>
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
  data () {
    return {
      // fallback: 'https://images.unsplash.com/photo-1516541196182-6bdb0516ed27?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=600&q=60'
      fallback: {
        image:'https://images.unsplash.com/photo-1539114283047-162d7e532da4?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=600&q=60',
        alt: 'Image by Fabrizio Conti from Unsplash https://unsplash.com/@staticlaw'
      }
    }

  },
	props: {
    // result: Object
    result: {
      type: Object,
      required: true
    }
    },
  methods: {
    renderImg(anImg) {
      let finalImg = null;
      if (anImg === null) {
        finalImg = this.fallback.image;
      } else {
        finalImg = 'http://image.tmdb.org/t/p/w500/' + anImg;
      }
      return finalImg;
    },
    renderImgAlt(anImg, aTitle) {
      let finalStr = null;
      if (anImg === null) {
        finalStr = this.fallback.alt;
      } else {
        finalStr = 'Poster image of ' + aTitle + ' from tMDB';
      }
      return finalStr;

    }
  }
}
</script>

<style>


</style>
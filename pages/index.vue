<template>
  <section class="opening">
    <div class="opening__box">
      <Intro>
          <p slot="content">
            It's easy to google for a generic list of the best movies to watch, but sometimes that search can be 
            onerous when you have something more specific in mind. Perhaps you're looking for a list of movies trending
            this week, or maybe a list of movies off the beaten path that matches original language or year release criteria. Maybe you just want to know, 
            of the films Ryan Gosling has acted in, which have won awards? Look no further, click on <span class='italics'>Explore</span> to get started.
          </p>
      </Intro>
    </div>
  </section>
</template>

<script>
import Intro from '~/components/intro.vue'

export default {
  data () {
    return {
      title: 'Welcome to the Movie Explorer'
    }
  },
  components: {
    Intro
  },
  head () {
    return {
      title: this.title,
      meta: [
        // hid is used as unique identifier. Do not use `vmid` for it as it will not work
        { hid: 'description', name: 'description', content: 'Movie Explorer is your one stop to discover and query for trending movies. Select the Explore page to begin.' }
      ]
    }
  }
}
</script>

<style lang="scss">

  .opening {
    margin: 5vw 15vw;
    &__box {
      border-top: 1px solid black;
      border-bottom: 1px solid black;
      padding: 4rem;
    }
  }
  .italics {
    font-style: italic;
  }

</style>
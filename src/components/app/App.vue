<template>
  <div class="app font-monospace container">
    <div class="content">
      <app-info :allMoviesCount="movies.length" :favouriteMoviesCount="movies.filter(c => c.favourite).length" />
      <Box>
        <search-panel :updateTermHandler="updateTermHandler" />
        <app-filter :updateFilterHandler="updateFilterHandler" :filterName="filter" />
      </Box>
      <movie-list :movies="onFilterHandler(onSearchHandler(movies, term), filter)" @onToggle="onToggleHandler" @onRemove="onRemoveHandler" />
      <movie-add-form @createMovie="createMovie" />
    </div>
  </div>
</template>


<script>
import AppInfo from "@/components/app-info/AppInfo.vue"
import SearchPanel from "@/components/search-panel/SearchPanel.vue"
import AppFilter from "@/components/app-filter/AppFilter.vue"
import MovieList from "@/components/movie-list/MovieList.vue"
import MovieAddForm from "@/components/movie-add-form/MovieAddForm.vue"
import Box from "@/ui-components/Box.vue"
export default {
  components: {
    AppInfo,
    SearchPanel,
    AppFilter,
    MovieList,
    MovieAddForm,
    Box
  },
  data() {
    return {
      movies: [
        {
          name: "Omar",
          viewers: 811,
          id: 1,
          favourite: false,
          like: true,
          link: "https://qiziqarli.uz/seriall/serial/26-umar-ibn-hattob-1-30-qism-umar-ibn-xattob-ozbek-tilida.html",
        },
        {
          name: "Qog'oz bino",
          viewers: 411,
          id: 2,
          favourite: false,
          like: false,
          link: "https://uzmovi.com/3350-qogoz-bino-premyera-uzbek-ozbek-tilida-barcha-qismlari/episode/11.html",
        },
        {
          name: "Po'lat",
          viewers: 711,
          id: 3,
          favourite: true,
          like: false,
          link: "https://www.youtube.com/watch?v=N_9CQtoz1qE",
        },
      ],
      term: '',
      filter: 'all',
    }
  },
  methods: {
    createMovie(item) {
      this.movies.push(item)
    },
    onToggleHandler({ id, prop }) {
      this.movies = this.movies.map(item => {
        if (item.id === id) {
          return { ...item, [prop]: !item[prop] }
        }
        return item
      })
    },
    onRemoveHandler(id) {
      // console.log(id);
      this.movies = this.movies.filter(c => c.id !== id)
    },
    onSearchHandler(arr, term) {
      if (term.length == 0) {
        return arr
      }

      return arr.filter(c => c.name.toLowerCase().indexOf(term) > -1)
    },

    onFilterHandler(arr, filter) {
      switch (filter) {
        case "popular":
          return arr.filter(c => c.like)
        case "mostViewers":
          return arr.filter(c => c.viewers > 500)
        default:
          return arr
      }
    },
    updateTermHandler(term) {
      this.term = term
    },
    updateFilterHandler(filter){
      this.filter = filter
    }
  }
}
</script>


<style>
.app {
  height: 100vh;
  color: black
}

.content {
  width: 1000px;
  min-height: 700px;
  background-color: #fff;
  margin: 0 auto;
  padding: 5rem 0;
}

.search-panel {
  margin-top: 2rem;
  padding: 1.5rem;
  background-color: #fcfaf5;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15)
}
</style>
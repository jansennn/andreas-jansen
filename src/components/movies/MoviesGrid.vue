<script>
import feather from "feather-icons";
import ProjectsFilter from "./ProjectsFilter.vue";
import MovieSingle from "./MovieSingle.vue";
import projects from "../../data/projects";
import axios from "axios";

export default {
  components: { MovieSingle, ProjectsFilter },
  data: () => {
    return {
      projects,
      projectsHeading: "Movies I've Watched",
      selectedCategory: "",
      searchProject: "",
      movies: [],
    };
  },
  computed: {
    // Get the filtered projects
    filteredProjects() {
      if (this.selectedCategory) {
        return this.filterProjectsByCategory();
      } else if (this.searchProject) {
        return this.filterProjectsBySearch();
      }
      return this.movies;
    },
  },
  methods: {
    // Filter projects by category
    filterProjectsByCategory() {
      return this.movies.filter((item) => {
        let category = item.title.charAt(0).toUpperCase() + item.title.slice(1);
        console.log(category);
        return category.includes(this.selectedCategory);
      });
    },
    // Filter projects by title search
    filterProjectsBySearch() {
      let project = new RegExp(this.searchProject, "i");
      return this.movies.filter((el) => el.title.match(project));
    },
    setMovies(data) {
      this.movies = data;
    },
  },
  mounted() {
    feather.replace();
    axios
      .get("https://profile-andreas-be.onrender.com/movie/rated")
      .then((response) => this.setMovies(response.data.results))
      .catch(function (error) {
        // handle error
        console.log("Gagal : ", error);
      })
      .then(function () {
        // always executed
      });
  },
};
</script>

<template>
  <!-- Projects grid -->
  <section class="pt-10 sm:pt-14">
    <!-- Projects grid title -->
    <div class="text-center">
      <p
        class="font-general-semibold text-2xl sm:text-5xl font-semibold mb-2 text-ternary-dark dark:text-ternary-light"
      >
        {{ projectsHeading }}
      </p>
    </div>

    <!-- Filter and search projects -->
    <div class="mt-1 sm:mt-1">
      <div class="grid place-items-center">
        <img
          class="h-60 w-60"
          src="https://www.themoviedb.org/assets/2/v4/logos/v2/blue_long_2-9665a76b1ae401a510ec1e0ca40ddcb3b0cfe45f1d51b77a308fea0845885648.svg"
        />
      </div>
      <div
        class="flex justify-between border-b border-primary-light dark:border-secondary-dark pb-3 gap-2"
      >
        <div class="flex justify-between gap-2">
          <span
            class="hidden sm:block bg-primary-light dark:bg-ternary-dark p-2.5 shadow-sm rounded-xl cursor-pointer"
          >
            <i
              data-feather="search"
              class="text-ternary-dark dark:text-ternary-light"
            ></i>
          </span>
          <input
            v-model="searchProject"
            class="font-general-medium pl-3 pr-1 sm:px-4 py-2 border-1 border-gray-200 dark:border-secondary-dark rounded-lg text-sm sm:text-md bg-secondary-light dark:bg-ternary-dark text-primary-dark dark:text-ternary-light"
            id="name"
            name="name"
            type="search"
            required=""
            placeholder="Search Movies"
            aria-label="Name"
          />
        </div>
        <ProjectsFilter @filter="selectedCategory = $event" />
      </div>
    </div>

    <!-- Projects grid -->
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 mt-6 sm:gap-10">
      <MovieSingle
        v-for="movie in filteredProjects"
        :key="movie.id"
        :movie="movie"
      />
    </div>
  </section>
</template>

<style scoped></style>

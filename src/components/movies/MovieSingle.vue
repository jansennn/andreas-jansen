<script>
export default {
  props: ["movie"],
};
</script>

<template>
  <router-link
    to="/movies/single-movie"
    class="rounded-xl shadow-lg hover:shadow-xl cursor-pointer mb-10 sm:mb-0 bg-secondary-light dark:bg-ternary-dark"
    aria-label="Single Movie"
  >
    <div>
      <img
        :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path"
        :alt="movie.title"
        class="rounded-t-xl border-none"
      />
    </div>
    <div class="text-center px-4 py-6">
      <p
        class="text-ellipsis overflow-hidden font-general-semibold text-xl dark:text-ternary-light font-semibold mb-2"
        style="overflow: hidden; white-space: nowrap"
      >
        {{ movie.title }}
      </p>
      <span
        class="font-general-medium text-lg text-ternary-dark dark:text-ternary-light"
        >{{ movie.category }}</span
      >
    </div>
  </router-link>
</template>

<style lang="scss" scoped></style>

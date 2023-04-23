<script>
export default {
  setup() {
    return {
      bios: [
        {
          id: 1,
          bio: "Hello and welcome to my website! My name is Andreas Tampubolon and I am a software engineer based in Jakarta, Indonesia. Currently 23 years old, I work for an e-wallet company where I specialize in developing and maintaining software systems.",
        },
        {
          id: 2,
          bio: "As a passionate software engineer, I am dedicated to creating innovative solutions that make people's lives easier. Whether it's designing user-friendly interfaces or streamlining complex processes, I love the challenge of solving problems through code.",
        },
        {
          id: 3,
          bio: "In my free time, I enjoy exploring new technologies and experimenting with different programming languages. I am also an avid reader and enjoy learning about the latest industry trends and developments.",
        },
        {
          id: 4,
          bio: "Thank you for visiting my website and please feel free to reach out if you have any questions or would like to collaborate on a project.",
        },
      ],
    };
  },
};
</script>

<template>
  <div class="block sm:flex sm:gap-10 mt-10 sm:mt-20">
    <!-- About profile image -->
    <div class="w-full sm:w-1/4 mb-7 sm:mb-0">
      <img
        src="@/assets/images/profile-andreas.jpg"
        class="rounded-xl w-96"
        alt=""
      />
    </div>

    <!-- About details -->
    <div class="w-full sm:w-3/4 text-left">
      <p
        v-for="bio in bios"
        :key="bio.id"
        class="font-general-regular mb-4 text-ternary-dark dark:text-ternary-light text-lg"
      >
        {{ bio.bio }}
      </p>
    </div>
  </div>
</template>

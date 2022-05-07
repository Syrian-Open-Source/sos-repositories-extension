<template>
  <div class="root">
    <div class="card" v-for="repository in repositories" :key="repository.id">
      <img src="images/logo.png" alt="Syrian Open Source" />
      <div class="description">
        <h2 class="description__name" @click="openUrl(repository.clone_url)">
          {{ repository.name }}
        </h2>
        <span class="description__type">
          <img src="images/stargazers.png" /> {{ repository.stargazers_count }}, 
          <img src="images/forks.png" /> {{ repository.forks }}
          <img src="images/issues.png" /> {{ repository.open_issues }}
        </span>
      </div>
      <span class="card__price" @click="cloneRepo(repository.clone_url)"
        >Clone</span
      >
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      repositories: [],
      loading: false,
    };
  },
  created() {
    fetch("https://api.github.com/users/Syrian-Open-Source/repos")
      .then((response) => response.json())
      .then((data) => {
        this.repositories = data;
        console.log(data);
      });
  },
  methods: {
    openUrl(url) {
      window.open(url, "_blank");
    },
    cloneRepo(url) {
      window.prompt("Copy to clipboard: Ctrl+C, Enter", `git clone ${url}`);
    },
  },
};
</script>

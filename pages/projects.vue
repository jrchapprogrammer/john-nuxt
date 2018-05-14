<template>
  <section class="section is-medium">
    <div class="container has-text-centered">
      <h1 class="title">My Projects</h1>
      <GitRepo :url='url' :repoName='repoName' :owner='owner' :made='made' :description='description'/>
      <p>
        Some of my projects can be found on <a href="https://github.com/jrchapprogrammer" target="_blank">GitHub</a>.
      </p>
    </div>
  </section>
</template>

<script>
import axios from "axios";
import GitRepo from "../components/GitRepo";
export default {
  components: GitRepo,
  name: "Projects",
  data() {
    return {
      data: []
    };
  },
  async asyncData({ params }) {
    let { data } = await axios.get(
      `https://api.github.com/users/jrchapprogrammer/repos?type=owner${
        params.id
      }`
    );
    return { project: data };
  },
  head() {
    return {
      url: this.project.url,
      repoName: this.project.name,
      owner: this.project.owner,
      made: this.project.deployments_url.created_url,
      description: this.project.description
    };
  }
};
</script>

<style scoped>

</style>
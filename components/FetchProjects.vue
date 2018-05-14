<template>
    <div>
        <!-- iterates over Github repos and outputs select repo data -->
        <ul v-if="projects && projects.length">
            <li v-for="project of projects" :key="project">
                <a :href="project.url" target="_blank">
                    <h2>{{project.name}}</h2>
                </a>
                <p><strong>{{project.owner}}</strong></p>
                <p>{{project.deployments_url.created_at}}</p>
                <p>{{project.description}}</p>
            </li>
        </ul>

        <ul v-if="errors && errors.length">
            <li v-for="error of errors" :key="error">
            {{error.message}}
            </li>
        </ul>    
    </div>
</template>

<script>
import axios from "axios";
export default {
  name: "FetchProjects",
  data: function() {
    return {
      projects: {},
      errors: []
    };
  },
  async created() {
    try {
      // Fetches Github repo data from API
      const response = await axios.get(
        "https://api.github.com/users/jrchapprogrammer/repos?type=owner"
      );
      this.projects = response.data;
    } catch (e) {
      this.errors.push(e);
    }
  }
};
</script>

<style scoped>
li {
  list-style-type: none;
}
a {
  text-decoration: none;
}
</style>
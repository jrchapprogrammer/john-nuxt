<template>
    <div>
        <!-- iterates over Github repos and outputs select repo data -->
        <ul v-if="projects && projects.length">
            <li v-for="project of projects" :key="project">
                <a :href="url" target="_blank">
                    <h2>{{ repoName }}</h2>
                </a>
                <p><strong>{{ owner }}</strong></p>
                <p>{{ made }}</p>
                <p>{{ description }}</p>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
  name: "GitRepo",
  props: ["url", "repoName", "owner", "made", "description"]
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
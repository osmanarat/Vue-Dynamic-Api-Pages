<template>
  <div>
    <h1>{{title}}</h1>
    <!-- <p> <img style="width:300px; height:300px;" :src="image"> </p> -->
    <p> {{description}}</p>
  <div>
    <p><strong>Continent:</strong> {{ continent }}</p>
    <p><strong>Mountain:</strong> {{ mountain }}</p>
    <p><strong>Path:</strong> {{ $route.path }}</p>
    </div>


    <NuxtLink to="/">Back to Mountains</NuxtLink>
  </div>
</template>
<script>
export default {
  async asyncData({ params, redirect }) {
    const mountains = await fetch(
      "https://api.nuxtjs.dev/mountains"
    ).then((res) => res.json());

    const filteredMountain = mountains.find(
      (el) =>
        el.continent.toLowerCase() === params.continent &&
        el.slug === params.mountain
    );
    if (filteredMountain) {
      return {
        continent: filteredMountain.continent,
        mountain: filteredMountain.title,
        image: filteredMountain.image,
        description:filteredMountain.description,
        title:filteredMountain.title
      };
    } else {
      redirect("/");
    }
  },
};
</script>

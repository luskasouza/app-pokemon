<template>
  <q-page
    ><div class="rows">
      <q-table
        dense
        color="s"
        :loading="loading"
        title="Treats"
        :rows="posts"
        :columns="columns"
        row-key="name"
        class="col"
      />
    </div>
    <!--<div>{{ posts }}</div>-->
  </q-page>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      loading: false,
      nextPage: 2,
      user: {},
      columns: [
        { name: 'name', label: 'name', field: 'name', align: 'left' },
        { name: 'url', label: 'url', field: 'url', align: 'left' },
      ],
      posts: [],
    };
  },
  created() {
    this.user = 'OK';
  },
  mounted() {
    console.log('mounted');
    return this.getPosts();
  },
  methods: {
    getPosts() {
      this.$axios
        .get('https://pokeapi.co/api/v2/pokemon/')
        .then((response) => {
          return (this.posts = response.data.results);
        })
        .finally(() => {
          setTimeout(() => {
            this.loading = false;
          }, 500);
        });
    },
  },
};
</script>

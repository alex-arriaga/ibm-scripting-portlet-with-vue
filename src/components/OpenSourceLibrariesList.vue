<template>
    <div class="row">
        <div class="col-12">
            <h2 class="mt-4 pb-3">Open Source Libraries</h2>
        </div>
        <div class="col-12 col-sm-6 col-md-4" v-for="library in libraries"
             :key="library.name">

            <article class="b-library bg-info">
                <h3 class="b-library__title">{{library.name}}</h3>
                <div>
                    <strong>Number of projects: </strong>
                    <span>{{library.project_count}}</span>
                </div>
                <div>
                    <strong>Default Language: </strong>
                    <span>{{library.default_language}}</span>
                </div>
                <!--:style="{borderBottomColor: library.color}"-->
                <a :href="library.homepage" target="_blank"
                   class="b-library__link btn btn-sm mt-3"
                   :style="{borderBottomColor: library.color}">
                    Visit its page
                </a>
            </article>

        </div>
    </div>
</template>

<script>
  import axios from 'axios';

  export default {
    name: 'OpenSourceLibrariesList',
    data() {
      return {
        libraries: [],
      };
    },
    created() {
      const serviceURL = 'https://libraries.io/api/platforms?api_key=f2a7cc8cba94821b0c90dda513499a75';
      const config = {};
      axios.get(serviceURL, config).then(response => {
        console.log(response.data);
        this.libraries = response.data;
      });
    },
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
    .b-library {
        margin-bottom: 20px;
        transition: all .3s ease-in-out;
        padding: 10px;
        color: white;

        .b-library__title {
            color: white;
            margin: 0;
        }

        .b-library__link {
            border-width: 3px;
            color: white;
            text-decoration: none;
        }
    }

    .b-library:hover {
        transform: translateY(-10px);
        box-shadow: 0 10px 30px 0 rgba(0, 0, 0, .1);
    }
</style>

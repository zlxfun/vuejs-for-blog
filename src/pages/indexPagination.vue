<template>
  <archives-show :Archives="Archives" :url="'/page/'" isPagination="1" @on-pagination="getArchivesList($event)">
    <div slot="archives-type-desc">
      <!--暂无-->
    </div>
  </archives-show>
</template>

<script>
  import ArchivesShow from '../components/archivesShow'
  export default {
    components: {
      ArchivesShow
    },
    created: function () {
      this.getArchivesList();
    },
    data () {
      return {
        Archives: [],
        page: this.$route.params.num
      }
    },
    methods: {
      getArchivesList (page) {  //分页获取文章
        if(this.page != 0) {
          page = this.page;
          this.page = 0;
        }
        //h5中无刷新修改
        this.$router.push({ name: 'indexPagination', params: { num: page }});
        this.$http.get('/api/getPagination?num='+page)
          .then((res) => {
          this.Archives = res.data;
        }, (err) => {
          console.log(err);
        })
      }
    }
  }
</script>

<style scoped>
</style>

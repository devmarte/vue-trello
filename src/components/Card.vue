<template>
  <div>
      Card
      <div v-if="loading">
          loading card...
      </div>
      <div v-else>{{cid}}</div>
  </div>
</template>

<script>
export default {
    data() {
        return{
            cid: 0,
            loading: false,
            moon: '',
        }
    },
    watch: {
        '$route':{
            handler: 'fetchData',
            immediate: true
        }
    },
    created() {
        this.fetchData()
    },
    methods:{
        fetchData() {
            this.loading = true;
            setTimeout(()=> {
                this.cid = this.$route.params.cid;
                this.loading = false;
            }, 500)
        }
    }
}
</script>

<style>

</style>
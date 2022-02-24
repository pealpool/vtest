<template>
  <div class="row">
    <div class="card"
         v-show="!da.searching"
         v-for="u in da.userInfo" :key="u.login"
    >
      <a :href="'https://github.com/'+u.login" target="_blank">
        <img :src="u.avatar_url" style='width: 100px'/>
      </a>
      <p class="card-text">{{u.login}}</p>
    </div>
<!--    <div v-show="da.searching" class="textC">Welcome！</div>-->
    <div v-show="da.searching" class="textC">Searching!</div>
    <div v-show="da.err" class="textC">Error:</div>
  </div>
</template>

<script>
export default {
  name: 'GaCon',
  data(){
    return{
      da:{
        userInfo:[],
        searching:false,
        err:false
      }
    }
  },
  methods:{
    traData(uInfo){
      this.da = {...this.da,...uInfo}
    }
  },
  mounted() {
    this.$bus.$on('traData',this.traData)
  },
  beforeDestroy() {
    this.$bus.$off('traData',this.traData)
  }
}
</script>

<style>

.card {
  float: left;
  width: 33.333%;
  padding: .75rem;
  margin-bottom: 2rem;
  border: 1px solid #efefef;
  text-align: center;
}

.card > img {
  margin-bottom: .75rem;
  border-radius: 100px;
}

.card-text {
  font-size: 85%;
}

.textC{
  font-size: 30px;
}
</style>

<template>
  <div class="dashboard-editor-container">
    <!-- <div class=" clearfix">
      <pan-thumb :image="avatar" style="float: left">
        Your roles:
        <span v-for="item in roles" :key="item" class="pan-info-roles">{{ item }}</span>
      </pan-thumb>
      <div class="info-container">
        <span class="display_name">{{ name }}</span>
        <span style="font-size:20px;padding-top:20px;display:inline-block;">{{ roles.join('|') }}'s Dashboard</span>
      </div>
    </div> -->
    <div>
      <p>As Opções são </p>
      <p v-for="option in options" :key="option">{{ options.option }}</p>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';
import RoletaResource from '@/api/resource.js';
const roletaResource = new RoletaResource('roleta');

export default {
  name: 'DashboardEditor',
  data() {
    return {
      emptyGif: '',
      options: [],
    };
  },
  computed: {
    ...mapGetters([
      'name',
      'avatar',
      'roles',
    ]),
  },
  created(){
    this.getRoletaOptions();
  },
  methods: {
    async getRoletaOptions() {
      const data = await roletaResource.list();
      console.log(data);
      this.options = data;
    },
  },
};
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
  .emptyGif {
    display: block;
    width: 45%;
    margin: 0 auto;
  }

  .dashboard-editor-container {
    background-color: #e3e3e3;
    min-height: 100vh;
    padding: 50px 60px 0px;
    .pan-info-roles {
      font-size: 12px;
      font-weight: 700;
      color: #333;
      display: block;
    }
    .info-container {
      position: relative;
      margin-left: 190px;
      height: 150px;
      line-height: 200px;
      .display_name {
        font-size: 48px;
        line-height: 48px;
        color: #212121;
        position: absolute;
        top: 25px;
      }
    }
  }
</style>

<template>
  <div class="header">
    <div class="container">
      <div class="header-inner">
        <h2>Todo Listo</h2>
      </div>
    </div>
  </div>
  <table-component></table-component>
</template>

<style scoped>
  .container {
    width: 1440px;
    margin: 0px auto;
  }

  .header-inner{
    padding: 30px 0px;
  }
  .header-inner h2{
    font-size:40px;
    font-weight: bold;
  }

  @media screen and (max-width: 768px) {
    .container {
      width: 100% !important;
      padding: 0px 15px;
    }
  }
</style>

<script>
import TableComponent from '@/components/table.vue';

export default {
  components: {
    'table-component': TableComponent
  },
};
</script>

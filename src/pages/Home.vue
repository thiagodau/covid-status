<template>
  <div>
    <div class="container">
      <h1>COVID19 - Status by BrazilApi</h1>
      <img :src="imageCovid" />
    </div>
    <Dados />
  </div>
</template>

<script>
import imageCovid from "../assets/coronavirus.svg";

import Dados from "../components/Dados";

export default {
  data: function () {
    return {
      imageCovid,
    };
  },
  components: {
    Dados,
  },
};
</script>

<style>
.container {
  padding: 30px;
  display: flex;
  align-items: center;
}

.container img {
  width: 5%;
  margin-left: 20px;
}
</style>
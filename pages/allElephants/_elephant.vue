<template>
  <div class="container">
    <sidenav />
    <div class="dashboard-view-container">
      <p class="title">Acumen Digital Interview Task / Elephantom > Elephant</p>
    </div>
    <div class="content">
      <div class="elephant-div">
        <img :src="`${image}`" class="elephant-img" />
      </div>

      <div class="tuffi-text">
        <div class="info">
          <p>
            <span class="tuffi-header">{{ name }}</span
            >{{ sex }}
          </p>
        </div>

        <div>
          <p class="tuffi-paragraph">{{ note }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import sidenav from '../../components/sidenav.vue'
export default {
  components: { sidenav },
  data() {
    return {
      tableData: [],
      elephantsId: '',
      name: '',
      sex: '',
      note: '',
      image: '',
    }
  },
  created() {
    this.getElephantsbyId()
  },

  methods: {
    async getElephantsbyId() {
      const baseUrl = 'http://acumen-elephantom.herokuapp.com/elephants/id/'
      const elephantIdPromise = await fetch(
        baseUrl + this.$route.params.elephant
      )
      const elephantsIdJson = elephantIdPromise.json()
      elephantsIdJson.then((response) => {
        if (!response.error) {
          this.image = response.data.image
          this.name = response.data.name
          this.sex = response.data.sex
          this.note = response.data.note
          console.log(this.$route)
          console.log(response)
        }
      })
    },
  },
}
</script>

<style scoped>
.container {
  width: 100%;
  overflow: hidden;
}
.content {
  /* width: 100%; */
  margin-left: 380px;
  padding: 1px 16px;
  overflow: hidden;
}
.dashboard-view-container {
  background: #ffffff;
  box-shadow: 0px -7px 24px rgba(0, 0, 0, 0.25);
  padding: 25px 20px;
  padding: 34px 35px 31px;
  width: 90%;
  margin-left: 360px;
}
.dashboard-view p,
.title {
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 28px;
  color: #30425a;
}

.elephant-div {
  margin: 40px;
  width: 100%;
  position: relative;
}
.elephant-div::after {
  position: absolute;
  background: linear-gradient(
    180deg,
    hsla(0, 0%, 76.9%, 0) -1.55%,
    rgba(29, 29, 242, 0.36863) 77.84%
  );
  bottom: 6px;
  width: 70%;
  content: '';
  top: 0;
  left: 0;
}
.elephant-img {
  width: 70%;
}
.tuffi-header {
  font-style: normal;
  font-weight: bold;
  font-size: 48px;
  line-height: 74px;
  color: #30425a;
  padding: 30px 10px 30px 0px;
}
.info {
  border-bottom: 1px solid rgba(196, 205, 213, 0.62);
  width: 70%;
}
.tuffi-text {
  font-style: normal;
  font-weight: normal;
  font-size: 18px;
  line-height: 28px;
  color: #30425a;
  margin: 40px;
  width: 100%;
}

.tuffi-paragraph {
  font-style: normal;
  font-weight: normal;
  font-size: 24px;
  line-height: 37px;
  width: 70%;
  color: #30425a;
  padding: 30px 0;
}
@media screen and (max-width: 700px) {
  .content {
    /* width: 100%; */
    margin-left: 0;
    padding: 1px 16px;
  }
  .dashboard-view-container {
    padding: 20px 20px;
    margin-top: 40px;
    margin-left: 200px;
    margin: 40px auto 0;
  }
  .dashboard-view p,
  .title {
    font-style: normal;
    font-weight: 400;
    font-size: 18px;
    line-height: 23px;
    color: #30425a;
  }

  .animal-div {
    margin: 30px 0;
    background: #ffffff;
    box-shadow: 0px 3px 10px -3px rgba(0, 0, 0, 0.25);
    width: 100%;
  }
  .animal-header {
    width: 100%;
  }
  .elephant-div {
    margin: 40px auto;
    width: 80%;
  }
  .elephant-img {
  /* width: 70%; */
  width: 100%;
}
.elephant-div::after {
  width: 100%;
}
.info {
  width: 82%;
}
}
</style>

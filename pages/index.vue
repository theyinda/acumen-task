<template>
  <div class="container">
    <sidenav />
    <div class="dashboard-view-container">
      <p class="title">Acumen Digital Interview Task / Elephantom</p>
    </div>
    <section class="dashboard-view">
      <div class="animal-div">
        <div class="animal-header">
          <h2>All Elephants</h2>
        </div>
        <div class="animal-table">
          <table>
            <thead>
              <tr class="table-header">
                <th>S/N</th>
                <th>Name</th>
                <th>Species</th>
                <th>Sex</th>
                <th>Affiliation</th>
                <th>Dob</th>
              </tr>
            </thead>

            <tr
              v-for="records in tableData"
              :key="records._id"
              @click="$router.push('/allElephants/' + records._id)"
            >
              <td class="">{{ records.index }}</td>
              <td class="">{{ records.name }}</td>
              <td class="">{{ records.species }}</td>
              <td class="">{{ records.sex }}</td>
              <td class="">{{ records.affiliation }}</td>
              <td class="">{{ records.dob }}</td>
            </tr>
          </table>
          <div class="pagination-container">
            <div class="pagination">
              <p>PAGE {{ currentPage }} OF {{ totalPages }}</p>
            </div>
            <div class="pagination-controls">
              <button
                class="page-left"
                :disabled="currentPage === 1"
                @click="previous"
              >
                ❮ &nbsp;
              </button>
              <button type="button" class="pageOne">{{ currentPage }}</button>
              <button
                type="button"
                class="pageTwo"
                :disabled="currentPage === totalPages"
                @click="next"
              >
                {{ currentPage + 1 }}
              </button>
              <button
                class="page-right"
                :disabled="currentPage === totalPages"
                @click="next"
              >
                ❯ &nbsp;
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import sidenav from '../components/sidenav.vue'
export default {
  components: { sidenav },
  data() {
    return {
      tableData: [],
      currentPage: 1,
      totalPages: 0,
      size: 0,
    }
  },
  created() {
    this.getElephants(0)
  },

  methods: {
    async getElephants(page) {
      const promise = await fetch(
        'http://acumen-elephantom.herokuapp.com/elephants/asian'
      )
      const elephantsJson = promise.json()
      elephantsJson.then((res) => {
        // this.tableData = res.data
        console.log(page)
        this.tableData = []
        const Elephants = res.data
        this.size = Elephants.length
        this.totalPages = Math.round(this.size / 8)
        Elephants.forEach((animal, index) => {
          if (index >= page && index <= page + 7) {
            this.tableData.push({
              _id: animal._id,
              index: index + 1,
              name: animal.name,
              species: animal.species,
              sex: animal.sex,
              affiliation: animal.affiliation,
              dob: animal.dob,
            })
          }
        })
      })
    },
    previous() {
      const previousPage = (this.currentPage - 2) * 8
      this.getElephants(previousPage)
      --this.currentPage
    },
    next() {
      const nextpage = this.currentPage * 8
      this.getElephants(nextpage)
      ++this.currentPage
    },
  },
}
</script>

<style scoped>
.container {
  width: 100%;
   background: #f5f8ff;
   overflow: hidden;
}
.dashboard-view {
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

.animal-div {
  margin: 30px 0;
  margin-top: 60px;
  background: #ffffff;
  box-shadow: 0px 3px 10px -3px rgba(0, 0, 0, 0.25);
  width: 80%;
  overflow-x: scroll;
}
a.nuxt-link-exact-active {
  background: #b9b9ff;
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 23px;
  color: #fff !important;
}
.animal-header {
  width: 100%;
}
.animal-header h2 {
  font-weight: 700;
  font-size: 18px;
  line-height: 23px;
  color: #30425a;
  padding: 20px 25px;
}
.animal-table {
  width: 100%;
  margin: 10px auto;
}
table {
  border-spacing: 0px;
  width: 100%;
}

.table-header {
  background: #e5e5e5;
  width: 10%;
}

tr:nth-of-type(even) {
  background-color: #f5f5f5;
}
tr:hover{
  background: #ddddff;
  cursor: pointer;
}
td {
  padding: 25px;
  width: 10%;
  text-align: left;
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 20px;
  color: #848383;
  
}

th {
  padding: 25px;
  text-align: left;
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 23px;

  color: #000000;
}
.pagination-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.pagination p {
  font-style: normal;
  font-weight: normal;
  font-size: 14px;
  line-height: 15px;
  color: #30425a;
  opacity: 0.9;
  padding: 35px 0;
}
button {
  margin-left: 15px;
}
.pageOne,
.pageTwo {
  background: #ffffff;
  border: 1px solid #dfe3e8;
  box-sizing: border-box;
  border-radius: 4px;
  padding: 8px 15px;
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
}

.pageOne,
.pageTwo :active {
  color: #0546e0;
  border: 1px solid #0546e0;
}
.page-left,
.page-right {
  background: #ffffff;
  border: 1px solid #dfe3e8;
  box-sizing: border-box;
  border-radius: 4px;
  color: #c4cdd5;
  padding: 9.5px 13px;
  text-align: center;
  font-style: normal;
  font-weight: bold;
  font-size: 14px;
  line-height: 20px;
}
.pagination-controls button:disabled {
  background: #919eab;
  opacity: 0.5;
  border-radius: 4px;
  cursor: not-allowed;
}
.active {
  border-color: #0546e0;
  color: #0546e0;
}
@media screen and (max-width: 700px) {
  .dashboard-view {
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
  .animal-table {
    overflow-x: scroll;
  }
}
</style>

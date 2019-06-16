<template>
    <div>
        <h4>Customers</h4>
         <div class="form-row">
          <div class="col-10">
            <input type="text" class="form-control" placeholder="Enter key word  ..." v-model="search" v-on:keyup="getfilteredData">
          </div>
        </div>
        <p class="mt-3" align="right">Page: {{ currentPage }} of {{ Math.ceil(rows/perPage) }}</p>
       <div>
          <b-table id="cust-table"
            striped
            :items="filteredData"
            :per-page="perPage"
            :current-page="currentPage">
          </b-table>
        </div>
        <div>
          <b-pagination
            v-model="currentPage"
            :total-rows="rows"
            :per-page="perPage"
            first-text="⏮"
            prev-text="⏪"
            next-text="⏩"
            last-text="⏭"
            align="center"
            aria-controls="cust-table"
            ></b-pagination>
        </div>
    </div>
</template>

<script>
export default {
  data () {
    return {
      apiData: [],
      filteredData: [],
      perPage: 10,
      currentPage: 1,
      search: ''
    }
  },
  computed: {
    rows () {
      return this.filteredData.length
    }
  },
  methods:{
    getfilteredData: function () {
      this.filteredData = this.apiData
      let filteredDataBySearch = []
      // then filter according to keyword, for now this only affects the name attribute of each data
      if (this.search !== '') {
        filteredDataBySearch = this.filteredData.filter(obj => obj.firstName.toLowerCase().indexOf(this.search.toLowerCase()) >= 0)      
        this.filteredData = filteredDataBySearch
      }
    }
  },
  mounted: function() {
    fetch('http://localhost:51770/api/customer', { 
      method: 'get' 
    })
    .then((response) => response.json())
    .then((jsonData) => {
      this.apiData = jsonData
    })
  }
}
</script>

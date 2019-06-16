<template>
    <div>
        <h3>Customers</h3>
        <p class="mt-3" align="right">Page: {{ currentPage }} of {{ rows/perPage }}</p>
       <div>
          <b-table id="cust-table"
            striped
            :items="apiData"
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
      perPage: 10,
      currentPage: 1
    }
  },
  computed: {
    rows () {
      return this.apiData.length
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

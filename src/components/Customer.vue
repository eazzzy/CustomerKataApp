<template>
    <div>
        <h1>Customers</h1>
    </div>
</template>

<script>
export default {
  data () {
    return {
      apiData: []
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

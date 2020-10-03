<template>
<div>
    <v-row>
        <v-col v-if="loading">
           <v-progress-circular
                indeterminate
                color="primary"
                    />
        </v-col>
        <v-col v-else>

             <card 
                :data="data"
             />
        </v-col>
    </v-row>
</div>
</template>

<script>
import card from './CardDialog'
import axios from 'axios'
export default {
    components: {
        card
    },
    data: () => ({
        data: '',
        id: '',
        loading: true
    }),
    created() {
        this.id = this.$route.fullPath.split('=')[1]
        this.fecthData()
    },
     methods : {
    fecthData() {
      axios.get('https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&api_key=p1v9iusZJSsWsj5taNVjJIfAGOg9mdzezScnD7G1&fbclid=IwAR2ELljNBooebWE-Wxr09YjVnqZKCSLCjn8bAYPTW-DkUWY0pwF8BHo9SJg')
      .then((res) => {
          this.data = res.data.photos.find(element => element.id == this.id)
          this.loading = false
      })
    }
  },
}
</script>
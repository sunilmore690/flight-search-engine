<template>
  <div class="container">
    <div><h2> Flight Search Engine</h2></div>
    <el-row>
      <el-col :span="8" :sm="8" :xs="24">
        <FilterFlights @onChangeFilter="onChangeFilter" @onPriceChange="onPriceChange" />
      </el-col>
      <el-col :span="16" :xs=24>
        <div>
          <span v-if='filters.source_code'>
            {{filters.source_code}} > {{filters.destination_code}}
          </span>
          
        </div>
        <Flights
          
          :flights="flights"
          
        />
      </el-col>
    </el-row>
  </div>
</template>

<script>
import Flights from "./components/Flights.vue";
import FilterFlights from "./components/FilterFlights.vue";
import { flights } from "./flights-data";
import _ from "underscore";
export default {
  name: "app",
  data() {
    return {
      flights,
      filters:{}
    };
  },
  components: {
    Flights,
    FilterFlights
  },
  methods: {
    onChangeFilter(filters) {
      console.log("filters", filters);
      this.filters = filters,
      this.flights = _.where(flights, filters);
    },
    onPriceChange(price_range) {
      console.log('hi',price_range)
      this.flights = this.flights.filter(flight=>parseInt(flight.fare.split(" ")[1], 10) >=price_range[0] && parseInt(flight.fare.split(" ")[1], 10) <=price_range[1])
    }
  },
  created() {}
};
</script>

<style>
body {
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  line-height: 1.6;
  /* background: #e8f7f0; */
}
.container {
  margin: 20px;
}
</style>

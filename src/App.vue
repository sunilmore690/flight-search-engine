<template>
  <div>
    <div class="site-title">
      <h2>Flight Search Engine</h2>
    </div>
    <div class="container">
      <el-row class="search-title">
        <el-col :span="8" :sm="8" :xs="24">
          <FilterFlights
            @onChangeFilter="onChangeFilter"
            @resetFilter="resetFilter"
            @onPriceChange="onPriceChange"
          />
        </el-col>
        <el-col :span="16" :xs="24">
          <div class="search-title">
            <span v-if="filters.source_code">{{filters.source_code}} > {{filters.destination_code}}</span>
          </div>
          <Flights :flights="flights" v-loading="loading" />
        </el-col>
      </el-row>
    </div>
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
      loading: false,
      flights,
      filters: {}
    };
  },
  components: {
    Flights,
    FilterFlights
  },
  methods: {
    onChangeFilter(filters) {
      console.log("filters", filters);
      this.filters = filters;
      this.loading = true;
      setTimeout(() => {
        this.flights = _.where(flights, filters);
        this.loading = false;
      }, 500);
    },
    onPriceChange(price_range) {
      console.log("hi", price_range);
      this.loading = true;
      setTimeout(() => {
        this.flights = this.flights.filter(
          flight =>
            parseInt(flight.fare.split(" ")[1], 10) >= price_range[0] &&
            parseInt(flight.fare.split(" ")[1], 10) <= price_range[1]
        );
        this.loading = false;
      }, 500);
    },
    resetFilter() {
      this.flights = flights;
      this.filters = {};
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
.search-title {
  margin-bottom: 30px;
}
.site-title {
  position: sticky;

  z-index: 5000;
  background: white;
  top: 0px;
  height: 50px;
}
</style>

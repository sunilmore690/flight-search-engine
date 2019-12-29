<template>
  <div>
    <el-tabs v-model="activeTab" @tab-click="handleClick" class="flilter-tabs">
      <el-tab-pane label="One Way" name="first"></el-tab-pane>
      <el-tab-pane label="Round Trip" name="second"></el-tab-pane>
     
    </el-tabs>
    <el-form ref="form" :model="form" label-width="120px" class="flight-filters">
      <el-select v-model="filters.source_code" filterable placeholder="Enter Origin City">
        <el-option v-for="item in cities" :key="item.value" :label="item.label" :value="item.value"></el-option>
      </el-select>
      <br />
      <el-select v-model="filters.destination_code" filterable placeholder="Enter Destination City">
        <el-option v-for="item in cities" :key="item.value" :label="item.label" :value="item.value"></el-option>
      </el-select>
      <br />
      <el-date-picker v-model="departure_date" type="date" placeholder="Departure Date"></el-date-picker>
      <br />
      <template  v-if="activeTab === 'second'">
        <el-date-picker v-model="return_date" type="date" placeholder="Return Date"></el-date-picker>
      <br />
      </template>
      
      <el-select v-model="value" placeholder="Passengers">
        <el-option v-for="item in 30" :key="item+'passenger'" :label="item" :value="item"></el-option>
      </el-select>
      <br />
      <el-button type="warning" @click="handleSearch">Search</el-button>
      <el-button plain @click="resetFilter">Reset</el-button>
    </el-form>
    <div class="price-slider">
      <div class="block">
        <div>Refine Flight Search</div>
        <el-slider v-model="price_range" range :max="12000"></el-slider>
      </div>
    </div>
  </div>
</template>

<script>
import { cities } from "../flights-data";
export default {
  name: "FilterFlights",
  data() {
    return {
      activeTab:'first',
      filters: {},
      departure_date: "",
      return_date: "",
      cities,
      price_range: [0, 12000]
    };
  },
  watch: {
    price_range(price_range) {
      console.log(price_range);
      this.$emit("onPriceChange", price_range);
    }
  },
  methods: {
    handleSearch() {
      this.$emit("onChangeFilter", this.filters);
    },
    resetFilter() {
      this.filters = {};
      this.$emit("resetFilter", this.filters);
    },
    handleClick(tab){
      console.log('tab',tab.name)
      this.activeTab = tab.name;

    }
  }
};
</script>

<style >
.price-slider {
  margin-top: 30px;
}
.el-input {
  margin-bottom: 10px;
}
/* .el-date-editor input {
  margin-bottom: 10px;
  width: 100%
}
.flight-filters{
  border:1px solid grey;
} */
form > div,.flilter-tabs,
.el-slider {
  width: 70% !important;
}
@media only screen and (max-width: 600px) {
  form > div,
.el-slider {
  width: 100% !important;
}
}
</style>

<template>
  <div>
    <el-card class="box-card" v-for="flight in flights" :key="flight.flight_id">
      <span class="flight-fare">{{flight.fare}}</span><br>
      <span>{{flight.flight_id}}</span><br>
      <span>{{flight.source_code}} > {{flight.destination_code}}</span><br>
      <span>Depart: {{flight.departs_at}}</span><br>
      <span>Arrives: {{flight.arrives_at}}</span><br>
    </el-card>
  </div>
</template>

<script>
export default {
  props: ["flights"],
  data() {
    return {
      flightsdata: []
    };
  },
  watch: {
    flights(data) {
      this.flightsdata = data;
    }
  }
};
</script>

<style>
.box-card {
  margin-bottom: 10px;
}
.flight-fare{
  font-size: large;
  font-weight: bolder
}
</style>

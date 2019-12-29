<template>
  <div>
    <el-card class="box-card" v-for="flight in flights" :key="flight.flight_id">
      <el-col :span="16">
        <span class="flight-fare">{{flight.fare}}</span>
        <br />
        <span>{{flight.flight_id}}</span>
        <br />
        <span>{{flight.source_code}} > {{flight.destination_code}}</span>
        <br />
        <span>Depart: {{flight.departs_at}}</span>
        <br />
        <span>Arrives: {{flight.arrives_at}}</span>
        <br />
      </el-col>
      <el-col :span="8" class='book-flight-btn'>
        <el-button type="warning" plain size='small'>Book Flight</el-button>
      </el-col>
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
.flight-fare {
  font-size: large;
  font-weight: bolder;
}
.book-flight-btn{
 padding-top: 80px;
}
</style>

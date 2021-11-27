<template>
  <div>
    <h1>Filters</h1>
    <h2>Periode</h2>
    <select v-model="periode" v-bind:value="this.periode" id="periode" v-on:change="submit">
      <option value="1">today</option>
      <option value="7">this week</option>
      <option value="30">wthis month</option>
    </select>
    <h2>Kind of articles</h2>
    <select v-model="kind" v-bind:value="this.kind" id="kind" v-on:change="submit">
      <option value="mostpopular" selected>Most popular</option>
      <option value="movies">Movie review</option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'Menu',
  data() {
    return {
      periode: "1",
      kind: "mostpopular"
    }
    
  },
  methods: {
    submit: function() {
      this.$emit("periodeData", this.periode);
      this.$emit("kindData", this.kind);
    }
  }
}
</script>

<style scoped>
h1{
  text-align: center;
  width: 100%;
  box-shadow: 0 2px 10px 0 grey;
  height: 40px;
  top:0;
  margin: 0;
  padding-top: 10px;
}
h2{
  padding:10px;
  padding-bottom: 0;
}
select{
  margin:0 10px;
  outline: none;
    border: none;
    width: 200px;
    height: 30px;
    border-radius: 15px;
    box-shadow: 0 2px 3px 0 grey;
}
</style>

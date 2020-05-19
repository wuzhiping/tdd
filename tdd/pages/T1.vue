<template>
  <div v-cloak>
    <i-select v-model="model5" style="width:200px">
      <i-option v-for="item in cityList" :value="item.value" :key="item.value">{{ item.label }}</i-option>
    </i-select>
  </div>
</template>

<script>
module.exports = {
  components: {},
  data() {
    return {
      model5:'',
      cityList: [
        {
          value: "New York",
          label: "New York"
        },
        {
          value: "London",
          label: "London"
        },
        {
          value: "Sydney",
          label: "Sydney"
        }
      ]
    };
  },
  watch: {
    "$store.state.data"() {
      console.dir("watch...");
      console.dir(this.$store.state);
    },
    model5(val){
      if(val == 'London'){
        this.$router.push({name:'list'})
                //.catch(err=>{});
      }
    }
  },
  methods: {
    submit: function(data) {
      console.dir(this.$store.state);
      $.Toast.error(JSON.stringify(data), this.$store.state.bizId);

      this.$store.commit("write", {
        isValid: true,
        data: {
          bizId: "biz",
          variables: {},
          log: {},
          opinion: "", //default: button name
          opinions: []
        }
      });
      // console.dir( this.$refs.form.$f.formData() );
    },
    
  },
  created: function() {
    this.$store.commit("error", "请先保存表单");
  },
  mounted: function() {
    this.rule = {};
  }
};
</script>

<style scoped>
s
</style>

<template>
  <div>
    <h1>{{$t("demo.message")}}</h1>
    <form-create ref="form" v-model="model" :rule="rule" :option="option"></form-create>
  </div>
</template>

<script>
module.exports = {
  components: {},
  data() {
    return {
      model: {},
      option: {
        form: {
          labelWidth: 100,
          showMessage: true,
          size: "large"
        },
        row: {
          gutter: 10
        },
        submitBtn: {
          show: false,
          type: "warning",
          long: true,
          icon: "refresh",
          innerText: "save",
          loading: false,
          col: {
            span: 4,
            push: 3
          }
        },
        resetBtn: false
      },
      rule: []
    };
  },
  methods: {},
  created: function() {
    for (var i = 0; i < 15; i++) {
      this.rule.push({
        type: "DatePicker",
        field: "start"+i,
        title: this.$t("demo.start"),
        value: new Date(),
        props: {
          type: "date",
          format: "yyyy-MM-dd",
          placeholder: "请选择起始时间"
        }
      });
    }
  },
  mounted: function() {}
};
</script>

<style scoped>
</style>

<template>
  <div v-cloak>
    <h1 v-if="$IN('admin')">{{$t("demo.message")}}</h1>
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
        onSubmit: this.submit,
        submitBtn: {
          show: true,
          type: "info",
          long: false,
          icon: "refresh",
          innerText: "save",
          loading: false        },
        resetBtn: false
      },
      rule: []
    };
  },
  watch: {
    "$store.state.data"() {
      console.dir("watch...");
      console.dir(this.$store.state);
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
    }
  },
  created: function() {
    this.$store.commit("error","请先保存表单"); 
  },
  mounted: function() {
    this.$API.F1();this.$API.F2();

    for (var i = 0; i < 10; i++) {
      this.rule.push({
        type: "DatePicker",
        field: "start" + i,
        title: this.$t("demo.start"),
        value: new Date(),
        props: {
          type: "date",
          format: "yyyy-MM-dd",
          placeholder: "请选择起始时间"
        }
      });
    }
  }
};
</script>

<style scoped>
</style>

<template>
<a v-on:click="showSub">
	<slot></slot>
</a>
</template>

<script>
import Vue from 'vue';

export default {
  	props: ['value',"dialogId"],
  	data :function () {
	    return {
	    }
	},
 	mounted : function(){
 		
 	},
	methods: {
	    showSub : function(){
	    	var listName = this.dialogId.split("-")[1]+"List";
	    	var that = this;
	    	
	    	Vue.set(this.$parent.$data.subTempData,listName,Vue.tools.CloneUtil.list(this.value[listName]||[]));
			var conf = {
				height : 600,
				width : 800,
				title : $(this.$el).text(),
				btn : true,
				type : "1",
				content : $('#' + this.dialogId)
			};
			conf.ok = function(index, innerWindow) {
				Vue.set(that.value,listName,that.$parent.$data.subTempData[listName]);
				layer.close(index);
			};
			$.Dialog.open(conf);
	    }
  	}
}
</script>

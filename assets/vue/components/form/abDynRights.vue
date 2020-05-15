<template> </template>

<script>
import Vue from 'vue'

export default {
  	props: ["value","permission","tablePermission"],
  	data :function () {
	    return {
	    	dynRights : null,
	    	sourcePerimission : null,
	    	sourceTablePermission : null,
	    }
	},
  	created : function(){
  		this.sourcePerimission = Vue.tools.CloneUtil.deep(this.permission);
  		this.sourceTablePermission = Vue.tools.CloneUtil.deep(this.tablePermission);
  		if(this.$slots.default[0].text){
  			this.dynRights = JSON.parse(this.$slots.default[0].text);
  		}
  		this.handle();
 	},
 	mounted : function(){
 	},
	methods: {
		//处理权限
	    handle : function(){
	    	if(!this.dynRights){
	    		return;
	    	}
	    	for(let key in this.value){
	    		window.eval("var " + key);
		    	eval(key + " = this.value." + key + ";");
	    	}
    	 	this.dynRights.forEach(item => {
    	 		let func;
    	 		eval("func = function() { " + item.script + " };");
    	 		let permission = this.sourcePerimission;
    	 		let rSort = ["n","r","w","b"];//权限排序
    	 		item.permissions.split(",").forEach(ite => {
    	 			let p;
        	 		eval("p = " + ite + ";");//源权限
        	 		if(rSort.indexOf(p) < rSort.indexOf(item.rights)){//权限不能越界修改
        	 			return;
        	 		}
        	 		if(func()){//满足条件修改
        	 			eval("this." + ite + " = '" + item.rights + "';");
        	 		}
        	 		this.$emit('update:permission',this.permission);
    	 		});
	    	});
	    },
	    //重新计算table权限
	    calTablePermission : function(){
	    	for(let key in this.tablePermission){
	    		let rSort = ["b","w","r","n"];//权限排序
	    		let p;
	    		//从高权限到低权限，如果字段有
	    		rSort.forEach(item => {
	    			if(p){
	    				return;
	    			}
	    			for(let k in this.permission[key]){
	    				let v = this.permission[key][k];
	    				if(v == item){
	    					p = item;
	    				}
	    			}
	    		});
	    		eval("this.tablePermission[key] = p;");
	    		this.$emit('update:tablePermission',this.tablePermission);
	    	}
	    }
  	},
 	watch : {
 		value : {
 			handler : function(newVal,oldVal){
 	 			this.handle();
 			},
 			deep:true
 		}
 	}
}
</script>

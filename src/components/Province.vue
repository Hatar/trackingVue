<template>
    <input 
        type="text" 
        class="form-control w-25 my-3" 
        autocomplete="off" 
        spellcheck="false" 
        v-model="filter"  
        placeholder="Search..."
    />
    <table id="tb_province" class="table table-bordered table-hover">
        <thead>
            <tr>
                <th>Province</th>
                <th>Total Doses*</th>
                <th>per 100 people</th>
                <th>Reported Doses</th>
                <th>Cur.Daily Doses</th>
                <th>Vaccinated</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="prov in provinces" :key="prov.id" v-show="filtered(prov)">
                <td class="text-danger">{{ prov.province }}</td>
                <td>{{ prov.total_doses }}</td>
                <td>{{ prov.per_people }}</td>
                <td>{{ prov.Reported }}</td>
                <td>{{ prov.doses }}</td>
                <td>{{ prov.Vaccinated }}</td>
            </tr>
        </tbody>
    </table>
</template>
<script>
export default {
    props:['provinces'],
    data(){
        return {
            filter: ''
        }
    },
    methods: {
        filtered(item) {
			let show = true;
			
			if(this.filter.length) {
				
				show = false;
				
				let filterKeyword = this.filter.toLowerCase();
				
				Object.keys(item).map(function(key) {
					if(typeof item[key] === 'string') {
						let value = item[key].toString().toLowerCase();
						
						if(value.includes(filterKeyword)) {
							show = true;
						}
					}
				});
			}
			
			return show;
        }
    }
}
</script>
<style lang="">
    
</style>
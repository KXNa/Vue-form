<template>
  <div class="container">
        <div class="checkbox">
            <el-checkbox :indeterminate="isIndeterminate" v-model="checkAll" @change="handleCheckAllChange">全选</el-checkbox>
            <div style="margin: 15px 0;"></div>
            <el-checkbox-group v-model="checkedCities1" @change="handleCheckedCitiesChange">
                <el-checkbox v-for="city in cities" :label="city" :key="city">{{city}}</el-checkbox>
            </el-checkbox-group>
            
        </div>
        <div class="checkboxnum">
            <el-checkbox-group 
                v-model="checkedCities2"
                :min="1"
                :max="2">
                <el-checkbox v-for="city in cities" :label="city" :key="city">{{city}}</el-checkbox>
            </el-checkbox-group>
        </div>
        <el-button type="success" icon="el-icon-check" circle @click.native="checkVal"></el-button>
        <div class="Transfer">
            <el-transfer
             filterable
             :filter-method="filterMethod"
             filter-placeholder="请输入城市拼音"
             v-model="value" :data="data"></el-transfer>
        </div>
  </div>
</template>
<script>
  const cityOptions = ['上海', '北京', '广州', '深圳'];
  export default {
    data() {
        
        const generateData = _ => {
            console.log(_)
        const data = [];
        const cities = ['上海', '北京', '广州', '深圳', '南京', '西安', '成都'];
        const pinyin = ['shanghai', 'beijing', 'guangzhou', 'shenzhen', 'nanjing', 'xian', 'chengdu'];
        cities.forEach((city, index) => {
          data.push({
            label: city,
            key: index,
            pinyin: pinyin[index]
          });
        });
        return data;
      };
      return {
        data: generateData(),
        value: [],
        filterMethod(query, item) {
          return item.pinyin.indexOf(query) > -1;
        },
        checkAll: false,
        checkedCities1: ['上海', '北京'],
        checkedCities2: ['上海', '北京'],
        cities: cityOptions,
        isIndeterminate: true
      };
    },
    methods: {
      handleCheckAllChange(val) {
        this.checkedCities = val ? cityOptions : [];
        this.isIndeterminate = false;
      },
      handleCheckedCitiesChange(value) {
        let checkedCount = value.length;
        this.checkAll = checkedCount === this.cities.length;
        this.isIndeterminate = checkedCount > 0 && checkedCount < this.cities.length;
      },
      checkVal() {
          console.log(this.checkedCities1, this.checkedCities2)
      }
    }
  };
</script>
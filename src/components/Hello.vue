<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <el-col :span="24" class="toolbar">
      <el-form :inline="true">
        <el-form-item>
          <el-input placeholder="请输入城市名称" v-model="input2"></el-input>
        </el-form-item>
        <el-form-item>
          <el-button v-on:click="greet">查询</el-button>
        </el-form-item>
      </el-form>
    </el-col>
    <el-col :span="24" v-if="show">
      <el-button type="primary">{{city}}</el-button>
            <el-button type="primary">{{country}}</el-button>

    </el-col>
    <el-col :span="24" v-if="show">
      <el-table
            :data="gridData"
            style="width: 100%">
            <el-table-column
              prop="date"
              label="日期"
              width="180">
            </el-table-column>
            <el-table-column
              prop="week"
              label="天">
            </el-table-column>
            <el-table-column
              prop="wea"
              label="天气情况"
              width="180">
            </el-table-column>
            <el-table-column
              prop="tem1"
              label="高温">
            </el-table-column>
            <el-table-column
              prop="tem2"
              label="低温"
              width="180">
            </el-table-column>
            <el-table-column
              prop="win_speed"
              label="风级"
              width="180">
            </el-table-column>

          </el-table>
    </el-col>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'A Simple VUE Weather Demo',
      input2:null,
      show:false,
      gridData:[],
      city:null,
      country:null
    }
  },
  methods: {
      greet: function() {
						this.$http.get(`https://www.tianqiapi.com/api/?city=${this.input2}&version=v1&appid=23722394&appsecret=AwCo2EYl`)

							.then((response) => {
                // console.log(response);
                this.city=response.data.city;
                this.country=response.data.country;
               this.gridData=response.data.data
               console.log(this.gridData);


               this.show = true
							})
							.catch(function(response) {
								console.log(response)
							})
					}
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bounce-enter-active {
  animation:bounce-in .5s;
}
.bounce-leave-active{
  animation:bounce-out .5s;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.05);
  }
  100% {
    transform: scale(1);
  }
}
@keyframes bounce-out {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(0.95);
  }
  100% {
    transform: scale(0);
  }
}
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
.el-table{
  margin:5% 10%;
}
.el-row {
    margin-bottom: 20px;

  }
  .el-row:last-child {
      margin-bottom: 0;
    }
  .el-col {
    border-radius: 4px;
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-purple {
    background: #d3dce6;
  }
  .bg-purple-light {
    background: #e5e9f2;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }
</style>

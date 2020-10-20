<template>
  <div>
  <el-container>
    <el-header>
      <div>
        <el-row :gutter="20">
          <el-col :span="6"><div>
            <template>
              <div class="block">
                <span  class="demonstration">反馈日期</span>
                <el-date-picker
                  size="mini"
                  v-model="value1"
                  type="date"
                  placeholder="选择日期">
                </el-date-picker>
              </div>
            </template>

          </div></el-col>
          <el-col :span="6"><div>
            <template>
              <div class="block">
                <span class="demonstration">至</span>
                <el-date-picker
                  v-model="value2"
                  size="mini"
                  type="date"
                  placeholder="选择日期">
                </el-date-picker>
              </div>
            </template>
          </div></el-col>
          <el-col :span="6"><div>
            <template>
              <div class="block">
                <span class="demonstration">到货日期</span>
                <el-date-picker
                  v-model="value3"
                  size="mini"
                  type="date"
                  placeholder="选择日期">
                </el-date-picker>
              </div>
            </template>
          </div></el-col>
          <el-col :span="6"><div>
            <template>
              <div class="block">
                <span class="demonstration">至</span>
                <el-date-picker
                  v-model="value4"
                  size="mini"
                  type="date"
                  placeholder="选择日期">
                </el-date-picker>
              </div>
            </template>
          </div></el-col>
        </el-row>
      </div>

      <br>
      <div>
        <el-row :gutter="20">

          <el-col :span="6"><div>
            <template>
              <span>异常类型</span>
              <el-select size="mini" v-model="errorType" placeholder="请选择">
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value">
                </el-option>
              </el-select>
            </template>
          </div></el-col>

          <el-col :span="6"><div>
            <template>
              <span>处理部门</span>
              <el-select size="mini" v-model="isTest" placeholder="请选择">
                <el-option
                  v-for="item in options"
                  :key="item.value"
                  :label="item.label"
                  :value="item.value">
                </el-option>
              </el-select>
            </template>
          </div></el-col>
          <el-col :span="6"><div>
            <span>物料编码</span>
            <el-input size="mini" style="width: 230px" v-model="materialCode" placeholder="请输入物料编码"></el-input>
          </div></el-col>
          <el-col :span="6"><div>
            <span>物料名称</span>
            <el-input size="mini" style="width: 230px" v-model="materialName" placeholder="请输入物料名称"></el-input>
          </div></el-col>
        </el-row>
      </div>
      <br>
      <div>
        <el-row>
          <el-col :span="18"><div>
            &nbsp;
          </div></el-col>
          <el-col :span="2"><div>
            <el-button type="primary" size="mini" >查询</el-button>
          </div></el-col>
          <el-col :span="2"><div>
            <el-button type="primary" size="mini" @click="dialogVisible = true">新增异常</el-button>
          </div></el-col>
          <el-col :span="2"><div>
            <el-button type="primary" size="mini" >导出表格</el-button>
          </div></el-col>
        </el-row>
      </div>
    </el-header>
    <br><br><br>

    <el-main>
      <template>
        <el-table
          :data="tableData"
          border
          style="width: 100%">
          <el-table-column
            prop="date"
            label="反馈日期">
          </el-table-column>
          <el-table-column
            prop="name"
            label="操作">
            <template slot-scope="scope">
              <el-button @click="handleClick(scope.row)" type="text" size="small">查看</el-button>
            </template>
          </el-table-column>
          <el-table-column
            prop="fenchang"
            label="分厂">
          </el-table-column>

          <el-table-column
            prop="custom"
            label="客户名">
          </el-table-column>

          <el-table-column
            prop="ldcode"
            label="凌达代码">
          </el-table-column>

          <el-table-column
            prop="xh"
            label="压缩机型号">
          </el-table-column>

          <el-table-column
            prop="type"
            label="类别">
          </el-table-column>

          <el-table-column
            prop="bzyq"
            label="包装要求">
          </el-table-column>
          <el-table-column
            prop="account"
            label="发货数量">
          </el-table-column>

          <el-table-column
            prop="yctype"
            label="异常类型">
          </el-table-column>

          <el-table-column
            prop="ms"
            label="描述">
          </el-table-column>

          <el-table-column
            prop="isTest"
            label="性能是否测试">
          </el-table-column>

          <el-table-column
            prop="clbm"
            label="处理部门">
          </el-table-column>

          <el-table-column
            prop="cljd"
            label="处理进度">
          </el-table-column>

          <el-table-column
            prop="dclbm"
            label="转为待处理部门">
          </el-table-column>

          <el-table-column
            prop="gjr"
            label="跟进人">
          </el-table-column>

          <el-table-column
            prop="bz"
            label="备注">
          </el-table-column>
        </el-table>
      </template>
    </el-main>
  </el-container>

  <el-dialog
    :visible.sync="dialogVisible">

    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px">

      <el-form-item required>
        <el-col :span="10">
          <el-form-item label="凌达代码" prop="code">
            <el-select size="mini" v-model="ldcode1" placeholder="请选择">
              <el-option
                v-for="item in ruleForm.LDoptions"
                :key="item.value"
                :label="item.label"
                :value="item.value">
              </el-option>
            </el-select>
          </el-form-item>
        </el-col>

        <el-col :span="12">
          <el-form-item label="客户名称" prop="custom1">
            <el-input v-model="ruleForm.customType1"  size="mini" placeholder="请输入内容"></el-input>
          </el-form-item>

        </el-col>
      </el-form-item>


      <el-form-item required>
        <el-col :span="10">
            <el-form-item label="压缩机型号" prop="custom1">
              <el-input v-model="ruleForm.xh" size="mini"  placeholder="请输入内容"></el-input>
            </el-form-item>
        </el-col>
        <el-col :span="12">
          <el-form-item label="包装类型" prop="custom1">
            <el-input v-model="ruleForm.bzlx1" size="mini"  placeholder="请输入内容"></el-input>
          </el-form-item>
        </el-col>
      </el-form-item>

      <el-form-item label="异常类型" prop="code" >
        <el-select v-model="ruleForm.errorValue" placeholder="请选择">
          <el-option
            v-for="item in ruleForm.errorOptions"
            :key="item.value"
            :label="item.label"
            :value="item.value">
          </el-option>
        </el-select>
      </el-form-item>

      <el-form-item  label="处理部门" prop="dept">
        <el-col :span="7">
          <el-form-item>
            <el-checkbox v-model="ruleForm.zhikong">质控部</el-checkbox>
          </el-form-item>
        </el-col>

        <el-col :span="7">
          <el-form-item>
            <el-checkbox v-model="ruleForm.zzhuang">总装分厂</el-checkbox>
          </el-form-item>
        </el-col>

        <el-col :span="7">
          <el-form-item>
            <el-checkbox v-model="ruleForm.shengchan">生产计划部</el-checkbox>
          </el-form-item>
        </el-col>
      </el-form-item>

      <el-button type="primary" @click="submitClick('ruleForm')">提交</el-button>
    </el-form>
  </el-dialog>
<!--    =============================-->
    <el-dialog :visible.sync="dialogVisible1">
      <el-form :model="ruleForm1" :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">

        <el-form-item required>
          <el-col :span="10">
            <el-form-item label="凌达代码" prop="custom1">
              <el-input value="atpx-4869" size="mini"  placeholder="请输入内容"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="压缩机型号" prop="custom1">
              <el-input value="dji-f" size="mini"  placeholder="请输入内容"></el-input>
            </el-form-item>
          </el-col>
        </el-form-item>

        <el-form-item required>
          <el-col :span="10">
            <el-form-item label="包装要求" prop="custom1">
              <el-input value="散件" size="mini"  placeholder="请输入内容"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="12">
            <el-form-item label="发货数量" prop="custom1">
              <el-input value="100" size="mini"  placeholder="请输入内容"></el-input>
            </el-form-item>
          </el-col>
        </el-form-item>

        <el-form-item required>
          <el-col :span="11">
            <el-form-item label="异常类型" prop="custom1">
              <el-input value="质量异常" size="mini"  placeholder="请输入内容"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="13">
            <el-form-item label="当前处部门" prop="custom1">
              <el-input value="质控部" size="mini"  placeholder="请输入内容"></el-input>
            </el-form-item>
          </el-col>
        </el-form-item>

<!--        ---------------------------------------->
        <span style="font-size: 20px;color: red">质控部</span><br>
        <el-form-item required>
          <el-col :span="11">
            <el-form-item label="处理结果" prop="custom1">
              <el-input v-model="cljg1" size="mini"  placeholder="请输入内容"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="13">
            <el-form-item label="备注" >
              <el-input v-model="bz1" size="mini"  placeholder="请输入内容"></el-input>
            </el-form-item>
          </el-col>
        </el-form-item>

        <el-form-item label="是否完异常" prop="code" >
          <el-select v-model="ruleForm1.sfyc" placeholder="请选择">
            <el-option
              v-for="item in ruleForm1.sfycOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
        </el-form-item>

        <el-form-item  label="处理部门" prop="dept">
          <el-col :span="7">
            <el-form-item>
              <el-checkbox v-model="ruleForm.zhikong">质控部</el-checkbox>
            </el-form-item>
          </el-col>

          <el-col :span="7">
            <el-form-item>
              <el-checkbox v-model="ruleForm.zzhuang">总装分厂</el-checkbox>
            </el-form-item>
          </el-col>

          <el-col :span="7">
            <el-form-item>
              <el-checkbox v-model="ruleForm.shengchan">生产计划部</el-checkbox>
            </el-form-item>
          </el-col>
        </el-form-item>

<!--       -------------------------- -->

        <span style="font-size: 20px;color: red">生产计划部</span><br>
        <el-form-item required>
          <el-col :span="11">
            <el-form-item label="处理结果" prop="custom1">
              <el-input v-model="cljg1" size="mini"  placeholder="请输入内容"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="13">
            <el-form-item label="备注" >
              <el-input v-model="bz1" size="mini"  placeholder="请输入内容"></el-input>
            </el-form-item>
          </el-col>
        </el-form-item>

        <el-form-item label="是否完异常" prop="code" >
          <el-select v-model="ruleForm1.sfyc" placeholder="请选择">
            <el-option
              v-for="item in ruleForm1.sfycOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
        </el-form-item>

        <el-form-item  label="处理部门" prop="dept">
          <el-col :span="7">
            <el-form-item>
              <el-checkbox v-model="ruleForm.zhikong">质控部</el-checkbox>
            </el-form-item>
          </el-col>

          <el-col :span="7">
            <el-form-item>
              <el-checkbox v-model="ruleForm.zzhuang">总装分厂</el-checkbox>
            </el-form-item>
          </el-col>

          <el-col :span="7">
            <el-form-item>
              <el-checkbox v-model="ruleForm.shengchan">生产计划部</el-checkbox>
            </el-form-item>
          </el-col>
        </el-form-item>

<!--       ------------------- -->

        <span style="font-size: 20px;color: red">总转分厂</span><br>
        <el-form-item required>
          <el-col :span="11">
            <el-form-item label="处理结果" prop="custom1">
              <el-input v-model="cljg1" size="mini"  placeholder="请输入内容"></el-input>
            </el-form-item>
          </el-col>
          <el-col :span="13">
            <el-form-item label="备注" >
              <el-input v-model="bz1" size="mini"  placeholder="请输入内容"></el-input>
            </el-form-item>
          </el-col>
        </el-form-item>

        <el-form-item label="是否完异常" prop="code" >
          <el-select v-model="ruleForm1.sfyc" placeholder="请选择">
            <el-option
              v-for="item in ruleForm1.sfycOptions"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
        </el-form-item>

        <el-form-item  label="处理部门" prop="dept">
          <el-col :span="7">
            <el-form-item>
              <el-checkbox v-model="ruleForm.zhikong">质控部</el-checkbox>
            </el-form-item>
          </el-col>

          <el-col :span="7">
            <el-form-item>
              <el-checkbox v-model="ruleForm.zzhuang">总装分厂</el-checkbox>
            </el-form-item>
          </el-col>

          <el-col :span="7">
            <el-form-item>
              <el-checkbox v-model="ruleForm.shengchan">生产计划部</el-checkbox>
            </el-form-item>
          </el-col>
        </el-form-item>

        <el-button type="primary" @click="submitClick1('ruleForm1')">提交</el-button>
      </el-form>
    </el-dialog>

</div>
</template>

<script>
    export default {
        name: "index",
      data(){
          return {

            ruleForm1:{
              sfyc:'',
              sfycOptions:[
                {
                  value:'是',
                  label:'是'
                },
                {
                  value:'否',
                  label:'否'
                }
              ]
            },

            cljg1:'',
            bz1:'',
            dialogVisible1:false,
            ldcode1:'',

            ruleForm: {
              xh:'',
              bzlx1:'',
              customType1:'',
              zhikong:'',
              zzhuang:'',
              shengchan:'',
              ldcode1:'',
              LDoptions:[
                {
                  value:'asd-12',
                  label:'asd-12'
                },
                {
                  value:'qwe-78',
                  label:'qwe-78'
                }
              ],
              errorValue:'',
              errorOptions:[
                {
                  value:'包装异常',
                  label:'包装异常'
                },
                {
                  value: '库存异常',
                  label: '库存异常'
                }
              ],
            },

            rules:{
              code:[{required: true, message: '请选择凌达代码', trigger: 'blur'}],
              custom1:[{required: true, message: '请完善输入数据', trigger: 'blur'}],
              dept:[{ required: true, message: '请选择处理部门：单选或多选', trigger: 'change' }]
            },


            dialogVisible:false,
            pickerOptions: {
              disabledDate(time) {
                return time.getTime() > Date.now();
              },
              shortcuts: [{
                text: '今天',
                onClick(picker) {
                  picker.$emit('pick', new Date());
                }
              }, {
                text: '昨天',
                onClick(picker) {
                  const date = new Date();
                  date.setTime(date.getTime() - 3600 * 1000 * 24);
                  picker.$emit('pick', date);
                }
              }, {
                text: '一周前',
                onClick(picker) {
                  const date = new Date();
                  date.setTime(date.getTime() - 3600 * 1000 * 24 * 7);
                  picker.$emit('pick', date);
                }
              }]
            },
            value1: '',
            value2: '',
            value3:'',
            value4:'',
            isTest:'',
            materialCode:'',
            materialName:'',
            customType:'',

            errorType:'',
            options: [{
              value: '选项1',
              label: '黄金糕'
            }, {
              value: '选项2',
              label: '双皮奶'
            }, {
              value: '选项3',
              label: '蚵仔煎'
            }, {
              value: '选项4',
              label: '龙须面'
            }, {
              value: '选项5',
              label: '北京烤鸭'
            }],
            tableData:[
              {
                date:'2020-10-15',
                fenchang:'珠海凌达',
                custom:'海尔',
                ldcode:'ld-10086',
                xh:'ac-45,',
                type:'测试',
                bzyq:'无',
                account:'10010',
                yclx:'质量异常',
                ms:'',
                isTest:'是',
                clbm:'质控部',
                cljd:'',
                clyj:'',
                dclbm:'总装分厂',
                gjr:'张三',
                bz:''
              },
              {
                date:'2020-10-15',
                fenchang:'珠海凌达',
                custom:'海尔',
                ldcode:'ld-10086',
                xh:'ac-45,',
                type:'测试',
                bzyq:'无',
                account:'10010',
                yclx:'质量异常',
                ms:'',
                isTest:'是',
                clbm:'质控部',
                cljd:'',
                clyj:'',
                dclbm:'总装分厂',
                gjr:'张三',
                bz:''
              },
              {
                date:'2020-10-15',
                fenchang:'珠海凌达',
                custom:'海尔',
                ldcode:'ld-10086',
                xh:'ac-45,',
                type:'测试',
                bzyq:'无',
                account:'10010',
                yclx:'质量异常',
                ms:'',
                isTest:'是',
                clbm:'质控部',
                cljd:'',
                clyj:'',
                dclbm:'总装分厂',
                gjr:'张三',
                bz:''
              },
              {
                date:'2020-10-15',
                fenchang:'珠海凌达',
                custom:'海尔',
                ldcode:'ld-10086',
                xh:'ac-45,',
                type:'测试',
                bzyq:'无',
                account:'10010',
                yclx:'质量异常',
                ms:'',
                isTest:'是',
                clbm:'质控部',
                cljd:'',
                clyj:'',
                dclbm:'总装分厂',
                gjr:'张三',
                bz:''
              },
            ],
          }
      },

      watch: {
        ldcode1(val,oldValue){
          if(val=='asd-12'){
            this.ruleForm.bzlx1='散件',
            this.ruleForm.customType1="珠海格力"
            this.ruleForm.xh='udh-11'
          }
          if(val=='qwe-78'){
            this.ruleForm.bzlx1='整包',
              this.ruleForm.customType1="汉芯国际"
            this.ruleForm.xh='Qualcomm-865'
          }
        }
      },

      methods: {
        submitClick(formName){
          this.$refs[formName].validate((valid) => {
            if (valid) {
              this.dialogVisible=false;
              this.$message({
                message:'新增异常成功',
                type:'success'
              })
            } else {
              console.log('error submit!!');
              return false;
            }
          });
        },
        submitClick1(formName){
          this.$refs[formName].validate((valid) => {
            if (valid) {
              this.dialogVisible=false;
              this.$message({
                message:'异常处理成功',
                type:'success'
              })
            } else {
              console.log('error submit!!');
              return false;
            }
          });
        },

        handleClick(row){
         this.dialogVisible1=true
        }
      }
    }
</script>

<style scoped>

  .el-header {
    padding: 0;
  }
</style>

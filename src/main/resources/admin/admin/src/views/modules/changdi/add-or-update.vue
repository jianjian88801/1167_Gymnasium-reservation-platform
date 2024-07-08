







<template>
    <div class="addEdit-block">
        <el-form
                class="detail-form-content"
                ref="ruleForm"
                :model="ruleForm"
                :rules="rules"
                label-width="80px"
                :style="{backgroundColor:addEditForm.addEditBoxColor}">
            <el-row>
                <input id="updateId" name="id" type="hidden">
               <el-col :span="12">
                   <el-form-item class="input" v-if="type!='info'"  label="场地编号" prop="changdiUuidNumber">
                       <el-input v-model="ruleForm.changdiUuidNumber"
                                 placeholder="场地编号" clearable  :readonly="ro.changdiUuidNumber"></el-input>
                   </el-form-item>
                   <div v-else>
                       <el-form-item class="input" label="场地编号" prop="changdiUuidNumber">
                           <el-input v-model="ruleForm.changdiUuidNumber"
                                     placeholder="场地编号" readonly></el-input>
                       </el-form-item>
                   </div>
               </el-col>
               <el-col :span="12">
                   <el-form-item class="input" v-if="type!='info'"  label="场地名称" prop="changdiName">
                       <el-input v-model="ruleForm.changdiName"
                                 placeholder="场地名称" clearable  :readonly="ro.changdiName"></el-input>
                   </el-form-item>
                   <div v-else>
                       <el-form-item class="input" label="场地名称" prop="changdiName">
                           <el-input v-model="ruleForm.changdiName"
                                     placeholder="场地名称" readonly></el-input>
                       </el-form-item>
                   </div>
               </el-col>
                <el-col :span="24">
                    <el-form-item class="upload" v-if="type!='info' && !ro.changdiPhoto" label="场地照片" prop="changdiPhoto">
                        <file-upload
                            tip="点击上传场地照片"
                            action="file/upload"
                            :limit="3"
                            :multiple="true"
                            :fileUrls="ruleForm.changdiPhoto?ruleForm.changdiPhoto:''"
                            @change="changdiPhotoUploadChange"
                        ></file-upload>
                    </el-form-item>
                    <div v-else>
                        <el-form-item v-if="ruleForm.changdiPhoto" label="场地照片" prop="changdiPhoto">
                            <img style="margin-right:20px;" v-bind:key="index" v-for="(item,index) in (ruleForm.changdiPhoto || '').split(',')" :src="item" width="100" height="100">
                        </el-form-item>
                    </div>
                </el-col>
                <el-col :span="12">
                    <el-form-item class="select" v-if="type!='info'"  label="场地类型" prop="changdiTypes">
                        <el-select v-model="ruleForm.changdiTypes" placeholder="请选择场地类型">
                            <el-option
                                v-for="(item,index) in changdiTypesOptions"
                                v-bind:key="item.codeIndex"
                                :label="item.indexName"
                                :value="item.codeIndex">
                            </el-option>
                        </el-select>
                    </el-form-item>
                    <div v-else>
                        <el-form-item class="input" label="场地类型" prop="changdiValue">
                        <el-input v-model="ruleForm.changdiValue"
                            placeholder="场地类型" readonly></el-input>
                        </el-form-item>
                    </div>
                </el-col>
               <el-col :span="12">
                   <el-form-item class="input" v-if="type!='info'"  label="场地原价" prop="changdiOldMoney">
                       <el-input v-model="ruleForm.changdiOldMoney"
                                 placeholder="场地原价" clearable  :readonly="ro.changdiOldMoney"></el-input>
                   </el-form-item>
                   <div v-else>
                       <el-form-item class="input" label="场地原价" prop="changdiOldMoney">
                           <el-input v-model="ruleForm.changdiOldMoney"
                                     placeholder="场地原价" readonly></el-input>
                       </el-form-item>
                   </div>
               </el-col>
               <el-col :span="12">
                   <el-form-item class="input" v-if="type!='info'"  label="场地现价" prop="changdiNewMoney">
                       <el-input v-model="ruleForm.changdiNewMoney"
                                 placeholder="场地现价" clearable  :readonly="ro.changdiNewMoney"></el-input>
                   </el-form-item>
                   <div v-else>
                       <el-form-item class="input" label="场地现价" prop="changdiNewMoney">
                           <el-input v-model="ruleForm.changdiNewMoney"
                                     placeholder="场地现价" readonly></el-input>
                       </el-form-item>
                   </div>
               </el-col>
               <el-col :span="12">
                   <el-form-item class="input" v-if="type!='info'"  label="时间段" prop="shijianduan">
                       <el-input v-model="ruleForm.shijianduan"
                                 placeholder="时间段" clearable  :readonly="ro.shijianduan"></el-input>
                   </el-form-item>
                   <div v-else>
                       <el-form-item class="input" label="时间段" prop="shijianduan">
                           <el-input v-model="ruleForm.shijianduan"
                                     placeholder="时间段" readonly></el-input>
                       </el-form-item>
                   </div>
               </el-col>
               <!--<el-col :span="12">
                   <el-form-item class="input" v-if="type!='info'"  label="人数" prop="shijianduanRen">
                       <el-input v-model="ruleForm.shijianduanRen"
                                 placeholder="人数" clearable  :readonly="ro.shijianduanRen"></el-input>
                   </el-form-item>
                   <div v-else>
                       <el-form-item class="input" label="人数" prop="shijianduanRen">
                           <el-input v-model="ruleForm.shijianduanRen"
                                     placeholder="人数" readonly></el-input>
                       </el-form-item>
                   </div>
               </el-col>-->
                <el-col :span="12">
                    <el-form-item class="select" v-if="type!='info'"  label="半全场" prop="banquanTypes">
                        <el-select v-model="ruleForm.banquanTypes" placeholder="请选择半全场">
                            <el-option
                                v-for="(item,index) in banquanTypesOptions"
                                v-bind:key="item.codeIndex"
                                :label="item.indexName"
                                :value="item.codeIndex">
                            </el-option>
                        </el-select>
                    </el-form-item>
                    <div v-else>
                        <el-form-item class="input" label="半全场" prop="banquanValue">
                        <el-input v-model="ruleForm.banquanValue"
                            placeholder="半全场" readonly></el-input>
                        </el-form-item>
                    </div>
                </el-col>
               <el-col :span="12">
                   <el-form-item class="input" v-if="type!='info'"  label="推荐吃饭地点" prop="tuijian">
                       <el-input v-model="ruleForm.tuijian"
                                 placeholder="推荐吃饭地点" clearable  :readonly="ro.tuijian"></el-input>
                   </el-form-item>
                   <div v-else>
                       <el-form-item class="input" label="推荐吃饭地点" prop="tuijian">
                           <el-input v-model="ruleForm.tuijian"
                                     placeholder="推荐吃饭地点" readonly></el-input>
                       </el-form-item>
                   </div>
               </el-col>
                <el-col :span="24">
                    <el-form-item v-if="type!='info'"  label="场地简介" prop="changdiContent">
                        <editor style="min-width: 200px; max-width: 600px;"
                                v-model="ruleForm.changdiContent"
                                class="editor"
                                action="file/upload">
                        </editor>
                    </el-form-item>
                    <div v-else>
                        <el-form-item v-if="ruleForm.changdiContent" label="场地简介" prop="changdiContent">
                            <span v-html="ruleForm.changdiContent"></span>
                        </el-form-item>
                    </div>
                </el-col>
            </el-row>
            <el-form-item class="btn">
                <el-button v-if="type!='info'" type="primary" class="btn-success" @click="onSubmit">提交</el-button>
                <el-button v-if="type!='info'" class="btn-close" @click="back()">取消</el-button>
                <el-button v-if="type=='info'" class="btn-close" @click="back()">返回</el-button>
            </el-form-item>
        </el-form>
    </div>
</template>
<script>
    import styleJs from "../../../utils/style.js";
    // 数字，邮件，手机，url，身份证校验
    import { isNumber,isIntNumer,isEmail,isPhone, isMobile,isURL,checkIdCard } from "@/utils/validate";
    export default {
        data() {
            return {
                addEditForm:null,
                id: '',
                type: '',
                sessionTable : "",//登录账户所在表名
                role : "",//权限
                ro:{
                    changdiUuidNumber: false,
                    changdiName: false,
                    changdiPhoto: false,
                    changdiTypes: false,
                    changdiOldMoney: false,
                    changdiNewMoney: false,
                    shijianduan: false,
                    shijianduanRen: false,
                    changdiClicknum: false,
                    banquanTypes: false,
                    shangxiaTypes: false,
                    tuijian: false,
                    changdiDelete: false,
                    changdiContent: false,
                },
                ruleForm: {
                    changdiUuidNumber: new Date().getTime(),
                    changdiName: '',
                    changdiPhoto: '',
                    changdiTypes: '',
                    changdiOldMoney: '',
                    changdiNewMoney: '',
                    shijianduan: '8-10,10-12,14-16,16-18',
                    shijianduanRen: '',
                    changdiClicknum: '',
                    banquanTypes: '',
                    shangxiaTypes: '',
                    tuijian: '',
                    changdiDelete: '',
                    changdiContent: '',
                },
                changdiTypesOptions : [],
                banquanTypesOptions : [],
                shangxiaTypesOptions : [],
                rules: {
                   changdiUuidNumber: [
                              { required: true, message: '场地编号不能为空', trigger: 'blur' },
                          ],
                   changdiName: [
                              { required: true, message: '场地名称不能为空', trigger: 'blur' },
                          ],
                   changdiPhoto: [
                              { required: true, message: '场地照片不能为空', trigger: 'blur' },
                          ],
                   changdiTypes: [
                              { required: true, message: '场地类型不能为空', trigger: 'blur' },
                              {  pattern: /^[1-9][0-9]*$/,
                                  message: '只允许输入整数',
                                  trigger: 'blur'
                              }
                          ],
                   changdiOldMoney: [
                              { required: true, message: '场地原价不能为空', trigger: 'blur' },
                              {  pattern: /^[0-9]{0,6}(\.[0-9]{1,2})?$/,
                                  message: '只允许输入整数6位,小数2位的数字',
                                  trigger: 'blur'
                              }
                          ],
                   changdiNewMoney: [
                              { required: true, message: '场地现价不能为空', trigger: 'blur' },
                              {  pattern: /^[0-9]{0,6}(\.[0-9]{1,2})?$/,
                                  message: '只允许输入整数6位,小数2位的数字',
                                  trigger: 'blur'
                              }
                          ],
                   shijianduan: [
                              { required: true, message: '时间段不能为空', trigger: 'blur' },
                          ],
                   shijianduanRen: [
                              { required: true, message: '人数不能为空', trigger: 'blur' },
                              {  pattern: /^[1-9][0-9]*$/,
                                  message: '只允许输入整数',
                                  trigger: 'blur'
                              }
                          ],
                   changdiClicknum: [
                              { required: true, message: '点击次数不能为空', trigger: 'blur' },
                              {  pattern: /^[1-9][0-9]*$/,
                                  message: '只允许输入整数',
                                  trigger: 'blur'
                              }
                          ],
                   banquanTypes: [
                              { required: true, message: '半全场不能为空', trigger: 'blur' },
                              {  pattern: /^[1-9][0-9]*$/,
                                  message: '只允许输入整数',
                                  trigger: 'blur'
                              }
                          ],
                   shangxiaTypes: [
                              { required: true, message: '是否上架不能为空', trigger: 'blur' },
                              {  pattern: /^[1-9][0-9]*$/,
                                  message: '只允许输入整数',
                                  trigger: 'blur'
                              }
                          ],
                   tuijian: [
                              { required: true, message: '推荐吃饭地点不能为空', trigger: 'blur' },
                          ],
                   changdiDelete: [
                              { required: true, message: '逻辑删除不能为空', trigger: 'blur' },
                              {  pattern: /^[1-9][0-9]*$/,
                                  message: '只允许输入整数',
                                  trigger: 'blur'
                              }
                          ],
                   changdiContent: [
                              { required: true, message: '场地简介不能为空', trigger: 'blur' },
                          ],
                }
            };
        },
        props: ["parent"],
        computed: {
        },
        created() {
            //获取当前登录用户的信息
            this.sessionTable = this.$storage.get("sessionTable");
            this.role = this.$storage.get("role");

            if (this.role != "管理员"){
                this.ro.changdiOldMoney = true;
                this.ro.changdiNewMoney = true;
            }
            this.addEditForm = styleJs.addStyle();
            this.addEditStyleChange()
            this.addEditUploadStyleChange()
            //获取下拉框信息
                this.$http({
                    url:`dictionary/page?page=1&limit=100&sort=&order=&dicCode=changdi_types`,
                    method: "get"
                }).then(({ data }) => {
                    if (data && data.code === 0) {
                        this.changdiTypesOptions = data.data.list;
                    }
                });
                this.$http({
                    url:`dictionary/page?page=1&limit=100&sort=&order=&dicCode=banquan_types`,
                    method: "get"
                }).then(({ data }) => {
                    if (data && data.code === 0) {
                        this.banquanTypesOptions = data.data.list;
                    }
                });
                this.$http({
                    url:`dictionary/page?page=1&limit=100&sort=&order=&dicCode=shangxia_types`,
                    method: "get"
                }).then(({ data }) => {
                    if (data && data.code === 0) {
                        this.shangxiaTypesOptions = data.data.list;
                    }
                });


        },
        mounted() {
        },
        methods: {
            // 下载
            download(file){
                window.open(`${file}`)
            },
            // 初始化
            init(id,type) {
                if (id) {
                    this.id = id;
                    this.type = type;
                }
                if(this.type=='info'||this.type=='else'){
                    this.info(id);
                }else if(this.type=='cross'){
                    var obj = this.$storage.getObj('crossObj');
                    for (var o in obj){

                      if(o=='changdiUuidNumber'){
                          this.ruleForm.changdiUuidNumber = obj[o];
                          this.ro.changdiUuidNumber = true;
                          continue;
                      }
                      if(o=='changdiName'){
                          this.ruleForm.changdiName = obj[o];
                          this.ro.changdiName = true;
                          continue;
                      }
                      if(o=='changdiPhoto'){
                          this.ruleForm.changdiPhoto = obj[o];
                          this.ro.changdiPhoto = true;
                          continue;
                      }
                      if(o=='changdiTypes'){
                          this.ruleForm.changdiTypes = obj[o];
                          this.ro.changdiTypes = true;
                          continue;
                      }
                      if(o=='changdiOldMoney'){
                          this.ruleForm.changdiOldMoney = obj[o];
                          this.ro.changdiOldMoney = true;
                          continue;
                      }
                      if(o=='changdiNewMoney'){
                          this.ruleForm.changdiNewMoney = obj[o];
                          this.ro.changdiNewMoney = true;
                          continue;
                      }
                      if(o=='shijianduan'){
                          this.ruleForm.shijianduan = obj[o];
                          this.ro.shijianduan = true;
                          continue;
                      }
                      if(o=='shijianduanRen'){
                          this.ruleForm.shijianduanRen = obj[o];
                          this.ro.shijianduanRen = true;
                          continue;
                      }
                      if(o=='changdiClicknum'){
                          this.ruleForm.changdiClicknum = obj[o];
                          this.ro.changdiClicknum = true;
                          continue;
                      }
                      if(o=='banquanTypes'){
                          this.ruleForm.banquanTypes = obj[o];
                          this.ro.banquanTypes = true;
                          continue;
                      }
                      if(o=='shangxiaTypes'){
                          this.ruleForm.shangxiaTypes = obj[o];
                          this.ro.shangxiaTypes = true;
                          continue;
                      }
                      if(o=='tuijian'){
                          this.ruleForm.tuijian = obj[o];
                          this.ro.tuijian = true;
                          continue;
                      }
                      if(o=='changdiDelete'){
                          this.ruleForm.changdiDelete = obj[o];
                          this.ro.changdiDelete = true;
                          continue;
                      }
                      if(o=='changdiContent'){
                          this.ruleForm.changdiContent = obj[o];
                          this.ro.changdiContent = true;
                          continue;
                      }
                    }
                }
                // 获取用户信息
                this.$http({
                    url:`${this.$storage.get("sessionTable")}/session`,
                    method: "get"
                }).then(({ data }) => {
                    if (data && data.code === 0) {
                        var json = data.data;
                    } else {
                        this.$message.error(data.msg);
                    }
                });
            },
            // 多级联动参数
            info(id) {
                this.$http({
                    url: `changdi/info/${id}`,
                    method: 'get'
                }).then(({ data }) => {
                    if (data && data.code === 0) {
                        this.ruleForm = data.data;
                        //解决前台上传图片后台不显示的问题
                        let reg=new RegExp('../../../upload','g')//g代表全部
                    } else {
                        this.$message.error(data.msg);
                    }
                });
            },
            // 提交
            onSubmit() {
                this.$refs["ruleForm"].validate(valid => {
                    if (valid) {
                        this.$http({
                            url:`changdi/${!this.ruleForm.id ? "save" : "update"}`,
                            method: "post",
                            data: this.ruleForm
                        }).then(({ data }) => {
                            if (data && data.code === 0) {
                                this.$message({
                                    message: "操作成功",
                                    type: "success",
                                    duration: 1500,
                                    onClose: () => {
                                        this.parent.showFlag = true;
                                        this.parent.addOrUpdateFlag = false;
                                        this.parent.changdiCrossAddOrUpdateFlag = false;
                                        this.parent.search();
                                        this.parent.contentStyleChange();
                                    }
                                });
                            } else {
                                this.$message.error(data.msg);
                            }
                        });
                    }
                });
            },
            // 获取uuid
            getUUID () {
                return new Date().getTime();
            },
            // 返回
            back() {
                this.parent.showFlag = true;
                this.parent.addOrUpdateFlag = false;
                this.parent.changdiCrossAddOrUpdateFlag = false;
                this.parent.contentStyleChange();
            },
            //图片
            changdiPhotoUploadChange(fileUrls){
                this.ruleForm.changdiPhoto = fileUrls;
                this.addEditUploadStyleChange()
            },

            addEditStyleChange() {
                this.$nextTick(()=>{
                    // input
                    document.querySelectorAll('.addEdit-block .input .el-input__inner').forEach(el=>{
                        el.style.height = this.addEditForm.inputHeight
                        el.style.color = this.addEditForm.inputFontColor
                        el.style.fontSize = this.addEditForm.inputFontSize
                        el.style.borderWidth = this.addEditForm.inputBorderWidth
                        el.style.borderStyle = this.addEditForm.inputBorderStyle
                        el.style.borderColor = this.addEditForm.inputBorderColor
                        el.style.borderRadius = this.addEditForm.inputBorderRadius
                        el.style.backgroundColor = this.addEditForm.inputBgColor
                    })
                    document.querySelectorAll('.addEdit-block .input .el-form-item__label').forEach(el=>{
                        el.style.lineHeight = this.addEditForm.inputHeight
                        el.style.color = this.addEditForm.inputLableColor
                        el.style.fontSize = this.addEditForm.inputLableFontSize
                    })
                    // select
                    document.querySelectorAll('.addEdit-block .select .el-input__inner').forEach(el=>{
                        el.style.height = this.addEditForm.selectHeight
                        el.style.color = this.addEditForm.selectFontColor
                        el.style.fontSize = this.addEditForm.selectFontSize
                        el.style.borderWidth = this.addEditForm.selectBorderWidth
                        el.style.borderStyle = this.addEditForm.selectBorderStyle
                        el.style.borderColor = this.addEditForm.selectBorderColor
                        el.style.borderRadius = this.addEditForm.selectBorderRadius
                        el.style.backgroundColor = this.addEditForm.selectBgColor
                    })
                    document.querySelectorAll('.addEdit-block .select .el-form-item__label').forEach(el=>{
                        el.style.lineHeight = this.addEditForm.selectHeight
                        el.style.color = this.addEditForm.selectLableColor
                        el.style.fontSize = this.addEditForm.selectLableFontSize
                    })
                    document.querySelectorAll('.addEdit-block .select .el-select__caret').forEach(el=>{
                        el.style.color = this.addEditForm.selectIconFontColor
                        el.style.fontSize = this.addEditForm.selectIconFontSize
                    })
                    // date
                    document.querySelectorAll('.addEdit-block .date .el-input__inner').forEach(el=>{
                        el.style.height = this.addEditForm.dateHeight
                        el.style.color = this.addEditForm.dateFontColor
                        el.style.fontSize = this.addEditForm.dateFontSize
                        el.style.borderWidth = this.addEditForm.dateBorderWidth
                        el.style.borderStyle = this.addEditForm.dateBorderStyle
                        el.style.borderColor = this.addEditForm.dateBorderColor
                        el.style.borderRadius = this.addEditForm.dateBorderRadius
                        el.style.backgroundColor = this.addEditForm.dateBgColor
                    })
                    document.querySelectorAll('.addEdit-block .date .el-form-item__label').forEach(el=>{
                        el.style.lineHeight = this.addEditForm.dateHeight
                        el.style.color = this.addEditForm.dateLableColor
                        el.style.fontSize = this.addEditForm.dateLableFontSize
                    })
                    document.querySelectorAll('.addEdit-block .date .el-input__icon').forEach(el=>{
                        el.style.color = this.addEditForm.dateIconFontColor
                        el.style.fontSize = this.addEditForm.dateIconFontSize
                        el.style.lineHeight = this.addEditForm.dateHeight
                    })
                    // upload
                    let iconLineHeight = parseInt(this.addEditForm.uploadHeight) - parseInt(this.addEditForm.uploadBorderWidth) * 2 + 'px'
                    document.querySelectorAll('.addEdit-block .upload .el-upload--picture-card').forEach(el=>{
                        el.style.width = this.addEditForm.uploadHeight
                        el.style.height = this.addEditForm.uploadHeight
                        el.style.borderWidth = this.addEditForm.uploadBorderWidth
                        el.style.borderStyle = this.addEditForm.uploadBorderStyle
                        el.style.borderColor = this.addEditForm.uploadBorderColor
                        el.style.borderRadius = this.addEditForm.uploadBorderRadius
                        el.style.backgroundColor = this.addEditForm.uploadBgColor
                    })
                    document.querySelectorAll('.addEdit-block .upload .el-form-item__label').forEach(el=>{
                        el.style.lineHeight = this.addEditForm.uploadHeight
                        el.style.color = this.addEditForm.uploadLableColor
                        el.style.fontSize = this.addEditForm.uploadLableFontSize
                    })
                    document.querySelectorAll('.addEdit-block .upload .el-icon-plus').forEach(el=>{
                        el.style.color = this.addEditForm.uploadIconFontColor
                        el.style.fontSize = this.addEditForm.uploadIconFontSize
                        el.style.lineHeight = iconLineHeight
                        el.style.display = 'block'
                    })
                    // 多文本输入框
                    document.querySelectorAll('.addEdit-block .textarea .el-textarea__inner').forEach(el=>{
                        el.style.height = this.addEditForm.textareaHeight
                        el.style.color = this.addEditForm.textareaFontColor
                        el.style.fontSize = this.addEditForm.textareaFontSize
                        el.style.borderWidth = this.addEditForm.textareaBorderWidth
                        el.style.borderStyle = this.addEditForm.textareaBorderStyle
                        el.style.borderColor = this.addEditForm.textareaBorderColor
                        el.style.borderRadius = this.addEditForm.textareaBorderRadius
                        el.style.backgroundColor = this.addEditForm.textareaBgColor
                    })
                    document.querySelectorAll('.addEdit-block .textarea .el-form-item__label').forEach(el=>{
                        // el.style.lineHeight = this.addEditForm.textareaHeight
                        el.style.color = this.addEditForm.textareaLableColor
                        el.style.fontSize = this.addEditForm.textareaLableFontSize
                    })
                    // 保存
                    document.querySelectorAll('.addEdit-block .btn .btn-success').forEach(el=>{
                        el.style.width = this.addEditForm.btnSaveWidth
                        el.style.height = this.addEditForm.btnSaveHeight
                        el.style.color = this.addEditForm.btnSaveFontColor
                        el.style.fontSize = this.addEditForm.btnSaveFontSize
                        el.style.borderWidth = this.addEditForm.btnSaveBorderWidth
                        el.style.borderStyle = this.addEditForm.btnSaveBorderStyle
                        el.style.borderColor = this.addEditForm.btnSaveBorderColor
                        el.style.borderRadius = this.addEditForm.btnSaveBorderRadius
                        el.style.backgroundColor = this.addEditForm.btnSaveBgColor
                    })
                    // 返回
                    document.querySelectorAll('.addEdit-block .btn .btn-close').forEach(el=>{
                        el.style.width = this.addEditForm.btnCancelWidth
                        el.style.height = this.addEditForm.btnCancelHeight
                        el.style.color = this.addEditForm.btnCancelFontColor
                        el.style.fontSize = this.addEditForm.btnCancelFontSize
                        el.style.borderWidth = this.addEditForm.btnCancelBorderWidth
                        el.style.borderStyle = this.addEditForm.btnCancelBorderStyle
                        el.style.borderColor = this.addEditForm.btnCancelBorderColor
                        el.style.borderRadius = this.addEditForm.btnCancelBorderRadius
                        el.style.backgroundColor = this.addEditForm.btnCancelBgColor
                    })
                })
            },
            addEditUploadStyleChange() {
                this.$nextTick(()=>{
                    document.querySelectorAll('.addEdit-block .upload .el-upload-list--picture-card .el-upload-list__item').forEach(el=>{
                        el.style.width = this.addEditForm.uploadHeight
                        el.style.height = this.addEditForm.uploadHeight
                        el.style.borderWidth = this.addEditForm.uploadBorderWidth
                        el.style.borderStyle = this.addEditForm.uploadBorderStyle
                        el.style.borderColor = this.addEditForm.uploadBorderColor
                        el.style.borderRadius = this.addEditForm.uploadBorderRadius
                        el.style.backgroundColor = this.addEditForm.uploadBgColor
                    })
                })
            },
        }
    };
</script>
<style lang="scss">
.editor{
  height: 500px;

  & /deep/ .ql-container {
	  height: 310px;
  }
}
.amap-wrapper {
  width: 100%;
  height: 500px;
}
.search-box {
  position: absolute;
}
.addEdit-block {
	margin: -10px;
}
.detail-form-content {
	padding: 12px;
}
.btn .el-button {
  padding: 0;
}</style>


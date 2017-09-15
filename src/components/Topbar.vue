<template>
    <div id="topbar">
        <div class="logo">
            Resume
        </div>
        <div class="actions">
            <el-button type="primary" @click="signUpDialogVisible = true" v-if="!currentUser">注册</el-button>
            <el-button @click="loginDialogVisible = true" v-if="!currentUser">登录</el-button>
            <el-button v-on:click="preview">预览</el-button>
            <el-button @click="saveOrUpdateResume" v-if="currentUser">保存</el-button>
            <el-button @click="logOut" v-if="currentUser">登出</el-button>
        </div>
        <el-dialog v-if="!currentUser" class="singup" title="注册" :visible.sync="signUpDialogVisible" :modal-append-to-body="false">
            <el-form :model="form">
                <el-form-item label="用户名">
                    <el-input v-model="form.username"></el-input>
                </el-form-item>
                <el-form-item label="密码">
                    <el-input v-model="form.password"></el-input>
                </el-form-item>            
            </el-form>
            <div slot="footer" class="dialog-footer">
                <el-button @click="signUpDialogVisible = false">取消</el-button>
                <el-button type="primary" @click="signUp">注册</el-button>
            </div>
        </el-dialog>
        <el-dialog class="login" title="登录" :visible.sync="loginDialogVisible" :modal-append-to-body="false">
            <el-form :model="form">
                <el-form-item label="用户名">
                    <el-input v-model="loginForm.username"></el-input>
                </el-form-item>
                <el-form-item label="密码">
                    <el-input v-model="loginForm.password"></el-input>
                </el-form-item>            
            </el-form>
            <div slot="footer" class="dialog-footer">
                <el-button @click="loginDialogVisible = false">取消</el-button>
                <el-button type="primary" @click="logIn">登录</el-button>
            </div>
        </el-dialog>        
    </div>
</template>

<script>
import AV from '../lib/leancloud'

export default {
    props: ['resume'],
    data() {
        return {
            currentUser: null,
            signUpDialogVisible: false,
            loginDialogVisible: false,
            form: {
                username: '',
                password: ''
            },
            loginForm: {
                username: '',
                password: ''
            },
            formLabelWidth: '120px',
            resumeContent: ''
        }
    },
    created(){
        this.currentUser = this.getCurrentUser()
        this.fetchResumeContent()
    },
    methods: {
        preview() {
            this.$emit('preview')
        },
        getCurrentUser() {
            let current = AV.User.current()
            if (current) {
                let {id, createdAt,attributes:{username}} = AV.User.current()
                return {id, username, createdAt}
            } else {
                return null
            }
        },
        signUp() {
            this.signUpDialogVisible = false
            let user = new AV.User()
            // 设置用户名
            user.setUsername(this.form.username)
            // 设置密码
            user.setPassword(this.form.password)

            user.signUp().then((loginedUser) => {
                console.log(loginedUser)
                this.currentUser = this.getCurrentUser()
            },function(error){
                console.log('注册失败')
            })
        },
        fetchResumeContent(){
            if(this.currentUser){
                var query = new AV.Query('Resumefolder')
                console.log(query.length,1)
                query.find().then((resume)=>{
                    console.log(resume,2)
                    console.log(resume.length)
                    let avResume = resume[0]
                    let id = avResume.id
                    this.resumeContent = JSON.parse(avResume.attributes.content)
                    console.log(this.resumeContent,3)
                    this.resumeContent.id = id
                    this.$emit('updete:resume',this.resumeContent)
                },function(error){
                    console.error(error)
                })
            }
        },
        logIn(){
            AV.User.logIn(this.loginForm.username,this.loginForm.password).then((loginedUser)=>{
                this.currentUser = this.getCurrentUser()
                this.loginDialogVisible = false
                this.fetchResumeContent()
            },function(error){
                console.log('登录失败')
            })
        },
        logOut(){
            AV.User.logOut()
            this.currentUser = null
            //强行刷新一次页面退回最初状态
            window.location.reload()
        },
        saveOrUpdateResume(){
            if(this.resume.id){
                this.updateResumeContent()
            }else{
                this.saveResumeContent()
            }
        },
        saveResumeContent(){
            let session = JSON.stringify(this.resume)
            var Resumefolder = AV.Object.extend('Resumefolder')
            var resumefolder = new Resumefolder()

            //设置当前登录用户读写
            var acl = new AV.ACL()
            acl.setReadAccess(AV.User.current(),true)
            acl.getWriteAccess(AV.User.current(),true)

            resumefolder.set('content',session)

            resumefolder.setACL(acl)

            resumefolder.save().then((resume)=>{
                this.resume.id = resume.id
                console.log('保存成功')
            },function(error){
                alert('保存失败')
            })
        },
        updateResumeContent(){
            let session = JSON.stringify(thie.resume)
            let avResume = AV.Object.createWithoutData('Resumefolder',this.resume.id)
            avResume.set('content',session)
            avResume.save().then(()=>{
                console.log('更新成功')
            })
        }
    }
}
</script>


<style>
#topbar{
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 16px;
    font-size: 20px;
}
</style>

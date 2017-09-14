<template>
    <div id="topbar">
        <div class="logo">
            Resume
        </div>
        <div class="actions">
            <el-button type="primary" @click="signUpDialogVisible = true">注册</el-button>
            <el-button @click="loginDialogVisible = true">登录</el-button>
            <el-button v-on:click="preview">预览</el-button>
            <el-button>保存</el-button>
            <el-button>登出</el-button>
        </div>
        <el-dialog class="singup" title="注册" :visible.sync="signUpDialogVisible" :modal-append-to-body="false">
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
                <el-button type="primary">注册</el-button>
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
                <el-button type="primary">登录</el-button>
            </div>
        </el-dialog>        
    </div>
</template>

<script>
import AV from '../lib/leancloud'

export default {
    data(){
        return {
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
        }
    },
    methods: {
        preview() {
            this.$emit('preview')
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

<template>
    <div>
        <h2>工作经历</h2>
        <el-form>
            <div v-for="(work,index) in workHistory" class="one-work-history">
                <i v-on:click="removeWorkHistory(index)" class="el-icon-close"></i>
                <el-form-item label="公司">
                    <el-input v-model="work.company"></el-input>
                </el-form-item>
                <el-form-item label="工作内容">
                    <el-input v-model="work.content"></el-input>
                </el-form-item>
            </div>
            <el-button type="primary" v-on:click="addWorkHistory()">添加</el-button>
        </el-form>
    </div>
</template>

<script>
export default {
    props: ['workHistory'],
    methods: {
        addWorkHistory(){
            this.workHistory.push({
                company: '',
                content: ''
            })
        },
        removeWorkHistory(index){
            this.workHistory.splice(index,1)
        }
    }
}
</script>

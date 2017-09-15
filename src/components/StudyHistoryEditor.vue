<template>
    <div>
        <h2>学习经历</h2>
        <el-form>
            <div v-for="(item,index) in studyHistory" class="one-work-history">
                <i v-on:click="removeStudyHistory(index)" class="el-icon-close"></i>
                <el-form-item label="学校">
                    <el-input v-model="studyHistory.school" /></el-input>
                </el-form-item>
                <el-form-item label="学历">
                    <el-input v-model="studyHistory.degree" /></el-input>
                </el-form-item>
                <el-form-item label="时间">
                    <el-input v-model="studyHistory.duration" /></el-input>
                </el-form-item>
            </div>
            <el-button type="primary" v-on:click="addStudyHistory">添加</el-button>
        </el-form>
    </div>
</template>

<script>
export default {
    props: ["studyHistory"],
    methods: {
        addStudyHistory() {
            this.studyHistory.push({
                school: '',
                degree: '',
                duration: ''
            })
        },
        removeStudyHistory(index) {
            this.studyHistory.splice(index, 1)
        }
    },
}
</script>

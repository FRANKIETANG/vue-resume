<template>
    <div id="editor">
        <nav>
            <ol>
                <li v-for="i in [0,1,2,3,4,5]" v-bind:class="{active:currentTab === i}" v-on:click="currentTab = i">
                    <svg class="icon">
                        <use v-bind:xlink:href="'#icon-'+icons[i]"></use>
                    </svg>                    
                </li>
            </ol>
        </nav>
        <ol class="panels">
            <li v-bind:class="{active:currentTab === 0}">
                <h2>个人信息</h2>
                <el-form>
                    <el-form-item label="姓名">
                        <el-input v-model="profile.name"></el-input>
                    </el-form-item>
                    <el-form-item label="城市">
                        <el-input v-model="profile.city"></el-input>
                    </el-form-item>
                    <el-form-item label="出生年日">
                        <el-input v-model="profile.birth"></el-input>
                    </el-form-item>                                        
                </el-form>
            </li>
            <li v-bind:class="{active:currentTab === 1}">
                <h2>工作经历</h2>
            </li>
            <li v-bind:class="{active:currentTab === 2}">
                <h2>学习经历</h2>
            </li>
            <li v-bind:class="{active:currentTab === 3}">
                <h2>项目经历</h2>
            </li>
            <li v-bind:class="{active:currentTab === 4}">
                <h2>获奖信息</h2>
            </li>
            <li v-bind:class="{active:currentTab === 5}">
                <h2>联系方式</h2>
            </li>                                                
        </ol>
    </div>
</template>

<script>
export default {
    data(){
        return{
            currentTab: 0,
            icons: ['sekuaibianxielianxiren','sekuaidiannao','icon-test1','icon-test','icon-test2','sekuaiyouxiji'],
            profile: {
                name: '',
                city: '',
                birth: ''
            }
        }
    }
}
</script>


<style>
#editor{
    min-height: 100px;
    display: flex;
}
#editor nav{
    background: #000;
    width: 80px;
}
nav ol li{
    padding: 16px 0;
    text-align: center;
}
nav ol li.active{
    background: #fff;
}
nav ol li.active .icon{
    fill: #000;
}
.panels li.active{
    display: block;
}
.panels li el-form el-input{
    width: 100%;
    background-color: red;
}
</style>

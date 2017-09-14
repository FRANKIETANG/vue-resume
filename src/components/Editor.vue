<template>
    <div id="editor">
        <nav>
            <ol>
                <li v-for="i in tabCount" v-bind:class="{active:currentTab === i}" v-on:click="currentTab = i">
                    <svg class="icon">
                        <use v-bind:xlink:href="'#icon-'+icons[i]"></use>
                    </svg>                    
                </li>
            </ol>
        </nav>
        <ol class="panels">
            <li v-bind:class="{active:currentTab === 0}">

                <ProfileEditor v-bind:profile="profile" />

            </li>
            <li v-bind:class="{active:currentTab === 1}">

                <WorkHistoryEditor v-bind:workHistory="workHistory"/>

            </li>
            <li v-bind:class="{active:currentTab === 2}">
                
                <StudyHistoryEditor v-bind:studyHistory="studyHistory"/>

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
import ProfileEditor from './ProfileEditor'
import WorkHistoryEditor from './WorkHistoryEditor'
import StudyHistoryEditor from './StudyHistoryEditor'

export default {
    components: {
        ProfileEditor,
        WorkHistoryEditor,
        StudyHistoryEditor
    },
    data(){
        return{
            currentTab: 0,
            tabCount: this.initTabcount(),
            icons: ['sekuaibianxielianxiren','sekuaidiannao','icon-test1','icon-test','icon-test2','sekuaiyouxiji'],
            profile: {
                name: '',
                city: '',
                birth: ''
            },
            workHistory: [
                { 
                    company: '',
                    content: '' 
                }
            ],
            studyHistory: [
                {
                    school: '',
                    degree: '',
                    duration: ''
                }
            ]
        }
    },
    methods:{
        initTabcount: function(){
            let count = [];
            for (let i = 0; i < 6; i++) {
                count[i] = i;
            }
            return count
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
.panels{
    overflow: auto;
    flex: 1;
}
.panels li{
    display: none;
    padding: 32px;
}
.panels li.active{
    display: block;
}
.panels li el-form el-input{
    width: 100%;
    background-color: red;
}
.one-work-history{
    position: relative;
}
.one-work-history .el-icon-close{
    position: absolute;
    right: 0;
    top: 0;
    font-size: 10px;
    line-height: 20px;
    z-index: 1;
    cursor: pointer;
}
</style>

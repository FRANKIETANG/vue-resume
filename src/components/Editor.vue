<template>
    <div id="editor">
        <nav>
            <ol>
                <li v-for="i in tabCount" v-bind:class="{active:currentTab === i}" v-on:click="currentTab = i" :key="i">
                    <svg class="icon">
                        <use v-bind:xlink:href="'#icon-'+icons[i]"></use>
                    </svg>
                </li>
            </ol>
        </nav>
        <ol class="panels">
            <li v-bind:class="{active:currentTab === 0}">

                <ProfileEditor v-bind:profile="resume.profile" />

            </li>
            <li v-bind:class="{active:currentTab === 1}">

                <itemHistoryEditor v-bind:items="resume.workHistory" v-bind:labels="{company:'公司',addr:'城市',duration:'时间',name:'岗位名字',content:'工作内容'}" title="工作经历" />

            </li>
            <li v-bind:class="{active:currentTab === 2}">

                <itemHistoryEditor v-bind:items="resume.studyHistory" v-bind:labels="{school:'学校',degree:'学历',duration:'时间',name:'专业',contacts:'主修课程'}" title="学习经历" />

            </li>
            <li v-bind:class="{active:currentTab === 3}">

                <itemHistoryEditor v-bind:items="resume.projects" v-bind:labels="{name:'项目经历',content:'项目内容'}" title="项目经历" />

            </li>
            <li v-bind:class="{active:currentTab === 4}">

                <itemHistoryEditor v-bind:items="resume.awards" v-bind:labels="{name:'奖项',content:'奖项简介'}" title="获奖信息" />

            </li>
            <li v-bind:class="{active:currentTab === 5}">

                <ContactsEditor v-bind:contacts="resume.contacts" />

            </li>
        </ol>
    </div>
</template>

<script>
import ProfileEditor from './ProfileEditor'
import itemHistoryEditor from './itemHistoryEditor'
import ContactsEditor from './Contacts'

export default {
    components: {
        ProfileEditor,
        itemHistoryEditor,
        ContactsEditor
    },
    props: ['resume'],
    data() {
        return {
            currentTab: 0,
            tabCount: this.initTabcount(),
            icons: ['sekuaibianxielianxiren', 'sekuaidiannao', 'icon-test1', 'icon-test', 'icon-test2', 'sekuaiyouxiji']
        }
    },
    methods: {
        initTabcount: function() {
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
#editor {
    min-height: 100px;
    display: flex;
}

#editor nav {
    background: #3d3c3c;
    width: 80px;
}

nav ol li {
    padding: 16px 0;
    text-align: center;
}

nav ol li.active {
    background: #fff;
}

nav ol li.active .icon {
    fill: #3d3c3c;
}

.panels {
    overflow: auto;
    flex: 1;
}

.panels li {
    display: none;
    padding: 32px;
}

.panels li.active {
    display: block;
}

.panels li el-form el-input {
    width: 100%;
    background-color: red;
}

.one-work-history {
    position: relative;
}

.one-work-history .el-icon-close {
    position: absolute;
    right: 0;
    top: 0;
    font-size: 10px;
    line-height: 20px;
    z-index: 1;
    cursor: pointer;
}
</style>

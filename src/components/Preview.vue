<template>
    <div id="preview">
        <div class="container">
            <div class="header">
                <div class="full-name">
                    <span class="name">{{resume.profile.name || '姓名'}}</span>
                </div>
                <div class="contact-info">
                    <span class="email">Email: </span>
                    <span class="email-val">{{resume.contacts.email || '邮箱'}}</span>
                    <span class="separator"></span>
                    <span class="phone">Phone: </span>
                    <span class="phone-val">{{resume.contacts.phone || '电话'}}</span>
                </div>
                <div class="about">
                    <span class="position">{{resume.profile.position || '目标岗位'}}</span>
                    <span class="desc">{{resume.profile.title || '自我介绍'}}</span>
                </div>
            </div>
            <div class="datails">
                <div class="section" v-if="filter(resume.workHistory).length > 0">
                    <div class="section-title">Experience</div>
                    <div class="section-list">
                        <div class="section-list-item" v-for="(item,index) in filter(resume.workHistory)" :key="index">
                            <div class="left">
                                <div class="name">{{item.company || '公司'}}</div>
                                <div class="addr">{{item.addr || '城市'}}</div>
                                <div class="duration">{{item.duration || '时间'}}</div>
                            </div>
                            <div class="right">
                                <div class="name">{{item.name || '岗位名字'}}</div>
                                <div class="desc">{{item.content || '工作内容'}}</div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="section" v-if="filter(resume.studyHistory).length > 0">
                    <div class="section-title">Education</div>
                    <div class="section-list">
                        <div class="section-list-item" v-for="(item,index) in filter(resume.studyHistory)" :key="index">
                            <div class="left">
                                <div class="name">{{item.school || '学校'}}</div>
                                <div class="addr">{{item.degree || '学历'}}</div>
                                <div class="duration">{{item.duration || '时间'}}</div>
                            </div>
                            <div class="right">
                                <div class="name">{{item.name || '专业'}}</div>
                                <div class="desc">{{item.contacts || '主修课程'}}</div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="section" v-if="filter(resume.projects).length > 0">
                    <div class="section-title">Projcets</div>
                    <div class="section-list">
                        <div class="section-list-item" v-for="(item,index) in filter(resume.projects)" :key="index">
                            <div class="name">{{item.name || '项目'}}</div>
                            <div class="text">{{item.content || '项目名字'}}</div>
                        </div>
                    </div>
                </div>
                <div class="section" v-if="filter(resume.awards).length > 0">
                    <div class="section-title">Awards</div>
                    <div class="section-list">
                        <div class="section-list-item" v-for="(item,index) in filter(resume.awards)" :key="index">
                            <div class="name">{{item.name || '获奖名称'}}</div>
                            <div class="text">{{item.content || '奖项简介'}}</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['resume'],
    methods: {
        filter(array) {
            return array.filter(item => !this.isEmpty(item))
        },
        isEmpty(object) {
            let empty = true
            for (let key in object) {
                if (object[key]) {
                    empty = false
                    break
                }
            }
            return empty
        }
    }
}
</script>


<style scoped lang='scss'>
#preview {
    min-height: 100%;
    .container {
        background: #fff;
        margin: 0px auto 0px;
        padding: 40px;
        margin: 50px;
    }
    .header {
        margin-bottom: 30px;
        .full-name {
            font-size: 40px;
            margin-bottom: 10px;
        }
        .name {
            font-weight: 700;
        }
        .contact-info {
            margin-bottom: 20px;
        }
        .email,
        .phone {
            color: #999;
            font-weight: 300;
        }
        .separator {
            height: 10px;
            display: inline-block;
            border-left: 2px solid #999;
            margin: 0px 10px;
        }
        .position {
            font-weight: bold;
            display: inline-block;
            margin-right: 10px;
            text-decoration: underline;
        }
    }
    .datails {
        line-height: 20px;
        .section {
            margin-bottom: 40px;
        }
        .section:last-of-type {
            margin-bottom: 0px;
        }
        .section-title {
            letter-spacing: 2px;
            color: rgb(78, 145, 255);
            font-weight: bold;
            margin-bottom: 10px;
        }
        .section-list-item {
            margin-bottom: 40px;
        }
        .section-list-item::last-of-type {
            margin-bottom: 0;
        }
        .left,
        .right {
            vertical-align: top;
            display: inline-block;
        }
        .left {
            width: 60%;
        }
        .right {
            width: 39%;
        }
        .name {
            font-weight: bold
        }
    }
}
</style>


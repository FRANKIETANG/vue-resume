<template>
    <div id="preview">
        <h1>{{resume.profile.name || '姓名'}}</h1>
        <p>{{resume.profile.city}} | {{resume.profile.birth}}</p>
        <p>{{resume.profile.title}}</p>
        <section v-if="filter(resume.projects).length > 0">
            <ul>
                <li v-for="item in filter(resume.projects)" :key="item">
                    {{item.name}}
                    {{item.content}}
                </li>
            </ul>
        </section>
    </div>
</template>

<script>
export default {
    props: ['resume'],
    methods: {
        filter(array){
            return array.filter(item => !this.isEmpty(item))
        },
        isEmpty(object){
            let empty = true
            for(let key in object){
                if(object[key]){
                    empty = false
                    break
                }
            }
            return empty
        }
    }
}
</script>


<style>
#preview{
    min-height: 100px;
}
</style>


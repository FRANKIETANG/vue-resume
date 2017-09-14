<template>
    <div>
        <h2>{{title}}</h2>
        <el-form>
            <div v-for="(item,index) in items" class="one-work-history" :key="index">
                <i v-on:click="removeItem(index)" class="el-icon-close"></i>
                <el-form-item v-for="key in keys" v-bind:label="labels[key] || key" :key="key">
                    <el-input v-model="item[key]"></el-input>
                </el-form-item>
            </div>
            <el-button type="primary" v-on:click="addItem()">添加</el-button>
        </el-form>
    </div>
</template>

<script>
export default {
    props: ['items','labels','title'],
    computed: {
        keys(){
            return (Object.keys(this.items[0]))
        }
    },
    methods: {
        addItem(){
            const empty = {}
            this.keys.map((key)=>{
                empty[key] = ''
            })
            this.items.push(empty)
        },
        removeItem(index){
            this.items.splice(index,1)
        }
    }
}
</script>

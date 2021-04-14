<template>
    <div class="header-table">
    <el-container>
        <el-header class="header-box">
            <div class="header">
		        <ul class="menu">
                    <li class="icon" @click="backHome"><a><i class="el-icon-s-home"></i>Home</a></li>
                </ul>
            </div>
        </el-header>
    </el-container>
    </div>
</template>

<script>

export default {
    methods: {
        backHome:function(){
            this.$router.push('/home')
        }
    },

};
</script>

<style>
.el-header {
    background-color: #409EFF;
    color: #333;
    text-align: center;
    line-height: 60px;
}
.header ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    overflow: hidden;
}
.header li {
    float: left;
    padding: 0px;
    font-family:"Times New Roman", Times, serif;
}
.header a {
    display: block;
    color: white;
    text-align: center;
    padding-left: 10px;
    padding-right: 10px;
    text-decoration: none;
    font-size:17px;
    font-family:"Times New Roman", Times, serif;
}
.header li:hover{
    background-color: rgb(119, 188, 252);
    /* background-color: rgba(0,68,187,0.7); */
}
</style>

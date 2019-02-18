<template>
    <tr>
        <td>{{id}}</td>
        <td>{{name}}</td>
        <td>{{phone}}</td>
        <td>{{email}}</td>
        <td>
            <button>Select</button>
        </td>
    </tr>
</template>

<script>
export default {
    props:['id','name','phone','email'],
    data(){
            return{
            }
        },
}
</script>

<style lang="scss">
td:hover{
    
}

    td{
        padding:10px;
        button{
            @include sButton();
        }
    }
</style>



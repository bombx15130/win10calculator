<template>
    <tr>
        <td>{{ sGender }}</td>
        <td>{{ sName }}</td>
        <td>{{ sPhone }}</td>
        <td>{{ sMail }}</td>
    </tr>
</template>

<script>
export default {
    props:['sGender','sName','sPhone','sMail'],
    data(){
        return{
        }
    }
}
</script>

<style>
td{
    padding:10px;
}
</style>



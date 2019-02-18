<template>
    <div class="pagination">
        <ul>
            <li
                v-for="p in pages"
                :key="p.key"
                :class="{ selected: currentPage == p.value }"
                @click="onClick(p.value)"
            >{{ p.key }}</li>
        </ul>
    </div>
</template>

<script>
export default {
    props:['perShow', 'count', 'currentPage'],
    data(){
        return {
        }
    },
    computed: {
        pages: function () {
            const pageCount =  this.count / this.perShow
            const pager = 2

            let range = []
            for (let i = Math.max(pager, this.currentPage - pager); i <= Math.min(pageCount - 1, this.currentPage + pager); i++) {
                range.push({ key: i, value: i })
            }

            if (this.currentPage > pager) {
                range.unshift({
                    key: '...',
                    value: this.currentPage - 5 > 1 ? this.currentPage - 5 : 1
                })
            }
            if (this.currentPage + pager < pageCount - 1) {
                range.push({
                    key: '...',
                    value: this.currentPage + 5 <= pageCount ? this.currentPage + 5 : pageCount
                })
            }

            range.unshift({ key: 1, value: 1 })
            range.unshift({ key: '<', value: this.currentPage - 1 })
            range.push({ key: 50, value: 50 })
            range.push({ key: '>', value: this.currentPage + 1 })

            return range
        },
    },
    methods:{
        onClick:function (value){
            let v
            switch (value) {
                case '<':
                    break
                case '>':
            }
            this.$emit('click', value)
        }
    }
}
</script>

<style>
*{
    /* outline: 1px solid #F00; */
}
li{
    padding:10px;
    display:inline-block;
    border:1px solid #CCC;
    font-size: 14px;
    cursor: pointer;
}

li:hover {
    background: #ccc;
}

.selected {
    color: #fff;
    background: #1c839c;
}

</style>



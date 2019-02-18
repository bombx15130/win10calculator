<template>
    <div @click="onClick" :class="['calButton', type]">{{ name }}</div>
</template>

<script>
export default {
    props: ['name', 'type'],
    data: function () {
        return {
        }
    },
    methods: {
        onClick: function () {
            if (this.type === 'number') {
                this.$emit('numberclick', this.name)
            } else {
                this.$emit('operatorclick', this.name)
            }
        }
    }
}
</script>

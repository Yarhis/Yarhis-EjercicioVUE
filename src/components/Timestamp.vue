<template>
    
        <span>{{formatdatetime}}</span>

   
</template>

<script>
    export default {
        name: "Timestamp",
        props: {
            datetime: Date
        },
        computed: {
            formatdatetime(){
                return this.pad(this.datetime.getDate()) + "/" + this.pad((this.datetime.getMonth()+1)) + "/" + this.datetime.getFullYear() + "--" + this.pad(this.datetime.getHours()) + ":" + this.pad(this.datetime.getMinutes()) + ":" + this.pad(this.datetime.getSeconds());
            }
        },

        methods: {
            pad(s) {
                return (s<10) ? "0" + s : s;
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>
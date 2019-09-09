<template>
    <header class="header">
        <h1>
            {{day}} {{dayNum}}, {{month}}-{{year}}
        </h1>
    </header>
</template>

<script>

export default {
    name: "Header",
    methods:{
        setdate(){
            const dayWeek = ["", "Monday", "Tuesday", "Wednessday", "Thursday", "Friday", "Saturday", "Sunday"];
            const month = ['January','February','March', 'April','May', 'June','July', 'August', 'September', 'October', 'November', 'December'];
            var currentDate = new Date().getDay();
            var numDay = new Date().getDate();
            var currentMonth = new Date().getMonth();
            var currentYear = new Date().getFullYear();
            this.dayNum = numDay;
            this.day = dayWeek[currentDate];
            this.month = month[currentMonth];
            this.year = currentYear;
        }
    },
    mounted(){
        this.setdate();
    },
    data(){
        return{
            day:"",
            month:"",
            year:"",
            dayNum:"",
        }
    },

}
</script>

<style scoped>
    .header{
        margin-left: auto;
        margin-right: auto;
        width: 40em;
        border-image: 30%;
        background: turquoise;
        color: blue;
        text-align: center;
        padding: 10px;
        border:1px solid blue;
        height:60px;
        font-weight: bold;

    } 
    .header a{
        color: #fff;
        padding-right: 5px;
    }
</style>
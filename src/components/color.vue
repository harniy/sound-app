<template>
    <div class="color_section">
        <h4>background Color:</h4>

        
            <ul class="colors">
                <li class="clr"
                v-for="color in colors"
                :key="color"
                :style="`background:${color}`"
                @click='bgColor(color)'
                ></li>
            </ul>
        
    </div>
</template>


<script>
export default {
    data(){
        return{
            colors: ["#b4e43fd1", "#d12039", "#151039", "#000000", "#fff", '#ffeb3bc4']
        }
    },
    methods:{
        bgColor(color){
            this.$emit('setColor', color)
        }
    }
}
</script>


<style>
h4{
    text-transform: uppercase;
    margin: 0;
}
ul.colors {
    display: flex;
    justify-content: center;
    align-items: center;
}

li.clr {
    width: 25px;
    height: 25px;
    margin: 0 7px;
    cursor: pointer;
}

</style>
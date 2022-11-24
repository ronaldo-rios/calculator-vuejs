    // A tag template é essencial para encapsular todo o html do componente:
<template>
    <div class="hello">
        <h1>{{ msg }}</h1>
        <div>

            <div class="col-md-4 m-3">
                <table class="table table-bordered">
                    
                    <tbody>
                        <tr class="output">
                            <td colspan="4">
                                {{ output || 0 }}
                            </td>
                        </tr>
                        <tr>
                            <td class="clean">DEL</td>
                            <td v-on:click="clearField" class="clean">AC</td>
                            <td>raiz</td>
                            <td>/</td>
                        </tr>
                        <tr>
                            <td>7</td>
                            <td>8</td>
                            <td>9</td>
                            <td>X</td>
                        </tr>
                        <tr>
                            <td>4</td>
                            <td>5</td>
                            <td>6</td>
                            <td>-</td>
                        </tr>
                        <tr>
                            <td>1</td>
                            <td>2</td>
                            <td>3</td>
                            <td>+</td>
                        </tr>
                        <tr>
                            <td v-on:click="calculatePercent">%</td>
                            <td>0</td>
                            <td>.</td>
                            <td class="equal">=</td>
                        </tr>
                    </tbody>
                </table>
            </div>

        </div>
    </div>
</template>
    

<script>// Component name "Calculator" should always be multi-word  vue/multi-word-component-names
export default {
    name: 'CalculatorVue',
    props: {
        msg: String
    },
    data(){
        return {
            output:''
        }
    },
    methods: {
        clearField(){
            this.output = '';
        },
        calculatePercent() {
            this.output = parseFloat(this.output) / 100;
        }
    }
}

</script>

<style scoped>
h3 {
    margin: 40px 0 0;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983
}

.output {
    background-color: rgb(14, 14, 14);
    color:#fff;
}

.equal {
    background-color:rgb(3, 131, 182);
    color:white;
}

.clean {
    background-color: rgb(236, 174, 4);
}

.equal:active {
    background-color: rgb(7, 74, 161);
}

.clean:active {
    background-color: rgb(165, 136, 8);
}

td {
    cursor:pointer;
}
</style>
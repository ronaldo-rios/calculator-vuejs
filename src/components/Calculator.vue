    // A tag template é essencial para encapsular todo o html do componente:
<template>
<div id="interface">
    <div id="msg">
        <h1>{{ msg }}</h1>
        <img :src="logo" :alt="description">
    </div>

    <div class="hello">
        <div id="bodyCalculator">

            <div class="col-md-4 calc bg bg-dark rounded-4 m-4">
                <table class="table table-borderless">

                    <tbody>
                        <tr class="output">
                            <!-- // Dentro da td temos a função de data do display e hora do display.
                            //Foi usada uma hierarquia de divs para que pudesse ser feito
                            //o comando space-between para o afastamento de data e hora: -->
                            <td v-on="init()" colspan="4">
                                <div id="displayDateAndTime">
                                    <div>{{ displayDate }}</div>
                                    <div>{{ displayTime }}</div>
                                </div>
                                <div>
                                 <!-- Aqui temos a parte de visualização dos números no display: -->
                                <br id="displayNumber">
                                    {{ output || 0 }}
                                </div>
                            </td>
                        </tr>
                        <tr>
                            <td class="clean" v-on:click="clickDel">DEL</td>
                            <td v-on:click="clearField" class="clean">AC</td>
                            <td class="operators" v-on:click="SquareRoot" alt="squareroot"><i
                                    class="fa-solid fa-square-root-variable"></i></td>
                            <td class="operators" @click="processOutput('divide')"><i class="fa-solid fa-divide"></i>
                            </td>
                        </tr>
                        <tr>
                            <td class="number" v-on:click="getNumber('7')" @click="limitNumbers">7</td>
                            <td class="number" v-on:click="getNumber('8')" @click="limitNumbers">8</td>
                            <td class="number" v-on:click="getNumber('9')" @click="limitNumbers">9</td>
                            <td class="operators" @click="processOutput('multiply')">X</td>
                        </tr>
                        <tr>
                            <td class="number" v-on:click="getNumber('4')" @click="limitNumbers">4</td>
                            <td class="number" v-on:click="getNumber('5')" @click="limitNumbers">5</td>
                            <td class="number" v-on:click="getNumber('6')" @click="limitNumbers">6</td>
                            <td class="operators" @click="processOutput('subtract')">-</td>
                        </tr>
                        <tr>
                            <td class="number" v-on:click="getNumber('1')" @click="limitNumbers">1</td>
                            <td class="number" v-on:click="getNumber('2')" @click="limitNumbers">2</td>
                            <td class="number" v-on:click="getNumber('3')" @click="limitNumbers">3</td>
                            <td class="operators" @click="processOutput('addition')">+</td>
                        </tr>
                        <tr>
                            <td class="operators" v-on:click="calculatePercent">%</td>
                            <td class="number" v-on:click="getNumber('0')" @click="limitNumbers">0</td>
                            <td class="operators" v-on:click="getDot">.</td>
                            <td class="equal" @click="updateOutput">=</td>
                        </tr>
                    </tbody>
                </table>
            </div>

        </div>
    </div>
</div>
</template>
    

<script>// Component name "Calculator" should always be multi-word  vue/multi-word-component-names


export default {
    name: 'CalculatorVue',
    props: {
        msg: String,
        
    },
    data() {
        return {
            displayTime: Date,
            displayDate: Date,
            output: '',
            previousValue: null,
            operationFired: false,
            logo: "/img/logo.png",
            description: "Logo Vue JS"
        }
    }, 
    
    
    //  Métodos usados para as operações de todos os botões da calculadora:
    methods: {
        // Limpar tudo:
        clearField() {
            this.output = '';
        },
        // Deletar um dígito por vez:
        clickDel(){
            if(this.output.length > 1){
                this.output = this.output.substring(0, this.output.length - 1);
            }
            else {
                this.output = '0';
            }
        },
        // Porcentagem:
        calculatePercent() {
            this.output = parseFloat(this.output) / 100;
        },
        // Raiz quadrada:
        SquareRoot() {
            this.output = parseFloat(Math.sqrt(this.output));
        },
        // Pegar número:
        getNumber(number) {

            if (this.operationFired) {
                this.output = ''
                this.operationFired = false
            }

            this.output = `${this.output}${number}`;
        },
        // Limitador do ".":
        getDot() {
            if (this.output.indexOf('.') === -1) {
                this.output = this.output + '.';
            }
        },
        // Processo de saída nas operações:
        processOutput(value) {

            if (value == 'addition') {
                this.operation = (a, b) => {
                    return parseFloat(a) + parseFloat(b);
                }
            }
            else if (value == 'subtract') {
                this.operation = (a, b) => {
                    return parseFloat(a) - parseFloat(b);
                }
            }
            else if (value == 'multiply') {
                this.operation = (a, b) => {
                    return parseFloat(a) * parseFloat(b);
                }
            }
            else if (value == 'divide') {
                this.operation = (a, b) => {
                    return parseFloat(a) / parseFloat(b);
                }
            }

            this.previousValue = this.output;
            this.operationFired = true;
        },
        // Função de atualização da operação para acréscimo de números sem perca do anterior:
        updateOutput() {
            this.output = `${this.operation(this.previousValue, this.output)}`;
            this.previousValue = null;
        },
        // Instância da data:
        setDisplayDateTime() {
            this.displayDate = new Date().toLocaleDateString("pt-br", {
                day: "2-digit",
                month: "long",
                year: "numeric"
            });
            // Instância do timer:
            this.displayTime = new Date().toLocaleTimeString("pt-br");
        },//Função que chama a função de instância de data e hora:
        init() {
            this.setDisplayDateTime();
            setInterval(() => {
                this.setDisplayDateTime();
            }, 1000);
        },
        // Limitador de números para não ocorrer o transbordamento no CSSe HTML:
        limitNumbers() {  
                    if(this.output.length > 26){
                        this.output = this.output.substring(0, 26)
                    }
        }

    }

}

</script>



<!-- Escopo do CSS da Calculator: -->
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
    color: #42b983;
}

.output {
    background-color: rgb(14, 14, 14);
    color: #fff;
}

.equal {
    background-color: rgb(3, 131, 182);
    color: white;
    border-radius: 10px;
    padding: 12px 12px;
}

.clean {
    background-color: rgb(236, 174, 4);
    border-radius: 10px;
    padding: 12px 12px;
}

.equal:active {
    background-color: rgb(7, 74, 161);
}

.clean:active {
    background-color: rgb(165, 136, 8);

}

.number {
    background-color: #6C757C;
    color: white;
    border-radius: 10px;
    padding: 12px 12px;
}

.number:active {
    background-color: black;
    color: white;

}

.operators {
    background-color: #6C757C;
    color: white;
    border-radius: 10px;
    padding: 12px 12px;
}

.operators:active {
    background-color: black;
    color: white;
}

#bodyCalculator {
    background-color: #212529;
    display: flex;
    align-items: center;
    border-radius: 10px;
    
}

.hello {
    display: flex;
    justify-content: center;
    align-items: center;
    height:auto;
   
}

#msg {
    display: flex;
    justify-content: center;
}


td {
    cursor: pointer;
    width: 70px;
    height: 70px;
    font-size: 25px;
}

table {
    border-collapse: separate;
    border-spacing: 15px 10px;
}

img {
    margin-left: 27px;
    width: 70px;
    height: 70px;
    animation: go-back 5s infinite;
}

@keyframes go-back {
    0% {
        transform: rotate(0);
    }
    100% {
        transform: rotate(360deg);
    }
}

.move {
    animation: go-back 5s;
}
.calc {
    width: 400px;
}

#display-time {
    font-size: smaller;
}

#display-date {
    font-size: smaller;
}

#interface {
    background-color: #65f7b5f6;
    display: grid;
    min-width:700px;
    justify-content: center;
    height: 100vh;
}

* {
    margin: 0;
    box-sizing:border-box;
}

#displayDateAndTime {
    font-size: 15px;
    display:flex;
    flex: 2;
    justify-content: space-between;
    
}


</style>
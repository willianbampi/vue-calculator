<template>
    <div class="calculator">
        <Display :value="displayValue"></Display>
        <Button label="AC" triple @on-click="clearMemory"></Button>
        <Button label="/" operation @on-click="setOperation"></Button>
        <Button label="7" @on-click="addDigit"></Button>
        <Button label="8" @on-click="addDigit"></Button>
        <Button label="9" @on-click="addDigit"></Button>
        <Button label="*" operation @on-click="setOperation"></Button>
        <Button label="4" @on-click="addDigit"></Button>
        <Button label="5" @on-click="addDigit"></Button>
        <Button label="6" @on-click="addDigit"></Button>
        <Button label="-" operation @on-click="setOperation"></Button>
        <Button label="1" @on-click="addDigit"></Button>
        <Button label="2" @on-click="addDigit"></Button>
        <Button label="3" @on-click="addDigit"></Button>
        <Button label="+" operation @on-click="setOperation"></Button>
        <Button label="0" double @on-click="addDigit"></Button>
        <Button label="." @on-click="addDigit"></Button>
        <Button label="=" operation @on-click="setOperation"></Button>
    </div>
</template>

<script>
    import Button from '../components/Button'
    import Display from '../components/Display'

    export default {
        data: function() {
            return {
                displayValue: "0",
                clearDisplay: false,
                operation: null,
                values: [0, 0],
                currentIndex: 0
            }
        },
        components: { Button, Display },
        methods: {
            clearMemory() {
                Object.assign(this.$data, this.$options.data())
            },
            setOperation(operation) {

                if(this.currentIndex === 0) {
                    this.operation = operation
                    this.currentIndex = 1
                    this.clearDisplay = true
                } else {
                    const finish = operation === "="
                    const currentOperation = this.operation

                    try {
                        if(currentOperation === "+") {
                            this.values[0] = this.values[0] + this.values[1]
                        } else if (currentOperation === "-") {
                            this.values[0] = this.values[0] - this.values[1]
                        } else if (currentOperation === "/") {
                            this.values[0] = this.values[0] / this.values[1]
                        } else if (currentOperation === "*") {
                            this.values[0] = this.values[0] * this.values[1]
                        } else {
                            this.values[0] = this.values[0]
                        }
                    } catch (error) {
                        this.$emit('onError', e)
                    }

                    this.values[1] = 0
                    this.displayValue = this.values[0]
                    this.operation = finish ? null : operation
                    this.currentIndex = finish ? 0 : 1
                    this.clearDisplay = !finish

                }

            },
            addDigit(digit) {
                
                if(digit === "." && this.displayValue.includes(".")) {
                    return
                }
                
                const clearDisplay = this.displayValue === "0" || this.clearDisplay
                const currentValue = clearDisplay ? "" : this.displayValue
                const displayValue = currentValue + digit
                
                this.displayValue = displayValue
                this.clearDisplay = false
                
                if(digit !== ".") {
                    const index = this.currentIndex
                    const newValue = parseFloat(displayValue)
                    this.values[index] = newValue
                }

            }    
        }
    }
</script>

<style>
    .calculator {
        height: 320px;
        width: 235px;
        border-radius: 5px;
        overflow: hidden;
        display: grid;
        grid-template-columns: repeat(4, 25%);
        grid-template-rows: 1fr 48px 48px 48px 48px 48px;
    }
</style>

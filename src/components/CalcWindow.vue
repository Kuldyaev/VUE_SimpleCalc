<template>
  <div class="conteiner">

    <div id='result'>
      <div id='smallNumber'>{{memoryDisplayed}}<span id="grey">{{operDisplayed}}</span></div>
      <div id='bigNumber'>{{minusDisplayed}}{{valueDisplayed}}</div>
    </div>
    <div id='name'>ЭЛЕКТРОНИКА NiXYR-17</div>
    <div class="btns">
    <div class="btn" v-for="btn in btns"  :key="btn.text" >
      <div class="btn-container" v-if="btn.type === 'action'" @click="compute(btn.text)">{{btn.text}}</div>
      <div class="btn-container" v-else-if="btn.type === 'reset'" @click="reset()" style="backgroundColor: #FBBBBB">{{btn.text}}</div>
      <div class="btn-container" v-else-if="btn.type === 'delete'" @click="deleteLastSymbol()"
      style="backgroundColor: #FBBBBB">{{btn.text}}</div>
      <div class="btn-container" v-else @click="handleDigit(btn.text)">{{btn.text}}</div>
    </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CalcWindow',
  data: function () {
    return {
      result: '',
      memory: 0,
      operation: ['+', '-', '*', '/'], // Сумма,разность,произведение,деление
      currentOperation: '',
      minus: false,
      btns: [
        { text: 'AC', type: 'reset' },
        { text: 'C', type: 'delete' },
        { text: 'SQR', type: 'action' },
        { text: '/', type: 'action' },
        { text: '7', type: 'number' },
        { text: '8', type: 'number' },
        { text: '9', type: 'number' },
        { text: '*', type: 'action' },
        { text: '4', type: 'number' },
        { text: '5', type: 'number' },
        { text: '6', type: 'number' },
        { text: '-', type: 'action' },
        { text: '1', type: 'number' },
        { text: '2', type: 'number' },
        { text: '3', type: 'number' },
        { text: '+', type: 'action' },
        { text: '+/-', type: 'action' },
        { text: '0', type: 'number' },
        { text: ',', type: 'action' },
        { text: '=', type: 'action' }
      ]
    }
  },
  computed: {
    valueDisplayed () {
      if (this.result === '') {
        return 0
      } else { return this.result }
    },
    minusDisplayed () {
      if (this.minus) {
        return '-'
      } else { return '' }
    },
    operDisplayed () {
      if (this.memory === 0) {
        return ''
      } else { return this.currentOperation }
    },
    memoryDisplayed () {
      if (this.memory === 0) {
        return ''
      } else { return this.memory }
    }
  },
  methods: {
    compute (x) {
      if (this.result.length < 21) {
        switch (x) {
          case ',':
            if ((this.result.length < 19) && (this.result.indexOf('.') === -1)) {
              this.result = this.result + '.'
            }
            break
          case '+':
            if (this.memory === 0) {
              this.memorize()
              this.clear()
            } else {
              this.execute(this.currentOperation)
            }
            this.currentOperation = this.operation[0]
            break
          case '-':
            if (this.memory === 0) {
              this.memorize()
              this.clear()
            } else {
              this.execute(this.currentOperation)
            }
            this.currentOperation = this.operation[1]
            break
          case '*':
            if (this.memory === 0) {
              this.memorize()
              this.clear()
            } else {
              this.execute(this.currentOperation)
            }
            this.currentOperation = this.operation[2]
            break
          case '/':
            if (this.memory === 0) {
              this.memorize()
              this.clear()
            } else {
              this.execute(this.currentOperation)
            }
            this.currentOperation = this.operation[3]
            break
          case '=':
            this.execute(this.currentOperation)
            this.currentOperation = ''
            this.result = String(this.memory)
            this.memory = 0
            break
          case '+/-':
            this.minus = !this.minus
            break
          case 'SQR':
            if (!this.minus) {
              this.result = String(Math.sqrt(+this.result))
            } else {
              this.minus = false
              this.result = 'Error'
            }
            break
          default:
            console.log(x)
        }
      }
    },
    handleDigit (x) {
      if (this.result.length < 21) {
        this.result = this.result + x
      }
    },
    reset () {
      this.clear()
      this.memory = 0
      this.currentOperation = ''
    },
    deleteLastSymbol () {
      if (this.result === 'Error') {
        this.result = ''
      } else {
        if (this.minus && this.result.length === 0) {
          this.minus = false
        } else {
          this.result = this.result.slice(0, -1)
        }
      }
    },
    memorize () {
      let m = 1
      if (this.minus) { m = -1 } else { m = 1 }
      this.memory = +this.result * m
    },
    execute (x) {
      let m = 1
      if (this.minus) { m = -1 } else { m = 1 }
      switch (x) {
        case '+':
          this.memory = this.memory + +this.result * m
          break
        case '-':
          this.memory = this.memory - +this.result * m
          break
        case '*':
          this.memory = this.memory * +this.result * m
          break
        case '/':
          this.memory = this.memory / +this.result * m
          break
        default:
          console.log(x)
      }
      this.clear()
    },
    clear () {
      this.result = ''
      this.minus = false
    },
    keyPress (e) {
      switch (e.key) {
        case '0':
        case '1':
        case '2':
        case '3':
        case '4':
        case '5':
        case '6':
        case '7':
        case '8':
        case '9':
          this.handleDigit(e.key)
          break
        case '+':
        case '-':
        case '*':
        case '/':
          this.compute(String(e.key))
          break
        case '.':
        case ',':
          this.compute(',')
          break
        case 'Backspace':
          this.deleteLastSymbol()
          break
        case 'Enter':
          this.compute('=')
          break
        case 'Delete':
          this.reset()
          break
        default:
          console.log(e.key)
          break
      }
    }
  },
  mounted () {
    this.$nextTick(() => {
      addEventListener('keydown', this.keyPress)
    })
  }
}
</script>

<style scoped>
.conteiner {
  max-width: 750px;
  max-height: 100%;
  margin: 0 auto;
}
#result{
  margin: 15px auto 0px auto;
  background-color: black;
  color:white;
  padding: 5px 15px;
  min-height: 100px;
  display: flex;
  flex-direction: column;
}
#bigNumber{
  font-size: 60px;
  display: flex;
  justify-content: end;
  align-items: center;
}
#smallNumber{
  font-size: 15px;
  display: flex;
  justify-content: end;
  align-items: center;
  margin-bottom: 5px;
}
#grey{
  color: grey;
}
#name{
  background-color: blue;
  color: silver;
  display: flex;
  justify-content: end;
  align-items: center;
  padding: 3px 10px 3px 0px;
}
.btns{
  display:flex;
  flex-wrap: wrap;
  justify-content: space-between;
  max-width: 746px;
  height: 100%;
  border: 2px solid black;

}
.btn{
  width: 21%;
  max-height: 100px;
  background-color: #F2F2F2;
  padding: 1%;
  border: 3px solid #EBEAEA;
  border-radius: 5px;
  margin: 1px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 60px;
}
.btn-container{
  width: 100%;
  height: 100%;
}
.btn:hover {
  font-size: 62px;
  background-color: #EBEAEA;
}
@media screen and (max-width: 600px) and (min-width: 376px) {
  .btn{
    font-size: 40px;
    padding: 4px;
  }
}
@media screen and (max-width: 408px)  {
  .btn{
    font-size: 30px;
    padding: 3px;
  }
}
</style>

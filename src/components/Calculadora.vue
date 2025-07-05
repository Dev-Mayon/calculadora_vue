<template>
  <div :class="[isDarkMode ? 'bg-dark text-light' : 'bg-externo']" style="min-height: 100vh;">
    <div class="container py-5">
      <transition name="fade-slide">
        <div
          v-show="mounted"
          class="mx-auto p-4 rounded shadow"
          style="max-width: 400px;"
          :class="isDarkMode ? 'bg-secondary text-light' : 'bg-calculadora text-dark'"
        >
          <h2 class="text-center mb-4 fw-bold">Calculadora</h2>

          <input type="number" inputmode="numeric" v-model.number="num1" class="form-control mb-3" placeholder="Digite o primeiro número" />
          <input type="number" inputmode="numeric" v-model.number="num2" class="form-control mb-3" placeholder="Digite o segundo número" />

          <select v-model="operacao" class="form-select mb-3 w-50 mx-auto" :disabled="camposVazios">
            <option disabled value="">Escolha</option>
            <option value="+">Somar</option>
            <option value="-">Subtrair</option>
            <option value="*">Multiplicar</option>
            <option value="/">Dividir</option>
          </select>

          <p class="text-center fw-semibold">Resultado: {{ mensagemResultado }}</p>

          <div v-if="historico.length" class="mt-4">
            <h5>Histórico:</h5>
            <transition-group name="fade" tag="ul" class="list-group mb-3">
              <li v-for="(item, index) in historico" :key="item + index" class="list-group-item" :class="isDarkMode ? 'bg-dark text-light' : ''">
                {{ item }}
              </li>
            </transition-group>

            <button @click="limparHistorico" class="btn btn-danger w-100" :disabled="historico.length === 0">Limpar Histórico</button>
            <button @click="novoCalculo" class="btn btn-secondary w-100 mt-2" :disabled="camposVazios && !operacao">Novo Cálculo</button>
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      num1: null,
      num2: null,
      operacao: '',
      historico: [],
      isDarkMode: false,
      mounted: false,
    };
  },
  computed: {
    camposVazios() {
      return this.num1 === null || this.num2 === null;
    },
    mensagemResultado() {
      if (this.camposVazios || !this.operacao) return '';
      if (this.operacao === '/' && this.num2 === 0) return 'Divisão por zero!';

      const resultado = this.calcular(this.num1, this.num2, this.operacao);
      const expressao = `${this.num1} ${this.operacao} ${this.num2} = ${resultado}`;
      if (!this.historico.includes(expressao)) {
        this.historico.push(expressao);
      }
      return resultado;
    },
  },
  methods: {
    calcular(a, b, op) {
      switch (op) {
        case '+': return a + b;
        case '-': return a - b;
        case '*': return a * b;
        case '/': return b !== 0 ? a / b : 'Erro';
        default: return '';
      }
    },
    limparHistorico() {
  this.historico.splice(0); // mais reativo que this.historico = []
},
    novoCalculo() {
      this.num1 = null;
      this.num2 = null;
      this.operacao = '';
    },
  },
  mounted() {
    this.mounted = true;
  },
};
</script>
<style scoped>
.fade-slide-enter-active {
  transition: all 0.5s ease;
}
.fade-slide-enter-from {
  opacity: 0;
  transform: translateY(20px);
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.4s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>


# 📟 Calculadora Aritmética com Vue.js

Uma calculadora simples e interativa desenvolvida em **Vue.js 3**, com suporte a:

- 🧮 Operações básicas: soma, subtração, multiplicação e divisão  
- 📜 Histórico de cálculos com animação suave  
- 🌙 Suporte a tema escuro (modo dark)  
- ✅ Validações (ex: divisão por zero, campos vazios)  
- 💡 Estilo moderno com Bootstrap 5  
- 🎬 Animação de entrada suave na calculadora  

---

## 🚀 Tecnologias utilizadas

- [Vue.js 3 (Vite)](https://vitejs.dev/)
- [Bootstrap 5](https://getbootstrap.com/)
- HTML5 + CSS3


---

## ⚙️ Funcionalidades

- Interface intuitiva e responsiva
- Seleção de operação aritmética via `<select>`
- Histórico animado com `<transition-group>`
- Botão "Limpar Histórico"
- Botão "Novo Cálculo"
- Estilos alternados para tema claro e escuro com `v-bind:class`
- Animação de entrada do card com `transition name="fade-slide"`

---

## 📁 Estrutura do Projeto

src/
├── components/
│ └── Calculadora.vue # Componente principal
├── assets/
│ └── global.css # Estilos globais personalizados
├── App.vue
└── main.js



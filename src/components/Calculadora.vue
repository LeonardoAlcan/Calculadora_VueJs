<template>
    <div :class="['app-wrapper', themeClass]">
        <button class="theme-toggle" @click="alternarTema">
            Alternar para {{ darkMode ? 'Claro' : 'Escuro' }}
        </button>

        <transition name="fade">
            <div v-if="mostrarCalculadora" class="calculadora">
                <div class="calculator">
                    <h1>Calculadora Aritmética</h1>

                    <div class="inputs">
                        <input type="number" v-model.number="numero1" placeholder="Número 1">
                        <select v-model="operacao">
                            <option value="+">+</option>
                            <option value="-">-</option>
                            <option value="*">*</option>
                            <option value="/">/</option>
                        </select>
                        <input type="number" v-model.number="numero2" placeholder="Número 2">
                    </div>

                    <div class="resultado">
                        <h2>Resultado: {{ resultado }}</h2>
                    </div>
                </div>
            </div>
        </transition>
    </div>
</template>

<script>
export default {
    name: 'Calculadora',
    data() {
        return {
            numero1: 0,
            numero2: 0,
            operacao: '+',
            darkMode: false,
            mostrarCalculadora: true,
        };
    },
    computed: {
        resultado() {
            const n1 = this.numero1;
            const n2 = this.numero2;
            switch (this.operacao) {
                case '+':
                    return n1 + n2;
                case '-':
                    return n1 - n2;
                case '*':
                    return n1 * n2;
                case '/':
                    return n2 !== 0 ? (n1 / n2).toFixed(2) : 'Erro: divisão por zero';
                default:
                    return 0;
            }
        },
        themeClass() {
            return this.darkMode ? 'dark' : 'light';
        },
    },
    methods: {
        alternarTema() {
            this.darkMode = !this.darkMode;
        },
    },
};
</script>

<style scoped>
/* Estilo base */
.app-wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 2rem;
    min-height: 100vh;
    transition: background-color 0.3s ease, color 0.3s ease;
    font-family: 'Segoe UI', sans-serif;
}

/* Botão de alternância de tema */
.theme-toggle {
    margin-bottom: 2rem;
    padding: 0.5rem 1rem;
    font-weight: bold;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    background-color: #4CAF50;
    color: white;
    transition: background 0.3s;
}

.theme-toggle:hover {
    background-color: #45a049;
}

/* Container principal da calculadora */
.calculadora {
    width: 100%;
    max-width: 480px;
    padding: 2rem;
    border-radius: 12px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    background-color: var(--bg-card);
    color: var(--text-color);
    transition: all 0.3s ease-in-out;
}

/* Título */
.calculator h1 {
    text-align: center;
    margin-bottom: 1.5rem;
    font-size: 1.5rem;
}

/* Seção de inputs */
.inputs {
    display: flex;
    gap: 0.5rem;
    justify-content: center;
    margin-bottom: 1.5rem;
    flex-wrap: wrap;
}

.inputs input,
.inputs select {
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 8px;
    width: 100px;
    font-size: 1rem;
}

/* Resultado */
.resultado {
    text-align: center;
}

.resultado h2 {
    color: var(--accent-color);
}

/* Animação de transição */
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.5s;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}

/* Light Theme */
.light {
    --bg-card: #ffffff;
    --text-color: #222222;
    --accent-color: #2e7d32;
    background-color: #f0f0f0;
    color: #222222;
}

/* Dark Theme */
.dark {
    --bg-card: #1e1e1e;
    --text-color: #f0f0f0;
    --accent-color: #66bb6a;
    background-color: #121212;
    color: #f0f0f0;
}

/* Responsividade */
@media (max-width: 600px) {
    .inputs {
        flex-direction: column;
        align-items: center;
    }

    .inputs input,
    .inputs select {
        width: 100%;
        max-width: 280px;
    }
}
</style>
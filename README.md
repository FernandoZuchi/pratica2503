# 🏋️ Aula Prática: Buscador de Endereço via CEP (Duração: 1h30)

## ✨ Objetivo da Aula
Desenvolver uma aplicação web simples que consome uma API externa para buscar dados de endereço a partir de um CEP informado pelo usuário. A aula abordará conceitos de HTML, CSS, JavaScript e consumo de APIs.

---

## ⌛ Roteiro da Aula (1h30)

### ✅ 1. Apresentação do Projeto (10 min)

- Mostrar o projeto final funcionando (demonstração rápida):
  - Aluno digita o CEP, clica em "Buscar" e os dados aparecem.

- Explicação do que é uma **API**:
  - Interface de comunicação entre dois sistemas.
  - Exemplo: BrasilAPI fornece dados de CEP de forma gratuita.

---

### 📁 2. Estrutura HTML (15 min)

**Arquivo:** `index.html`

```html
<!DOCTYPE html>
<html lang="pt-br">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Buscador de Endereço</title>
    <link rel="stylesheet" href="./css/style.css" />
  </head>
  <body>
    <div id="app">
      <div class="container-form">
        <div class="logo">
          <img src="./assets/map.svg" alt="Ícone de mapa" />
          <h1>Buscar Endereço</h1>
        </div>
        <input type="text" placeholder="Digite o cep" />
        <button>Buscar</button>
      </div>
      <div class="result"></div>
    </div>
    <script src="./scripts/main.js"></script>
  </body>
</html>
```

**Explicação:**
- `div#app`: estrutura principal.
- `input` e `button`: para interação do usuário.
- `div.result`: onde os dados aparecerão.
- Script JS no final garante que o HTML já esteja carregado.

---

### 🎨 3. Estilo com CSS (20 min)

**Arquivo:** `css/style.css`

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  min-height: 100vh;
  background-color: #232323;
  color: #fff;
}

#app {
  display: flex;
  gap: 40px;
  max-width: 900px;
  width: 100%;
  margin: 20px auto;
}

img {
  width: 64px;
}

.container-form {
  background-color: #171717;
  width: 50%;
  border-radius: 20px;
  padding: 32px;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

input {
  padding: 12px;
  border-radius: 8px;
  background-color: #232323;
  border: none;
  outline: none;
  color: #fff;
}

button {
  padding: 12px;
  border-radius: 8px;
  background-color: #7fff00;
  border: none;
  color: #232233;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}

.result {
  flex: 1;
  background-color: #171717;
  padding: 20px;
  border-radius: 20px;
}

p {
  font-size: 20px;
  font-weight: 700;
  margin-top: 16px;
}
```

**Explicação:**
- Reset com `*` para padronizar.
- `Flexbox` para layout responsivo.
- Estilo moderno, escuro, com destaque no botão.
- Classes reutilizáveis.

---

### ⚖️ 4. Lógica com JavaScript (30 min)

**Arquivo:** `scripts/main.js`

```js
const input = document.querySelector('input')
const button = document.querySelector('button')
const result = document.querySelector('.result')

button.addEventListener('click', async () => {
  const cep = input.value.trim()

  if (cep === '') {
    alert('Digite um CEP válido.')
    return
  }

  const url = `https://brasilapi.com.br/api/cep/v2/${cep}`

  try {
    const response = await fetch(url)

    if (!response.ok) {
      throw new Error('CEP não encontrado')
    }

    const data = await response.json()

    result.innerHTML = `
      <p>CEP: ${data.cep}</p>
      <p>Rua: ${data.street}</p>
      <p>Cidade: ${data.city}</p>
      <p>Bairro: ${data.neighborhood}</p>
      <p>Estado: ${data.state}</p>
    `
  } catch (error) {
    result.innerHTML = `<p style="color:red">Erro: ${error.message}</p>`
  }

  input.value = ''
  input.focus()
})
```

**Explicação:**
- Selecionamos elementos do DOM.
- Criamos um evento de clique.
- Usamos `fetch` + `async/await` para consumir a API.
- Validamos CEP vazio e tratamos erros com `try...catch`.

---

### 📊 5. Testes e Melhorias (10 min)

- Testar CEPs reais (ex: 01001000).
- Testar CEPs errados para verificar o tratamento de erro.

**Sugestões de melhorias:**
- Adicionar loading (carregando...).
- Bloquear caracteres não numéricos no input.
- Criar mensagem "Digite um CEP" antes da busca.

---

## 🎓 Conteúdos Aprendidos
- Estrutura HTML de uma aplicação web.
- Estilização com CSS.
- Manipulação de eventos e DOM com JS.
- Consumo de APIs públicas com `fetch`.
- Tratamento de erros com `try...catch`.
- Experiência simulada de integração de dados externos.

---

## 💼 Valor de Mercado
- Saber consumir APIs é essencial em sistemas modernos.
- Trabalhar com JS assíncrono é prática comum em front-end.
- APIs são a base da comunicação entre front-end e back-end.

---

## 📅 Tarefa para Casa (Extra e Opcional)
- Adicionar barra de carregamento. (HTML + CSS)
- Criar versão responsiva para celular. (HTML + CSS)
- Validar CEP com Regex (ex: `/^\d{8}$/`). (HTML + CSS + JS)

---


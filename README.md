# Aula: Componentes Estáticos e Dinâmicos em React

## Objetivo da aula

Criar uma pequena página em React usando:

- Componentes estáticos
- Componentes dinâmicos com `props`
- Renderização de listas com `map`
- Personalização com Tailwind CSS

---

## 1. O que é um componente?

Em React, um componente é uma parte da interface que pode ser reutilizada.

Exemplo:

```jsx
function Titulo() {
  return <h1>Minha página em React</h1>;
}
```

Depois, usamos esse componente assim:

```jsx
<Titulo />
```

Pense no componente como uma peça de LEGO. Só que sem o risco de pisar descalço. Amém.

---

## 2. Criando o projeto com Vite

No terminal, rode:

```bash
npm create vite@latest aula-componentes
```

Escolha:

```txt
React
JavaScript
```

---

## 3. Configurando o Tailwind CSS

Instale o Tailwind:

```bash
npm install tailwindcss @tailwindcss/vite
```

No arquivo `vite.config.js`, deixe assim:

```js
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import tailwindcss from '@tailwindcss/vite'

export default defineConfig({
  plugins: [react(), tailwindcss()],
})
```

No arquivo `src/index.css`, coloque:

```css
@import "tailwindcss";
```

---

## 4. Estrutura da aula

Vamos criar uma página simples com:

```txt
src/
├── App.jsx
├── main.jsx
├── index.css
└── components/
    ├── Header.jsx
    ├── Footer.jsx
    ├── CardAluno.jsx
    └── ListaTecnologias.jsx
```

---

# Parte 1: Componentes Estáticos

## 5. Criando o componente Header

Crie a pasta `components` dentro de `src`.

Depois, crie o arquivo:

```txt
src/components/Header.jsx
```

Código:

```jsx
function Header() {
  return (
    <header className="bg-blue-600 text-white p-6 rounded-xl text-center">
      <h1 className="text-3xl font-bold">Aula de React</h1>
      <p className="mt-2">Criando componentes estáticos e dinâmicos</p>
    </header>
  );
}

export default Header;
```

Esse componente é estático porque sempre mostra o mesmo conteúdo.

---

## 6. Criando o componente Footer

Crie o arquivo:

```txt
src/components/Footer.jsx
```

Código:

```jsx
function Footer() {
  return (
    <footer className="bg-gray-800 text-white p-4 rounded-xl text-center mt-6">
      <p>Desenvolvido na aula de React</p>
    </footer>
  );
}

export default Footer;
```

Também é estático, pois não recebe dados de fora.

---

# Parte 2: Componentes Dinâmicos

## 7. O que são props?

`props` são informações que um componente recebe de outro componente.

Na prática, elas funcionam como parâmetros de uma função.

Observe este exemplo:

```js
<CardAluno nome="Ana" curso="Front-end" idade={20} />
```

Nesse código, o componente `CardAluno` recebe três informações:

```bash
nome
curso
idade
```

Essas informações são chamadas de `props`.

Dentro do componente, podemos receber essas `props` assim:

```js
function CardAluno({ nome, curso, idade }) {
  return (
    <div>
      <h2>{nome}</h2>
      <p>{curso}</p>
      <p>{idade}</p>
    </div>
  );
}
```

Agora o React substitui cada valor:

```bash
{nome}  vira Ana
{curso} vira Front-end
{idade} vira 20
```

### Por que usar props?

Porque elas deixam o componente reutilizável.

Sem props, teríamos que criar vários componentes parecidos:

```js
function CardAna() {
  return <h2>Ana</h2>;
}

function CardCarlos() {
  return <h2>Carlos</h2>;
}
```

Isso é repetição. E repetição em código é igual cadeira rangendo: no começo você ignora, depois enlouquece.

Com props, criamos apenas um componente:

```js
function CardAluno({ nome }) {
  return <h2>{nome}</h2>;
}
```

E usamos várias vezes, mudando apenas os dados:

```js
<CardAluno nome="Ana" />
<CardAluno nome="Carlos" />
<CardAluno nome="Mariana" />
```

O componente é o mesmo.

Os dados mudam.

## 8. Componente dinâmico com props

Agora vamos criar um componente que muda de acordo com os dados recebidos.

Crie o arquivo:

```txt
src/components/CardAluno.jsx
```

Código:

```jsx
function CardAluno({ nome, curso, idade }) {
  return (
    <div className="bg-white shadow-md rounded-xl p-5 border border-gray-200">
      <h2 className="text-xl font-bold text-blue-600">{nome}</h2>
      <p className="text-gray-700">Curso: {curso}</p>
      <p className="text-gray-700">Idade: {idade} anos</p>
    </div>
  );
}

export default CardAluno;
```

Aqui usamos `props`.

As propriedades são:

```jsx
nome
curso
idade
```

Ou seja, o componente muda de acordo com os valores enviados.

---

## 9. Componente dinâmico com lista

Agora vamos criar um componente que recebe uma lista e mostra os itens na tela.

Crie o arquivo:

```txt
src/components/ListaTecnologias.jsx
```

Código:

```jsx
function ListaTecnologias({ tecnologias }) {
  return (
    <section className="bg-gray-100 p-5 rounded-xl">
      <h2 className="text-2xl font-bold mb-4">Tecnologias estudadas</h2>

      <ul className="space-y-2">
        {tecnologias.map((tecnologia, index) => (
          <li
            key={index}
            className="bg-white p-3 rounded-lg shadow-sm border border-gray-200"
          >
            {tecnologia}
          </li>
        ))}
      </ul>
    </section>
  );
}

export default ListaTecnologias;
```

Esse componente é dinâmico porque depende da lista enviada pelo `App.jsx`.

---

# Parte 3: Montando a página

## 10. Usando os componentes no App.jsx

Abra o arquivo:

```txt
src/App.jsx
```

Apague tudo e coloque:

```jsx
import Header from "./components/Header";
import Footer from "./components/Footer";
import CardAluno from "./components/CardAluno";
import ListaTecnologias from "./components/ListaTecnologias";

function App() {
  const tecnologias = ["HTML", "CSS", "JavaScript", "React"];

  return (
    <main className="min-h-screen bg-gray-200 p-6">
      <div className="max-w-3xl mx-auto space-y-6">
        <Header />

        <section className="grid gap-4 md:grid-cols-2">
          <CardAluno nome="Ana" curso="Front-end" idade={20} />
          <CardAluno nome="Carlos" curso="React" idade={22} />
        </section>

        <ListaTecnologias tecnologias={tecnologias} />

        <Footer />
      </div>
    </main>
  );
}

export default App;
```

---

# Resultado esperado

A página terá:

- Um cabeçalho fixo
- Dois cards de alunos usando o mesmo componente
- Uma lista de tecnologias
- Um rodapé fixo
- Estilização com Tailwind CSS

---

# Explicação rápida

## Componentes estáticos

São componentes que mostram sempre o mesmo conteúdo.

Exemplo:

```jsx
<Header />
<Footer />
```

Eles não recebem dados externos.

---

## Componentes dinâmicos

São componentes que mudam de acordo com os dados recebidos.

Exemplo:

```jsx
<CardAluno nome="Ana" curso="Front-end" idade={20} />
```

O componente `CardAluno` recebe informações e exibe valores diferentes.

---

## Renderização de lista

Usamos `map` para percorrer um array e exibir seus itens:

```jsx
{tecnologias.map((tecnologia, index) => (
  <li key={index}>{tecnologia}</li>
))}
```

O `key` ajuda o React a identificar cada item da lista.

---

# Atividade prática

Crie mais um aluno no `App.jsx`.

Exemplo:

```jsx
<CardAluno nome="Mariana" curso="JavaScript" idade={19} />
```

Depois, adicione mais duas tecnologias na lista:

```jsx
const tecnologias = ["HTML", "CSS", "JavaScript", "React", "Node.js", "Vite"];
```

---

# Desafio pequeno

Crie um novo componente chamado `Mensagem.jsx`.

Ele deve receber uma propriedade chamada `texto`.

Exemplo de uso:

```jsx
<Mensagem texto="React trabalha com componentes reutilizáveis." />
```

Exemplo de componente:

```jsx
function Mensagem({ texto }) {
  return (
    <div className="bg-yellow-100 border border-yellow-300 p-4 rounded-xl">
      <p>{texto}</p>
    </div>
  );
}

export default Mensagem;
```

Depois, importe e use esse componente no `App.jsx`.

---

# Fechamento

Nesta aula, você criou:

- Componentes estáticos
- Componentes dinâmicos com props
- Um componente que renderiza lista
- Uma interface simples com Tailwind CSS

React começa pequeno mesmo. Depois vira projeto com 48 pastas, 12 contextos e um botão que ninguém sabe quem fez. Normal.

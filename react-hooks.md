## React Hooks - Explicado a Fundo

- Versão React Hooks => 16.8.0
- Só funciona em componentes do tipo função (Functional Components)
- Import direto the react

### `useState`

- Usagem basica 
    - `const [state, setState] = useState(defaultState)`  
    `state` - Guarda o state.  
    `setState` - Atualiza o state.  
    `defaultState` - Valor default do state.      
    - Adicionar o `setState` em um `onClick` de um `button` e mostrar dando update ao clickar no botão.  
    - Adicionar o `setState` em um `onClick` de um `input` e mostrar dando update ao digitar no input.
    - Fazer um update em um objeto, usando multiplos `input`s.
- Casos a normais
    - `const stateArray = useState(someValue)`
    - `const state = useState(someValue)[0]`
    - `const setState = useState(someValue)[1]`
- Valor default a fundo
- Usando o state anteriora fundo

### `useEffect`

- Usagem basica
- Array de dependência
- Efeito de clean up 
- Primeiro Render


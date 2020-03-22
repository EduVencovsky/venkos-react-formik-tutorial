# React Hooks - Explicado a Fundo

- Versão React Hooks => 16.8.0
- Só funciona em componentes do tipo função (Functional Components)
- Import direto the react

## `useState`

#### Usagem basica 

`const [state, setState] = useState(defaultState)` 

Onde:

- `state` - Guarda o state.  
- `setState` - Atualiza o state e rederiza o componente.  
- `defaultState` - Valor default do state.    

Exemplos:

- Utilizando o state com um input
    ```javascript
    function App() {
        const [x, setX] = useState('')

        return (
            <div>
                <p>
                    {x}
                </p>
                <input value={x} onChange={e => setX(e.target.value)} />
            </div>
        )
    }
    ```

- Utilizando o com um button
    ```javascript
    function App() {
        const [x, setX] = useState(0)

        return (
            <div>
            <p>
                {x}
            </p>
            <button onClick={() => setX(x + 1)}>Incremet</button>
            </div>
        )
    }

    ```


- Utilizando o state como objeto
    ```javascript
    function App() {
        const [x, setX] = useState({ count: 0, name: '' })

        return (
            <div>
                <p>
                    {x.count}
                </p>
                <p>
                    {x.name}
                </p>
                <input value={x.name} onChange={e => setX({ count: x.count + 1, name: e.target.value })} />
            </div>
        )
    }
    ```

#### Casos a normais

  Em alguns casos, o `useState` não é usado da maneira "convencional".
  ```javascript
  const anyValue = 0

  function App() {
    const [x, setX] = useState()

    const stateArray = useState(anyValue)
    const state = useState(anyValue)[0]
    const setState = useState(anyValue)[1]

    console.log(stateArray)
    console.log(state)
    console.log(setState)
    
    return (
      <div>
        {x}
        <button onClick={() => setX(x + "a")}>
          Click
        </button>
      </div>
    )
  }
  ```


#### Valor default

- Valor default é settado apenas uma vez.

  Ao passar um state como valor default de outro state, o valor do state será afetado apenas no primeiro render do componente.
  ```javascript
  function App() {
      const [count1, setCount1] = useState(0)
      const [count2, setCount2] = useState(count1)

      return (
          <div>
              <p>
                  {count1}
              </p>
              <button onClick={() => setCount1(count1 + 1)}>
                  Count 1
              </button>
              <p>
                  {count2}
              </p>
              <button onClick={() => setCount2(count2 + 1)}>
                  Count 2
              </button>
          </div>
      )
  }
  ```

- Passando uma função como valor default.    

  Se for necessário chamar uma função para retornar o valor default do `useState`, é possivel passar uma funcão que retornar o valor dessa função para evitar processamentos desnecessários. 
  ```javascript
  const getInitialValue = number => {
    console.log('getInitialValue' + number)
    return number % 2
  }

  function App() {
    const [count1, setCount1] = useState(getInitialValue(1))
    const [count2, setCount2] = useState(() => getInitialValue(2))

    return (
      <div>
        <p>
          {count1}
        </p>
        <button onClick={() => setCount1(count1 + 1)}>
          Increment
        </button>
        <p>
          {count2}
        </p>
        <button onClick={() => setCount2(count2 + 1)}>
          Increment
        </button>
      </div>
    )
  }
  ```

#### Usando o state anterior no setState

- Passando uma função para setState

  É possivél passar uma função para o setState, onde o primeiro parametro dessa função recebe o valor anterior do state. 

  ```javascript
  function App() {
    const [x, setX] = useState(0)
    
    return (
      <div>
        <p>
          {x}
        </p>
        <button onClick={() => setX(prev => prev + 1)}>
          Click
        </button>
      </div>
    )
  }
  ```

- Quando usar o state anterior?

  Em alguns casos, é necessário usar o state anterior para evitar comportamentos indesejados.

  ```javascript
  const condition = true

  function App() {
    const [count1, setCount1] = useState(0)
    const [count2, setCount2] = useState(0)

    const handleClick1 = () => {
      setCount1(count1 + 1)
      if(condition){
        setCount1(count1 + 1)
      }
    }

    const handleClick2 = () => {
      setCount2(prev => prev + 1)
      if(condition){
        setCount2(prev => prev + 1)
      }
    }

    return (
      <div>
        <p>
          {count1}
        </p>
        <button onClick={handleClick1}>
          Increment 1
        </button>
        <p>
          {count2}
        </p>
        <button onClick={handleClick2}>
          Increment 2
        </button>
      </div>
    )
  }
  ```

## `useEffect`

- Usagem basica
- Array de dependência
- Efeito de clean up 
- Primeiro Render


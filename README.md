# O que são Styled Components?

- Styled Components é uma solução de estilo `CSS-in-JS` para o React.js.
- Ele usa `tagged template literals` que permitem escrever `CSS simples` com `escopo para um único componente`.

# Recursos/Benefícios

- Automatic critical CSS.
- A biblioteca automaticamente acompanha quais componentes são renderizados na tela e injeta apenas os estilos.
- Sem class name bugs.
- A biblioteca gera nomes de classes únicos para cada estilo.
- Easier deletions of CSS: com a biblioteca, cada estilo é ligado ao componente.
- Dynamic styling.
- Painless maintance.
- Automatic vendor prefixing.

# Como criar um Styled Component?

Basta instalar a `biblioteca styled-components` na aplicação e, no arquivo onde ele será criado, importar styled da biblioteca. Em seguida, basta criar uma variável e atribuir a ela:

```
styled.tag`estilo`
```

```
import styled from "styled-components";

export const StyledButton = styled.button`
  border: 2px solid #4caf50;
  background-color: #4caf50;
  color: #fff;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  cursor: pointer;
  transition: 0.5s all ease-out;
`;
```

# Props

Assim como no React.js, é possível passar props, que são `atributos read-only`, para os componentes utilizando `${ }` da seguinte forma:

No arquivo .jsx:
```
<StyledButton variant="outline">Styled Button</StyledButton>
```

No arquivo com o styled component:
```
background-color: ${(props) => props.variant === "outline" ? "#fff" : "#4caf50"};
color: ${(props) => (props.variant === "outline" ? 
```

# Herdar estilos

É possível fazer um styled component `herdar` os estilos de outro componente utilizando `styled(component)` da seguinte forma:

```
export const FancyButton = styled(StyledButton)`
  background-image: linear-gradient(to right, #f6d365 0%, #fda085 100%);
  border: none;
`;
```

# Pseudo-classes

É possível utilizar pseudo-classes adicionando um `&:hover {}`, por exemplo, dentro do `template literal` do styled component:

```
export const StyledButton = styled.button`
  &:hover {
    background-color: ${(props) =>
      props.variant !== "outline" ? "#fff" : "#4caf50"};
    color: ${(props) => (props.variant !== "outline" ? "#4caf50" : "#fff")};
  }
`;
```

# Definir o component como sendo uma âncora (\<a\>)

É possível transformar o botão `Fancy Button` em um \<a\> da seguinte forma:

```
<FancyButton as="a">Fancy Button</FancyButton>
```

# Passar props para ser um atributo

É possível definir o `type` do component passando uma `prop` para ele. Neste caso, é necessário utilizando o `método .attrs` da seguinte forma:

```
export const SubmitButton = styled(StyledButton).attrs((props) => ({
  type: "submit",
}))``;
```

# Adicionar animações (@keyframes)

Para adicionar animações, basta importar o `keyframes` da biblioteca styled-components e utilizar ele com `template literal`:

```
import { keyframes } from "styled-components";

const rotate = keyframes`
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(360deg);
    }
`;
```

# ThemeProvider

Com a biblioteca styled components, é possível criar um `tema` que será aplicado na `aplicação inteira`, basta `importar` o `ThemeProvider`, adicionar o `atributo theme` e `encapsular` toda a aplicação dentro dele da seguinte forma:

```
import { ThemeProvider } from "styled-components";

const theme = {
  dark: {
    primary: "#000",
    text: "#fff"
  },
  light: {
    primary: "#fff",
    text: "#000"
  }
}

function App() {
  return (
    <ThemeProvider theme={theme}>
      <>
        <StyledButton>Styled Button</StyledButton>
      </>
    </ThemeProvider>
  )
}
```

# Global Styles

Para adicionar `estilos globais`, basta importar a `função createGlobalStyle` da biblioteca styled-components e utlizar `template literal` da seguinte forma:

```
import { createGlobalStyle } from "styled-components";

const GlobalStyle = createGlobalStyle`
  button {
    font-family: ${props => props.theme.fontFamily};
  }
`;
```

Após a criação do estilo global, basta adicionar ele como `children` do `ThemeProvider` da seguinte forma:

```
function App() {
  return (
    <ThemeProvider theme={theme}>
      <GlobalStyle/>
      <>
        <StyledButton>Styled Button</StyledButton>
      </>
    </ThemeProvider>
  )
}
```
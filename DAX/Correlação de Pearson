# Medidas DAX – Correlação de Pearson

Este documento apresenta as medidas DAX utilizadas para o cálculo dinâmico do coeficiente de correlação de Pearson no Power BI. As medidas permitem calcular automaticamente a correlação entre dois atributos selecionados pelo usuário, utilizando uma tabela virtual construída a partir da base integrada.

---

## Nº Atributos

Conta a quantidade de observações (anos) consideradas no cálculo da correlação.

```DAX
Nº Atributos =
DISTINCTCOUNT('Tabela Unificada'[ANO])
```

---

## X

Calcula o somatório dos valores do atributo selecionado para o eixo **X**.

```DAX
X =
VAR vX = SELECTEDVALUE('Atributos 2'[Atributo])
VAR vY = SELECTEDVALUE('Atributos 1'[Atributo])

VAR Virtual =
SUMMARIZE(
    'Tabela Unificada (2)',
    'Tabela Unificada (2)'[ANO],
    "X", CALCULATE(
        MAX('Tabela Unificada (2)'[Valor]),
        'Tabela Unificada (2)'[Atributo] = vX
    ),
    "Y", CALCULATE(
        MAX('Tabela Unificada (2)'[Valor]),
        'Tabela Unificada (2)'[Atributo] = vY
    )
)

RETURN
SUMX(
    Virtual,
    [X]
)
```

---

## Y

Calcula o somatório dos valores do atributo selecionado para o eixo **Y**.

```DAX
Y =
VAR vX = SELECTEDVALUE('Atributos 2'[Atributo])
VAR vY = SELECTEDVALUE('Atributos 1'[Atributo])

VAR Virtual =
SUMMARIZE(
    'Tabela Unificada (2)',
    'Tabela Unificada (2)'[ANO],
    "X", CALCULATE(
        MAX('Tabela Unificada (2)'[Valor]),
        'Tabela Unificada (2)'[Atributo] = vX
    ),
    "Y", CALCULATE(
        MAX('Tabela Unificada (2)'[Valor]),
        'Tabela Unificada (2)'[Atributo] = vY
    )
)

RETURN
SUMX(
    Virtual,
    [Y]
)
```

---

## X²

Calcula o somatório dos quadrados dos valores do atributo **X**.

```DAX
X² =
VAR vX = SELECTEDVALUE('Atributos 2'[Atributo])
VAR vY = SELECTEDVALUE('Atributos 1'[Atributo])

VAR Virtual =
SUMMARIZE(
    'Tabela Unificada (2)',
    'Tabela Unificada (2)'[ANO],
    "X", CALCULATE(
        MAX('Tabela Unificada (2)'[Valor]),
        'Tabela Unificada (2)'[Atributo] = vX
    ),
    "Y", CALCULATE(
        MAX('Tabela Unificada (2)'[Valor]),
        'Tabela Unificada (2)'[Atributo] = vY
    )
)

RETURN
SUMX(
    Virtual,
    [X] * [X]
)
```

---

## Y²

Calcula o somatório dos quadrados dos valores do atributo **Y**.

```DAX
Y² =
VAR vX = SELECTEDVALUE('Atributos 2'[Atributo])
VAR vY = SELECTEDVALUE('Atributos 1'[Atributo])

VAR Virtual =
SUMMARIZE(
    'Tabela Unificada (2)',
    'Tabela Unificada (2)'[ANO],
    "X", CALCULATE(
        MAX('Tabela Unificada (2)'[Valor]),
        'Tabela Unificada (2)'[Atributo] = vX
    ),
    "Y", CALCULATE(
        MAX('Tabela Unificada (2)'[Valor]),
        'Tabela Unificada (2)'[Atributo] = vY
    )
)

RETURN
SUMX(
    Virtual,
    [Y] * [Y]
)
```

---

## XY

Calcula o somatório do produto entre os valores correspondentes dos atributos **X** e **Y**.

```DAX
XY =
VAR vX = SELECTEDVALUE('Atributos 2'[Atributo])
VAR vY = SELECTEDVALUE('Atributos 1'[Atributo])

VAR Virtual =
SUMMARIZE(
    'Tabela Unificada (2)',
    'Tabela Unificada (2)'[ANO],
    "X", CALCULATE(
        MAX('Tabela Unificada (2)'[Valor]),
        'Tabela Unificada (2)'[Atributo] = vX
    ),
    "Y", CALCULATE(
        MAX('Tabela Unificada (2)'[Valor]),
        'Tabela Unificada (2)'[Atributo] = vY
    )
)

RETURN
SUMX(
    Virtual,
    [X] * [Y]
)
```

---

## Coeficiente Correlação

Aplica a fórmula do coeficiente de correlação linear de Pearson utilizando as medidas auxiliares calculadas anteriormente.

```DAX
Coeficiente Correlação =
DIVIDE(
    [Nº Atributos] * [XY] - [X] * [Y],
    SQRT(
        ([Nº Atributos] * [X²] - [X]^2) *
        ([Nº Atributos] * [Y²] - [Y]^2)
    )
)
```

---

## Funcionamento

As medidas **X**, **Y**, **X²**, **Y²** e **XY** são calculadas a partir de uma tabela virtual construída com `SUMMARIZE`, agrupando os dados por ano e recuperando os valores dos dois atributos selecionados pelos segmentadores do relatório.

Em seguida, essas medidas são utilizadas na implementação da fórmula do coeficiente de Pearson, permitindo que a correlação seja recalculada dinamicamente conforme o usuário altera os atributos analisados. Dessa forma, a matriz de correlação do dashboard torna-se totalmente interativa, possibilitando explorar diferentes combinações de variáveis sem a necessidade de criar medidas específicas para cada par de atributos.

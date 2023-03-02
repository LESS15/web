---
title: "Variáveis"
description: Um guia Pawn para iniciantes sobre variáveis
---

## Variáveis

Um dos conceitos mais importantes na programação é o conceito de 'variáveis'. Na programação, uma variável é uma entidade que é mutável, mas em termos de que ? Na linguagem Pawn, uma variável detém um 'valor' a qualquer momento e esse valor - como o nome sugere - é 'variável' ou 'mudável'.
A razão pela qual as variáveis são tão importantes é porque são basicamente pequenas unidades de memória de computador que podem manter ou 'lembrar' valores diferentes enquanto o programa está em execução (em execução), e essa propriedade se revela muito útil na programação. Por exemplo, você quer acompanhar a pontuação de 100 jogadores em um jogo, você pode fazê-lo facilmente programando o computador para armazenar (lembrar) e atualizar esses valores. Mais tarde, se você quiser encontrar a pontuação média desses jogadores ou quiser criar um quadro de líderes, esses valores das variáveis podem ser facilmente acessados e utilizados para esse fim.

### Declarando variáveis

A seguir está a sintaxe para a declaração de variáveis:
```c
// Criando (mais apropriadamente, 'declarando') uma variável chamada 'MinhaVariavel'

new MinhaVariavel;

// A palavra-chave `new` é usada para declarar uma variável
// Na linha acima é declarada uma variável com o nome 'MinhaVariavel'.
// O ponto e vírgula ; é usado no final para fechar a declaração.
```

The declaration syntax can be better understood by looking at some examples :

```c
new var;
new municao;
new pontuacao;
new veiculos;
new maiorespontuacoes;
```

Cada uma das variáveis definidas acima tem um valor por padrão, que é zero. Há diferentes maneiras de atribuir valores a uma variável. Um método é atribuir diretamente um valor à variável como ela é declarada:
```c
new letras = 25;
```

No exemplo acima, uma variável chamada 'letras' está sendo declarada, com um valor de 25. Você notará um sinal de igualdade que é um simples Operador de Atribuição que pode ser usado para atribuir valores a variáveis. Ele avalia a expressão à sua direita e atribui o valor resultante à variável referenciada no seu lado esquerdo. Além da atribuição de valores diretamente na declaração, você também pode fazê-lo em várias partes do seu código:
```c
new letras;

letras = 25;
```

### Escopos

A modificação do valor de uma variável só é possível se a parte do código onde você está referenciando a variável estiver dentro do escopo dessa variável. O escopo de uma variável depende do bloco de código ou da posição onde essa variável foi declarada. Por exemplo, uma variável sendo declarada fora de qualquer bloco de código, geralmente no início do script, tem um escopo 'Global' e pode ser acessada de qualquer lugar dentro do script:
```c
#include <a_samp>

new g_var = 5;

public OnFilterScriptInit()
{
    g_var = 10;
    
    printf("O valor agora é: %i", g_var); // Imprime no console o valor da variável 'g_var' que como definimos, é '10'
    return 1;
}

public OnPlayerConnect(playerid)
{
    g_var = 100;
    
    printf("O valor da variável agora é: %i", g_var); // Agora imprime no console a mesma variável só que com outro valor, que como definimos é '100'
    return 1;
}

// Saída do console:
// O valor é 10
// O valor é 100

// Nota: A primeira linha de saída é mostrada ao ligar o servidor. Enquanto a segunda linha de saída é mostrada somente quando um jogador se conecta no servidor.
```

Além das variáveis "globais" (escopadas), existem variáveis "locais" ou "privadas" que podem ser acessadas somente de dentro do bloco de código onde foram declaradas.
```c
#include <a_samp>

public OnFilterScriptInit ()
{
    new localVar;

    localVar = 5;

    return 1;
}

public OnPlayerConnect (playerid)
{
    localVar = 10; // Esta linha mostrará um erro na compilação por que a variável está fora de seu escopo que é a função "OnFilterScriptInit" que é chamada ao ligar o servidor.

    return 1;
}
```

Se você tentar compilar o código acima, o compilador mostrará um erro que é razoável, já que uma variável local está sendo referenciada em um bloco de código completamente diferente. Nota: Se for um bloco de código aninhado, então a variável pode ser acessada a partir daí.

Uma coisa importante a ser observada é que você não pode declarar variáveis com os mesmos nomes se seus escopos intercederem. Por exemplo, se você já tem uma variável chamada 'pontuacao' em um escopo global, você não pode criar outra variável chamada 'pontuacao' no escopo global, assim como uma variável local, e isto é verdade também para o contrário (se você já tem uma variável local, evite declarar uma variável global com o mesmo nome).
```c
#include <a_samp>

new g_score;

public OnFilterScriptInit ()
{
    new g_score = 5; // Essa linha mostrará um erro.
    return 1;
}
```

### Regras de nomenclatura

Agora que você sabe como declarar variáveis, você precisa conhecer as regras de nomenclatura para declarar variáveis que estão listadas abaixo:

- Todos os nomes de variáveis devem começar com uma letra ou um sublinhado (`_`)
- Após a primeira letra inicial, os nomes das variáveis podem conter letras e números, mas sem espaços ou caracteres especiais.
- Os nomes das variáveis são sensíveis a maiúsculas e minúsculas, ou seja, as letras maiúsculas são distintas das letras minúsculas.
- Usar uma palavra reservada (palavra-chave) como nome de variável mostrará um erro.

#### Exemplos:

```c
new new; // Incorreto: Usando uma palavra-chave reservada 'new'
new _new; // Correto

new 10letters; // Incorreto: Declaração do nome começando com um número
new letters10; // Correto
new letters_10; // Correto

new my name; // Incorrect: Espaço na declaração do nome
new my_name; // Correto

new !nternet; // Incorreto
new Internet; // Correto
```

### Armazenando diferentes tipos de dados

Depois disso, agora vamos ver alguns exemplos de que tipos de dados podem ser armazenados em variáveis e como:
```c
new letra = 'M';


new valor = 100;


new valorDecimal = 1.0;
// Funciona, mas mostrará um aviso do compilador: 
// warning 213: tag mismatch


new MotorOn = true;
// Funciona, e não mostrará um aviso de compilação, mas é sugerido o uso de uma Tag


new Setenca = "Isso é uma sentenca";
// Irá mostrar um erro:
// error 006: must be assigned to an array
```

Uma variável é capaz de conter um caractere, valor inteiro, booleano (verdadeiro ou falso) e um valor de flutuação (valor decimal). Os comentários no código acima mostram que armazenar uma string em uma variável resulta em um erro (como as strings podem ser armazenadas somente em _Arrays_). Fora isso, atribuir um valor de flutuação a uma variável resultará em um aviso do compilador, o que pode ser evitado pela adição de 'tags'. Sem tags adequadas, o script mostrará avisos após a compilação, mas será executável. As tags informam ao compilador sobre o tipo de dados que se pretende armazenar na variável, que por sua vez nos informa na forma de erros ou aviso se cometermos um erro de quebra de programa no código. Exemplo de tags:
```c
new valorDecimal = 1.0; // Incorreto
new bool: valorDecimal = 1.0 // Incorreto
new Float: valorDecimal = 1.0; // Correto

new switchOn = 1.0; // Incorreto
new switchOn = true; // Incorreto, mas não mostrará um erro ou aviso do compilador
new bool: switchOn = true; // Correto
```

O uso de Tags corretas é importante para evitar quaisquer erros ou bugs durante a execução do código.

Sendo o Pawn uma linguagem Typeless nos permite armazenar diferentes tipos de dados na mesma variável que pode ser útil em alguns casos e incômoda em outros, mas tal uso de variáveis não é recomendado.
```c
#include <a_samp>

public OnFilterScriptInit ()
{

    new var ;

    var = 'a';
    printf ("%c", var);

    var = 1;
    printf ("%d", var);

    var = 1.0;
    printf ("%f", var);

    var = true;
    printf ("%d", var); // Imprime um valor 0 ou 1

    return 1;
}

// Saída do console:
a
1
1.000000
1
```

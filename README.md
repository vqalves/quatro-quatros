# Quatro Quatros

QQSolver é um pequeno software para calcular as variações do problema dos [Quatro Quatros](https://pt.wikipedia.org/wiki/Quatro_quatros).

A base do desafio é, utilizando operações matemáticas básicas e apenas quatro números 4, elaborar as fórmulas para calcular todos os números de 0 a 100. Por exemplo:
* 0 = 44 - 44
* 1 = 44 / 44
* 2 = (4/4) + (4/4)

## Estratégia

O software se baseia em força-bruta - mapear e calcular todas as variações possíveis, e filtrar os resultados de interesse.

Para que a força-bruta seja viável, um algoritmo adequado para processar grandes volumes foi utilizado.

Algumas estratégias adicionais também foram implementadas, apesar de haver espaço para maiores otimizações:

* **Definição do limite dos cálculos** - Algumas funções unárias, como fatorial, podem ser repetidos ad infinitum. Por exemplo, (3!)! =  6! = 720. Portanto, foi adotado o [double](https://docs.microsoft.com/pt-br/dotnet/csharp/language-reference/keywords/double) para determinar o limite do aprofundamento.
* **Dicionário de fatoriais e termiais** - Um dicionário de fatorial e um de [termial](https://pt.wikipedia.org/wiki/Termial) são pré-preenchidos antes do inicio de processamento, para evitar o recálculo nas (muitas) situações em que ele é necessário. Pela quantidade de variações de um termial, foi adotado [int](https://docs.microsoft.com/pt-br/dotnet/csharp/language-reference/keywords/int) como limite de aprofundamento, calculando até 65535? = 2147450880.
* **Pré-carregamento dos fragmentos das fórmula** - A fórmula final de um "quatro quatros" é sempre composta de quatro números interagindo entre si. Então, são pré-processadas todas as formas que 2 e 3 números interagem, para só depois aplicar o mesmo principio para a combinação dos fragmentos 2-2 e 1-3. Quando o objetivo é apenas a formulação mais simples, aqui se utiliza apenas os fragmentos mais simples para chegar a um mesmo valor.
* **Mapeamento das fórmulas finais ad-hoc** - Utilizando o yield do C#, é possível calcular as fórmulas finais sob demanda e descartar logo em seguida, evitando sobrecarregar a memória do computador.
* **Formatação escrita da fórmula apenas sob demanda** - Em versões anteriores, a fórmula para print era escrita no momento que o objeto era criado. Cerca de 20% do processamento total era dedicado apenas para isso. Uma otimização foi feita para que a formatação só execute quando é necessário printar.

## Resultado

Após o setup inicial, o sistema conseguiu mapear e processar mais de 500.000 fórmulas por segundo.

O arquivo [Naturais.txt](https://github.com/StiveHawk/quatro-quatros/blob/master/Naturais.txt) contém todos os números naturais que o sistema gerou, em sua formulação mais simples (menos quantidade de operações possíveis para chegar ao número).

## Autor

Projeto idealizado por StiveHawk.

Inspirado em "Os quatro quatros" do livro "O Homem que Calculava", de Malba Tahan.

## Licença

Este projeto nasceu como parte de um estudo, e não há restrições de uso, cópia, modificação ou distribuição.

Mas referenciar este link é bem-vindo!
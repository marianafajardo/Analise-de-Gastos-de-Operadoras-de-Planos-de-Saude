<h1 align="center">Análise de Gastos com Operadoras de Planos de Saúde</h1>

<p align="center">
  <img src="https://user-images.githubusercontent.com/102304054/174603377-eae88112-4b41-4aa2-b03a-67fdccd859b8.png">
</p>

## 1. Dashboard

Esse dashboard foi desenvolvido através do curso de **"Power BI Para Data Science, Versão 2.0"**, realizado pela [Data Science Academy](https://www.datascienceacademy.com.br/). Ele pode ser visualizado de forma online e interativa, clicando na imagem abaixo:

<p align="center">
<a href="https://app.powerbi.com/view?r=eyJrIjoiZjU3MGVlZGMtMDVlNy00YTIzLWExOGMtYjk1YjdjNTA5M2JlIiwidCI6IjhlNDJlNTBlLTNkMWEtNDAzYy04ZWZmLTU4OGJkOGQxMjk5ZiJ9"><img src="https://user-images.githubusercontent.com/102304054/175696517-140582c6-a014-4fc7-b702-1649905772b6.png"></a>
</p>

## 2. Estudo de Caso

Os diretores de uma operadora de plano de saúde perceberam que os gastos de seguro de saúde aumentaram de forma considerável e precisam monitorar a evolução dos gastos. Os diretores fizeram diversas perguntas e gostariam de poder visualizar as respostas em uma única tela ou visualização. Os dados disponíveis correspondem ao ano anterior dos usuários da operadora e possuem as colunas: **idade**, **sexo**, **IMC (índice de massa corpórea)**, se é **criança**, se é **fumante**, a **região do usuário** e o **valor de seguro saúde** de cada usuário. 

Os diretores precisam de respostas às seguintes perguntas:

1. Qual é o gasto da operadora?
2. Qual é a idade média dos usuários da operadora?
3. Qual é o gasto médio por região?
4. Qual é a faixa etária possui maior gasto com seguro saúde por região?
5. As Crianças tem gasto maior que adultos?
6. Qual é a proporção de crianças por região?
7. O aumento da idade influencia no IMC?
8. Quem tem maior gasto, homens ou mulheres?
9. Se o usuário for mulher, o IMC é a cima ou abaixo da média?
10. Se for homem, com mais de 50 anos e da região Sudeste, o gasto é maior ou menor que a média de gastos da região?

Os dados fornecidos possuem *"problemas"*, erros que foram propositalmente inseridos no dataset (simulando problemas do mundo real). A proposta é responder às perguntas dos diretores através da elaboração de um dashboard e também detectar os problemas nos dados e decidir como resolvê-los.

## 3. Modelagem dos dados

No modelo foram identificados alguns erros, sendo eles:

* O cabeçalho está duplicado;
* O Power BI não conseguiu identificar a primeira linha como sendo o cabeçalho;

<img src="https://user-images.githubusercontent.com/102304054/175753464-2f3ee3cc-e9e9-4726-9787-58f22d3b3477.png"/><a>
</p>

Para resolver os dois problemas a cima, abri o Power Query e selecionei a opção *Usar a Primeira Linha como Cabeçalho*, resolvendo o problema dos nomes nas colunas. Em seguida, a opção Remover Linhas Principais, foi selecionada para excluir a linha que antes estava repetida.
Como próximo passo e com o objetivo de verificar se o modelo apresentava outras inconsistências, foi utilizado o filtro em cada coluna para validar se existiam dados inconsistentes, que provou-se verdadeiro em diversas colunas, eram elas: **Sexo**, **Fumante** e **Região**. 

<img src="https://user-images.githubusercontent.com/102304054/175753831-68a45081-36a1-4a43-ac2b-603abf452380.png"/><a>
</p>

Para resolver essas inconsistências, utilizei uma espécie de atalho, ou seja, ocultei através da filtragem os valores inconsistentes. 
Obs: É preciso entender que para criar gráficos essa alternativa atende, porém caso fosse trabalhar com machine learning, treinamento de modelo ou tarefas estatísticas mais avançadas, essa opção não seria suficiente, seria necessário remover realmente esses registros do conjunto de dados.

* Analisando as colunas **Crianças** e **Idade**, conclui-se que não é possível responder as perguntas de número 5 e 6, já que com base nos dados apresentados na **Idade**, não existem crianças nesse dataset.
* *Realizar  a organização dos dados, onde cada palavra deve ser devidamente acentuada e suas primeiras letras tornarem-se maiúsculas, a fim de deixar o relatório final mais legível.
* *Correção do tipo de variável utilizada em algumas das colunas, de Texto foram convertidas em Número Inteiro ou Número Decimal. As colunas que sofreram mudanças de tipo de variável foram: **Idade** (número inteiro), **IMC** (número decimal) e **Valor Seguro Saúde** (número decimal).

<img src="https://user-images.githubusercontent.com/102304054/175753841-e8e8713e-7a05-44dc-9d70-2bc2a57312a6.png"/><a>
</p>

* *Os grupos de dados* foram criados a partir da opção *Novos grupos de dados* no formato de *Lista* utilizando a coluna **Idade** como referência. Assim, as duas novas colunas chamadas **Faixa Etária** e **Meia Idade** foram preenchidas com informações que separavam os clientes da seguradora em grupos por faixa etária além de mais dois grupos de maior ou menor de 50 anos.
* Por fim, utilizando a opção *Nova medida*, as duas medidas *Média Idade* e *Média IMC* foram adicionadas ao dataset utilizando a fórmula *AVERAGE* do Power Query, trazendo as médias, respectivamente, da Idade e do IMC dos usuários do plano de saúde.

<img src="https://user-images.githubusercontent.com/102304054/175753852-28506a34-da83-4dfa-8a54-6649c45edfb5.png"/><a>
</p>

## 4. Indicadores

Depois desse processo de análise exploratória, foi possível dar início no desenvolvimento das Visualizações, conforme as informações solicitadas pela área de negócio.

**1. Qual é o gasto da operadora?**

<img src="https://user-images.githubusercontent.com/102304054/175773573-41cd6db2-b931-495c-8d81-09704ed2b6d3.png"/><a>
</p>

Para responder a essa pergunta, foi utilizado um *cartão*, trazendo o total da coluna **"Valor_seguro_saude"**.

**2. Qual é a idade média dos usuários da operadora?**

<img src="https://user-images.githubusercontent.com/102304054/175773579-6a7108a6-e466-44d9-bee6-bb5f9d5077a5.png"/><a>
</p>

Para responder a essa pergunta, foi criada uma medida chamada de *"Média_Idade"*, utilizando a tabela *"seguro_saude"*, coluna **Idade** e a função *AVERAGE*. A medida *"Média_Idade"*, foi adicionada a um *cartão*.

**3. Qual é o gasto médio por região?**

<img src="https://user-images.githubusercontent.com/102304054/175773580-8fe1194f-990a-4c91-9bde-5365318ebbec.png"/><a>
</p>

Para responder a essa pergunta, foi utilizado um *gráfico de barras*, em eixo a coluna **"Região"** e em valores a coluna **"Valor_seguro_saude"**. Por padrão, o Power BI, inclui como resultado a soma de uma coluna, porém é possível alterar esse valor para média, Mediana, Variação, Desvio padrão, etc. E para o caso a cima, selecionamos a média da coluna correspondente. 

**4. Qual é a faixa etária possui maior gasto com seguro saúde por região?**

<img src="https://user-images.githubusercontent.com/102304054/175773585-86d882d0-e46d-4825-95c5-ac29c293e9fb.png"/><a>
</p>

Para responder a essa pergunta, foi utilizado um *gráfico de barras clusterizado na vertical* e o recurso *"Grupos de dados"*, a fim de criar uma coluna denominada de **"Faixa Etária"**, contendo as faixas etárias contidas no gráfico a cima. 
Conclui-se que as pessoas na faixa etária de *"50 à 59"* e região *"Sul"*, possuem um maior gasto com seguro saúde.

**5. As Crianças tem gasto maior que adultos?**

Para responder a essa pergunta, foi analisado o conjunto de dados e identificado que a especificação não está condizente com os dados, ou seja, a coluna **"Criança"** que deveria indicar se os usuários são ou não são crianças, apresenta uma classificação de 0 à 5, não deixando claro o que cada um dos números representa. Além disso, não está de acordo com coluna **"idade"**, a qual mostra que não há crianças neste dataset, já que a menor idade é de 18 anos. Portanto, não é possível se as crianças tem gasto maior ou menor que adultos com os dados que foram fornecidos. 

**6. Qual é a proporção de crianças por região?**

Assim como na questão 5, não é possível responder a proporção de crianças por região com os dados que foram fornecidos no conjunto de dados.

**7. O aumento da idade influencia no IMC?**

<img src="https://user-images.githubusercontent.com/102304054/175773589-e92b34c7-c88d-4614-b57f-35552683705d.png"/><a>
</p>

Para responder a essa pergunta, foi utilizado um *gráfico de dispersão*, ou seja, um gráfico de análise bivariada, que mostra a relação de duas variáveis. Nesse estudo de caso, o objetivo é estudar a relação entre a variável **"Idade"** e a variável **"IMC"**. 
No eixo X foi adicionado os dados relacionados a **"Idade"** e no eixo Y, os dados relacionados ao **"IMC"**. No entanto, para atingir a visualização desejada, é necessário selecionar a opção *"Não resumir"* para que não seja feito nenhum cálculo com os dados. 
Além disso, foi adicionado uma linha de tendência para facilitar na interpretação do gráfico, sendo possível notar uma tendência positiva, ou seja, aparentemente crescente, concluindo que a medida que a idade aumenta, o IMC aumenta, também.

**8. Quem tem maior gasto, homens ou mulheres?**

<img src="https://user-images.githubusercontent.com/102304054/175773595-6851f881-3afa-4f58-9373-31af38609ba2.png"/><a>
</p>

Para responder a essa pergunta, foi utilizado um *gráfico de rosca*, a variável **"Sexo"** em detalhes e a variável **"Valor_seguro_saude"** em valores, concluindo que pessoas do sexo Masculino tiveram um gasto maior de Seguro saúde, do que pessoas do sexo Feminino. 

**9. Se o usuário for mulher, o IMC é a cima ou abaixo da média?**

<img src="https://user-images.githubusercontent.com/102304054/175773598-bb798aed-6c9e-4d5a-8540-f774209b2476.png"/><a>
</p>

Para responder a essa pergunta, foi criado uma *tabela* com um *cartão* associado. No cartão foi adicionado a medida *"Média_IMC"*, mostrando a média de IMC de todas as pessoas, totalizando 30.64. E na tabela, a medida *"Média_IMC"* segmentada por sexo, possibilitando a separação das médias de IMC por sexo, concluindo que se a pessoa é do sexo feminino, estará abaixo da média de IMC, já se for do sexo masculino, estará a cima da média de IMC.

**10. Se for homem, com mais de 50 anos e da região Sudeste, o gasto é maior ou menor que a média de gastos da região?**

<img src="https://user-images.githubusercontent.com/102304054/175773602-56705ab0-ca9b-421c-a1a9-77392a239bd5.png"/><a>
</p>

Como proposta de solução dessa pergunta, foi configurado alguns filtros através da opção *"Segmentação de Dados"*.

Primeiramente, para criação do filtro relacionado a *"Meia-Idade"*, foi utilizado novamente o recurso *"Grupos de dados"*, a fim de criar uma coluna denominada de **"Meia-idade"**, contendo a classificação de *"Mais de 50"* e *"Menos de 50"*. Como complemento, foi incluso um filtro específico para *"Região"* e um outro filtro para *"Sexo"*.

Em seguida, com o objetivo de realizar a comparação dos valores filtrados, foi adicionado uma tabela com *"valores fixos"* relacionados as respectivas *"Regiões"* e a *"Média de valor seguro Saúde"* por região. Essa tabela, não possui interatividade com os filtros, isto é, ela não sofre alterações quando a filtragem ocorre no dashboard.

E assim, é possível concluir que a média da região Sudeste baseada nos filtros (Meia-Idade, Região e Sexo), é de 15.355,57, ou seja, está a cima da média total por Região (Sudeste), a qual possui a média equivalente a 12.268,34.

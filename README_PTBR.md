 <h1 align="center"> "Hotel Chain Cancellation Rating" </h1>

![Getting Started](./img/bank.jpg)


# Sejam bem-vindos ao meu projeto de portfólio da competição de dados da Comunidade DS: "Billion Bank"


## 1.0 Contexto do Negócio

O Billion Bank é um banco digital brasileiro, fundado em 2021. Trabalha hoje com contas digitais, e cartões de crédito.

Quando um cliente solicita aumento de limite no cartão de crédito, o banco consulta uma empresa de crédito terceira, que retorna uma recomendação: "negar" ou "conceder". Essa resposta é repassada ao cliente.

Dado que a empresa de crédito precisa levantar maiores informações de histórico financeiro do cliente com terceiros, o retorno da recomendação ao banco leva até 5 dias úteis!

Tratando-se de um serviço, a cada solicitação de aumento de limite feita por um cliente, o banco tem um custo adicional de consulta. Visando reduzir este custo, em 2022, o banco passou a só aceitar novos pedidos de aumento de limite a cada 3 meses.

O banco viu um aumento leve do churn no primeiro semestre, que se acentuou mais no segundo, chegando a um ponto já preocupante. O time de CS fez contato com antigos clientes, e constatou que o principal motivo do churn foi a percepção de burocracia relacionada ao aumento nos limites.

Para reverter o cenário, o banco traçou um plano de ação com dois objetivos:
1 - Desburocratizar o processo, permitindo que o cliente possa solicitar um novo limite uma vez por semana, tendo uma resposta instantânea.
2 - Desativar as consultas de recomendação de aumento de limites feitas hoje com a empresa terceira, que são demoradas e custosas.

Para concretizar o plano, foi solicitado ao time de cientistas de dados, que com base no histórico de recomendações ("negar" ou "conceder") da empresa de crédito, aliado ao histórico financeiro dos clientes, desenvolvam um modelo de avaliação de aumento de limite de cartão de crédito dentro de casa.

O modelo de classificação, deve informar se o Billion Bank deve "negar" ou "conceder" o aumento no limite solicitado pelo cliente.

**Fonte:** [ Kaggle ](https://www.kaggle.com/competitions/cdshackdays3)


## 2.0 Planejamento prévio

* Nesta competição os alunos da Comunidade DS foram divididos em Squad's com 4 estudantes cada. Ao todo tivemos 24 Squad's e mais de 90 participantes ao todo.
* O meu Squad teve a seguinte formação:

![Squad](./img/leaderboard.png)


### O método CRISP-DS foi utilizado como base para o desenvolvimento deste projeto

![Crisp](./img/ciclo.png)


### 2.1 Ferramentas, IDE's e Bibliotecas

* Python 3.09
* Visual Studio Code
* Jupyter Notebook
* Deepnote
* Bibliotecas: Seaborn, Pandas, Numpy, Inflection, Scipy, Dython_Nominal, XGBoost, SKLearn, Category Encoders e LightGBM

### 2.2 Produto final

* Uma solução de classificação que aponte a melhor previsão possível para um cancelamento de uma reserva realizada na rede. Dessa maneira a rede hoteleira poderá tomar as melhores medidas cabíveis, embasada nos perfis dos seus clientes, para poder evitar o cancelamento de reservas já realizadas.


## 3.0 Dados

##### Estes dados são públicos e foram baixados na página web do [Kaggle](https://www.kaggle.com/competitions/cdshackdays4).

### 3.1 Atributos de origem

| **Atributos**                           |  **Tipo**  |  **Descrição**                                               |
| ----------------------------------------|------------|--------------------------------------------------------------|
| id                                      | int64      | Número de indentificação                                     |
| classificacao_do_hotel                  | object     | Quantidade de estrelas do hotel                              |
| meses_da_reserva_ate_o_check-in         | int64      | Quantidade de meses da reserva até o check-in                |
| numero_de_pernoites_reservadas          | int64      | Número de pernoites reservados                               |
| numero_de_hospedes                      | float64    | Número de de hóspedes                                        |
| regime_de_alimentacao                   | object     | Tipo de refeição inclusa                                     |
| nacionalidade                           | object     | Nacionalidade                                                |
| forma_de_reserva                        | object     | Como a reserva foi realizada                                 |
| ja_se_hospedou_anterioremente           | object     | Se o cliente já se hospedou no hotel                         |
| tipo_do_quarto_reservado                | object     | Tipo de quanrto/suíte                                        |
| reserva_feita_por_agencia_de_turismo    | object     | Se a reserva foi feita em agência de turismo                 |
| reserva_feita_por_empresa               | object     | Se a reserva foi realizada por uma empresa                   |
| reserva_com_estacionamento              | object     | Se a reserva inclui vaga para estacionamento de veículo      |
| reserva_com_observacoes                 | object     | Observações a serem feitas no ato da reserva                 |
| reserva_cancelada                       | int64      | Variável alvo, saber ser haverá cancelamento da reserva      |


### 3.2 Atributos criados

* estrelas_quarto -> o percentual de classificação do quarto entre 4 e 5 estrelas
* combo_alimentacao -> o tipo de regime de alimentação derivado do tipo de quarto
* nights_per_hotel -> a mediana dentre o tipo de quarto locado e a classificação do hotel.


## Visualização dos atributos numéricos em gráfico de barras
![histplot](./img/histplot.png)

## Visualização dos meses da reserva até a data do check-in 
![scatter](./img/scatter.png)

## Visualização da correlação de Atributos Categóricos utilizando a fórmula Cramer's.
![cramer](./img/cramer.png)


## Visualização da correlação de Atributos Categóricos utilizando a fórmula do Coeficiente de Incerteza de Theil.
![theil](./img/theil.png)



## 4.0 Modelagem dos dados

Nesta etapa, os dados foram preparados para o início das aplicações dos modelos de Machine Learning.<br>
Foram utilizadas técnicas de Rescaling do tipo numérico e categórico, através do 'Label Encoder', 'Target Encoder' e 'Robust Scaler'

## 5.0 Machine Learning Modeling

Nesse processo de escolha de modelos de Machine Learning, foram relizados testes e treinamentos com seis tipos de Classificadores, eles são os seguintes: Random Forest Classifier, Extra Tree Classifier, XGBoost Classifier, LGBM Classifier, K-Nearest Neighbors e o Decision Tree Classifier.<br>
A métrica utilizada para a avalição dos algoritmos de classificação foi o F1 Score.

## Performance

![perform](./img/score.png)


## 6.0 Ensemble Learning

Aqui aplicamos a técnica de Ensemble Learning, para aplicação de tal técnica utilizamos a biblioteca 'Voting Classifier' da 'Scikit Learn'.<br>
Este algoritmo combina o conceito de diferentes classificadores de Machine Learning, e usa a maioria dos votos ou a média das probabilidades previstas, para
assim, realizar a predição da classe alvo. Essa classificação pode se usada para alcançar uma simetria de performance no balanceamento geral dos dados. Em outras palavras, o algoritmo potencializa as vantagens de um determinado algoritmo de Machine Learning para balancear as suas fraquezas na classificação.

## Performance Final de:

# 0.9731184748459742

## 7.0 Conclusão

Passadas as 32 horas de duração do Hack Days, as submissões foram encerradas e o Leaderboard foi fechado.
O trabalho desenvolvido pelo nosso time apresentou uma acurácia final de 0.97146 e nós realizamos 21 submissões ao todo. A nota mais alta é a que conta neste tipo de competição.<br>
No fechamento geral do leaderboard ficamos na 4º colocação, provando que estávamos desenvolvendo nosso projeto no caminho certo. 
A classificação final foi decidida na casa dos centésimos, mostrando assim, como a disputa foi super acirrada na reta final e as equipes estavam balanceadas e focadas na entrega de um bom trabalho final.<br>
Nós da EquiPÃO dos dados conseguimos entregar um excelente trabalho, num intervalo de tempo super justo, então temos muito o que comemorar.<br>
O aprendizado nesse curto espaço de tempo foi ENORME!!!
Só tenho a agradecer os meus companheiros de equipe, são eles: Samuel, Juli, Valéria e Wilmara. Deixo também o meu agradecimento aos nossos professores e a todos da Comunidade DS!!!


## Leaderboard

![leaderboard](./img/leaderboard.png)
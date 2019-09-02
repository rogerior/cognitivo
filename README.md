## Autor: Rogério Rodrigues Carvalho


Para a resolução desse Teste utilizei a metodologia de data mining CRISP-DM.

![crisp-dm](https://user-images.githubusercontent.com/11646044/64084631-c5e18d00-cd03-11e9-907a-8deb8c19e35f.png)

O CRISP-DM é dividido em 6 fases que são: 
1. Business Understanding
2. Data Understanding
3. Data Preparation
4. Modeling
5. Evaluation
6. Deployment

Existe um Jupyter Notebook para cada uma das etapas acima, exceto a etapa de “Deployment” que não foi solicitado para ser feito.


##### Respostas para os pontos solicitados: 

**a. Como foi a definição da sua estratégia de modelagem?**

Projetei e realizei as seguintes etapas:
1. Tratamento dos dados
	- Binarizar atributo ‘type’
	- Tratar valores inconsistentes do atributo ‘alcohol’
2. Separar 20% dos dados para serem usados como dados de validação e 80% para treino das técnicas de predição
3. Montar pipeline de treinamento dos modelos da seguinte forma:
	- Os 80% dos dados, escolher de qual forma eles serão separados (split). As opções disponíveis de separação dos dados são:
		- 80% para treino e 20% para teste, ou
		- 75% para treino e 25% para teste, ou
		- 70% para treino e 30% para teste
	- Aplicar normalizadores: o normalizador que será utilizado é escolhido de forma aleatória, tendo a opção de não escolher nenhum normalizador para utilizar também. Os normalizadores disponíveis são:
		- StandardScaler
		- RobustScaler
		- MinMaxScaler
		- Normalizer
	- Aplicar redutor de dimensionalidade: é escolhido de forma aleatória se será utilizado o redutor de dimensionalidade ou não. Caso seja escolhido utilizar o redutor de dimensionalidade, será utilizado o:
		- PCA
	- Testar 15 técnicas de regressão:
		- AdaBoostRegressor
		- BaggingRegressor
		- DecisionTreeRegressor
		- ExtraTreeRegressor
		- ExtraTreesRegressor
		- GradientBoostingRegressor
		- HuberRegressor
		- KNeighborsRegressor
		- LinearRegression
		- MLPRegressor
		- PassiveAggressiveRegressor
		- RadiusNeighborsRegressor
		- RandomForestRegressor
		- SGDRegressor
		- TheilSenRegressor
	- Utilizar Random Search para descobrir melhor combinação de parâmetros do pipeline, definindo o Random Search para realizar 4 iterações
	- Avaliar desempenho do modelo com as 4 métricas de regressão:
		- Mean absolute error
		- Mean squared error
		- Mean squared log error
		- Median absolute error
	- Salvar resultado do desempenho do modelo, em arquivo .csv
	- Salvar modelo gerado
- Observação: Cada técnica teve o Pipeline montado (de forma aleatória) e executado por 20 vezes, com o objetivo de encontrar a combinação de Pipeline e parâmetros que apresente o melhor desempenho


**b. Como foi definida a função de custo utilizada?**

O atributo classe ‘quality’ representa a nota da qualidade do vinho. 

Em problemas que devemos predizer a nota (tipo de dado ordinal), o objetivo é aproximar o máximo possível do valor predito com o valor real, e não acertar em cima.

Com base no objetivo da predição, trabalhei este conjunto de dados como sendo um problema de **regressão**, então fiz a escolha de 4 das principais métricas/funções de custo de problemas de regressão, que são as:
- Mean absolute error (MAE)
- Mean squared error (MSE)
- Mean squared log error
- Median absolute error


**c. Qual foi o critério utilizado na seleção do modelo final?**
	
Na documentação do Random Search explica que por padrão é utilizado a métrica (score) padrão de cada técnica de regressão. 

Verificando na documentação de todas as técnicas de regressão que eu utilizei, identifiquei que a métrica (score) padrão de todas é o   coeficiente de determinação, também conhecido como R^2. Então o critério utilizado para a seleção do modelo foi o R^2.

**d. Qual foi o critério utilizado para validação do modelo? Por que escolheu utilizar este método?** 

Utilizei como critério para validar o modelo gerado, um conjunto de 20% dos dados que foi separado para serem utilizados nesta etapa de validação. 

Escolhi utilizar essa abordagem pois os dados de validação que foram separados representam um conjunto de dados que o modelo não conhece, e esta forma possibilita identificarmos como é o desempenho do modelo com dados nunca vistos. 

**e. Quais evidências você possui de que seu modelo é suficientemente bom?**

Segundo a documentação das métricas utilizadas, quanto mais próximo de 0 o resultado da métrica, significa que o modelo de predição teve um melhor desempenho.

Observando a tabela abaixo (essa tabela representa o desempenho de todos os modelos testados) que está ordenada pelo menor valor da métrica ‘Mean squared log error’, identifiquei que os modelos apresentaram ótimos desempenhos, tendo valor de 0 (o melhor resultado possível) na métrica ‘Mean absolute error’ e valores bem próximo de 0 na métrica ‘Mean squared log error’.

![tabela_melhores_desempenhos](https://user-images.githubusercontent.com/11646044/64084640-d1cd4f00-cd03-11e9-9813-6d87f4c07691.png)


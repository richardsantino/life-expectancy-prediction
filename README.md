## Predição de expectativa de vida.
Este projeto tem como objetivo entender como variaveis da humanidade se relacionam com a expectativa de vida e criar um modelo preditivo que, baseado em variaveis de entrada, prevê a expectativa de vida.

## Conteúdo
0. [Desafio](#desafio)
1. [Dados](#dados)
2. [Insights](#insights)
3. [Modelo](#insights)

## Desafio
É parte do desafio responder as seguintes questões:

**1.** Os diversos fatores preditivos escolhidos inicialmente realmente afetam a expectativa de vida? Quais são as variáveis preditoras que de fato influenciam a expectativa de vida? <br>
**2.** Um país com expectativa de vida baixa (inferior a 65 anos) deveria aumentar seus gastos com saúde para melhorar sua longevidade média? <br>
**3.** Como as taxas de mortalidade infantil e adulta afetam a expectativa de vida? <br>
**4.** A expectativa de vida tem correlação positiva ou negativa com hábitos alimentares, estilo de vida, prática de exercícios, tabagismo, consumo de álcool etc.? <br>
**5.** Qual é o impacto da escolaridade na longevidade humana? <br>
**6.** A expectativa de vida apresenta relação positiva ou negativa com o consumo de álcool? <br>
**7.** Países densamente povoados tendem a ter expectativa de vida mais baixa? <br>
**8.** Qual é o impacto da cobertura vacinal (imunização) sobre a expectativa de vida? <br>
**9.** Criar um modelo preditivo para prever a expectativa de vida.

## Dados
Os dados foram coletados pela World Health Organization (WHO ~ Organização Mundial de Saúde) e United Nations (ONU ~ Organização das Nações Unidas). Refletem a humanidade entre 2000 e 2015 para 193 países *(population_2000_2015_all_countries.csv)*. <br>
Os dados de população, continente e subcontinente **('Population', 'region', 'subregion')** foram extraidos via API durante o projeto *(population_2000_2015_all_countries.csv, region_subregion_all_countries.csv)*.

- **'Year'**: Ano.
- **'Country'**: País.
- **'region'**: Continente.
- **'subregion'**: Subcontinente.
- **'Status'**: Status de desenvolvimento.
- **'Population'**: Quantidade de pessoas.
- **'Income composition of resources'**: Índice de Desenvolvimento Humano (IDH) baseado na renda.
- **'Schooling'**: Quantidade de anos de escolarização.
- **'Alcohol'**: Quantidade consumida de álcool em média por pessoa de 15+ anos (l ~ puro álcool).
- **'GDP'**: Produto Interno Bruto (PIB) médio por pessoa (U$D).
- **'BMI'**: IMC médio das pessoas.
- **'thinness 10-19 years'**: Percentual de pessoas de 10 a 19 anos magras (%).
- **'thinness 5-9 years'**: Percentual de pessoas de 5 a 9 anos magras (%).
- **'Total expenditure'**: Percentual do gasto do governo gasto com saúde (%).
- **'Hepatitis B'**: Percentual de bebês (1- anos) imunes contra Hepatite B (%).
- **'Polio'**: Percentual de bebês (1- anos) imunes contra Poliomielite (%).
- **'Diphtheria'**: Percentual de bebês (1- anos) imunes contra difteria tétano e coqueluche (vacina combinada) (%).
- **'Adult Mortality'**: Quantidade de mortes de pessoas de 15 a 60 anos (a cada 1k pessoas).
- **'infant deaths'**: Quantidade de mortes infantis (a cada 1k pessoas).
- **'under-five deaths'**: Quantidade de mortes de crianças (5- anos) (a cada 1k pessoas).
- **'HIV/AIDS'**: Quantidade de mortes de crianças (5- anos) por HIV/AIDS (a cada 1k pessoas).
- **'Measles'**: Quantidade de casos de sarampo (a cada 1k pessoas).
- **'Life expectancy'**: Expectativa de vida (anos).

🔗 [dataset link ~ Kaggle](https://www.kaggle.com/datasets/kumarajarshi/life-expectancy-who) <br>
⚙️ [api região e subregião link ~ Publicapi](https://publicapi.dev/rest-countries-api) <br>
⚙️ [api população link ~ World Bank](https://documents.worldbank.org/en/publication/documents-reports/api) <br>
 
## Insights
As respostas para o desafio se beaseam no EDA, mais especificamente na *Analise Bivariada* usando Regressão Linear (OLS) e respeitando as premissas para inferir insights sobre os coeficientes (variaveis dos dados). <br>
O modelo linear (OLS) obteve um **R²** de 0.872, logo os coeficientes certamente explicam como as variaveis influenciam a expectativa de vida.

**1.**
As variaveis preditoras significantes que influenciam a expectativa de vida são:
- Year, positivamente (imagino que seja uma variavel proxy pra outra variavel).
- Developed, positivamente.
- Population, positivamente (imagino que seja uma variavel proxy pra outra variavel).
- Income_composition_of_resources, positivamente.
- Schooling, positivamente. (mais impactante ~ coef: 0.1802)
- GDP, positivamente.
- Polio, positivamente.
- Diphtheria, positivamente.
- Polio, positivamente.
- Diphtheria, positivamente.
- Measles, negativamente.
- HIV_AIDS, negativamente. (mais impactante ~ coef: -0.2468)
- under_five_deaths, negativamente.
- Adult_Mortality, negativamente.
- thinness_10_19_years, negativamente.
- Hepatitis_B, negativamente, tal variavel deveria influenciar positivamente, logo imagino que possa existir uma variavel de confusão por trás.

-- dummies *subregion* sobre comparação a Southern Asia -- 
- North_America, positivamente. (mais impactante ~ coef: 0.0419)
- Southern_Europe, positivamente.
- Middle_Africa, negativamente.
- Eastern_Europe, negativamente.
- Western_Africa, negativamente. (mais impactante ~ coef: -0.2174)
- Southern_Africa, negativamente.
- South_Eastern_Asia, negativamente.
- Eastern_Africa, negativamente.
- Melanesia, negativamente.
- Central_Asia, negativamente.
- Micronesia, negativamente.

variaveis *não* significantes:
- Alcohol, muito irrelevante.
- BMI.
- Total_expenditure, p-value: 0.311, tal variavel deveria ser fortemente relacionada com a expectativa de vida, será que os gastos com saudes acontecem de forma errada ("sem inteligência")?

-- dummies *subregion* sobre comparação a Southern Asia -- 
- Southeast_Europe.
- Northern_Africa.
- Caribbean.
- South_America.
- Western_Asia.
- Australia_and_New_Zealand.
- Central_Europe.
- Western_Europe.
- Central_America.
- Eastern_Asia.
- Northern_Europe.
- Polynesia.

**2.** Depende, dados dizem que o **percentual de gosto do governo gasto com saude** não influencia significavelmente a *expectativa de vida*, porem vimos que vacinação de **Diphtheria** e **Polio** em crianças influenciam positivamente (e significavelmente) a *expectativa de vida*. Com isso imagino que o gasto com saude tenha que ser "inteligente" (mais estratégico) e não apenas por gastar.

**3.** Afetam negativamente a *expectativa de vida*, sendo a mortalidade adulta (2x+) mais impactante.

**4.** O dataset não contem dados exatos para responder tal pergunta, porem usando as variaveis **thinness_10_19_years** e **thinness_5_9_years** como proxy de habitos saudaveis/não saudaveis (magreza reflete habitos não saudaveis), vemos que habitos não saudaveis influenciam negativamete (e significavelmente) a expectativa de vida.

**5.** Impacto posito e o maior das variaveis que impactam positivamente, outro insight que fortifica que a humanidade precisa fazer coisas mais "inteligentes". Pode também mostrar que a escolarização esta sendo bem administrada pelo governo para influenciar a *expectativa de vida*.

**6.** Consumo de álcool é irrelevante para influenciar a expectativa de vida.

**7.** Não, tendem a ter expectativa de vida mais alta. 

**8.** Positivo **Diphtheria** e **Polio** para e nagativo para **Hepatitis_B**, sendo, em módulo, o coef de **Hepatitis_B** o menor (menos impactante) e **Diphtheria** o maior (mais impactante).

## Modelo
...

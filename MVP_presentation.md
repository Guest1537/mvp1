# MVP Engenharia de Dados
Pedro Caleffi Barbosa

# Objetivo
Explorar e analisar dados disponíveis na base do Sistema de Estimativas de Emissões e Remoções de Gases de Efeito Estufa (SEEG). 
Perguntas:

(I) Qual o maior emissor de gases de efeito estufa referentes à mudança de uso do solo e florestas?

(II) Quais são as 10 principais atividades mais emissoras de GEE no Brasil durante o período?

(III) Quais foram e quando ocorreram os picos de produção das atividades contempladas na base de dados?


# Busca pelos dados
Seleção dos arquivos "ATIVIDADE_SEEG10_TODOS_SETORES_2022.10.23" e "1-SEEG10_GERAL-BR_UF_2022.10.27-FINAL-SITE"

https://seeg.eco.br/download/

Em: TABELA DE DADOS DE ATIVIDADE - BRASIL E ESTADOS (SEEG10) e DOWNLOAD DA TABELA GERAL DE DADOS - Brasil e Estados (1990-2021)
![image](https://github.com/Guest1537/mvp1/assets/143922275/3459ef67-f960-4ba7-9f5e-36de8fcf6c7c)

Em 26/09/2023 às 21:23 o link para download da tabela selecionada no site estava quebrado.
Arquivos também disponíveis para download em: 

https://docs.google.com/spreadsheets/d/1Qby5NARoUhZdUbmauSw5sHaVK6qnRKjM/edit?usp=sharing&ouid=117863055539952818718&rtpof=true&sd=true 

https://docs.google.com/spreadsheets/d/1p2_P_Jn47gnI_4w_ZRjQ-V5pSVMM93zq/edit?usp=drive_link&ouid=117863055539952818718&rtpof=true&sd=true


Em "ATIVIDADE_SEEG10_TODOS_SETORES_2022.10.23": Seleção das tabelas "Dados de Atividade BR", "Dados de Atividade UF" e "Dados Mudanças de Uso da Terra"
![image](https://github.com/Guest1537/mvp1/assets/143922275/17d74460-10aa-404b-ae53-f958789608b0)

Criação de tabelas individuais:
Dados de Atividade BR -> Dados.de.atividades.BR - link para download do google drive: https://drive.google.com/file/d/1v2n61Z0ohyJr4eVc9iFx-fNKp4mdAIBE/view?usp=drive_link

Dados de Atividade UF -> Dados.de.atividade.UF - link para download do google drive: https://drive.google.com/file/d/12wLLh8iTZx-zahf_qrM8qbJrYO08s_c1/view?usp=drive_link

Dados Mudanças de Uso da Terra -> Dados.mudancas.de.uso.de.terra - link para download do google drive: https://drive.google.com/file/d/1h1NAL4hrh0KdyzYUmqFLnySVH31eKJY2/view?usp=drive_link

Abaixo, imagens das respectivas tabelas antes de ser transformada em csv:

![image](https://github.com/Guest1537/mvp1/assets/143922275/1fb0ed15-df9d-4cc5-bb72-65d63931c56d)

![image](https://github.com/Guest1537/mvp1/assets/143922275/f10e4b42-19a6-4d63-90d4-91473637ae6b)

![image](https://github.com/Guest1537/mvp1/assets/143922275/77a23392-9c83-40ed-8858-95173252c4c5)

Em "1-SEEG10_GERAL-BR_UF_2022.10.27-FINAL-SITE": Seleção da tabela "GEEBrasil"

![image](https://github.com/Guest1537/mvp1/assets/143922275/5911d60a-8291-40e8-9d1d-5d9da02d9f30)

Criação de tabela individual: GEEBrasil - link para download do google drive: https://drive.google.com/file/d/1jH8rNZVKT_Hv-0GAFMrjPv9edXiPSUNo/view?usp=drive_link

Abaixo, imagem da tabela supracitada após transformação em csv:

![image](https://github.com/Guest1537/mvp1/assets/143922275/ebb472fe-3c94-43a6-ac92-46b7a3ac2abe)


# Coleta
Dados baixados para a máquina local e inseridos manualmente em um bucket (mvpgee) do Google Cloud

![image](https://github.com/Guest1537/mvp1/assets/143922275/6de4291d-0656-4c6c-9616-afc561fc098f)

![image](https://github.com/Guest1537/mvp1/assets/143922275/41f37f5a-8c27-499e-92b4-be8fbd180670)

Exemplo de upload para o bucket (mvpgee) utilizando o terminal Cloud Shell

![image](https://github.com/Guest1537/mvp1/assets/143922275/af18d1bc-0470-42c6-b335-6e3b3ee25c36)




# Modelagem

##### Dados de Atividade BR e Dados de Atividade UF
![image](https://github.com/Guest1537/mvp1/assets/143922275/84396943-097f-4597-80f5-3a2eef25eaea)

Única diferença entre as tabelas BR e UF supracitadas é a coluna UF:

Setor - Setorização da atividade produtiva em "Descricao"

Ano - Ano de referência à produção referenciada em "Descricao", entre 1970 e 2021

Descricao - Atividade produtiva

Unidade - Unidade de mensuração da produção vinculada à "Descricao". Ex.: Produção de Aço em toneladas -> Unidade = t

UF:

  - Em: Dados de Atividade BR, BR = Brasil

  - Em: Dados de Atividade UF, UF = UF de referência da produção apresentada

Valor - Quantidade produzida em "Unidade" para a "Descricao"

  - Em: Dados de Atividade BR, Quantidade produzida no Brasil para o "Ano"

  - Em: Dados de Atividade UF, Quantidade produzida no "UF" referência para o "Ano"

Fonte - Fonte dos dados apresentados na tupla

##### Dados Mudanças de Uso da Terra
![image](https://github.com/Guest1537/mvp1/assets/143922275/d7a7f5b6-5175-4abb-976e-cbf521a37b95)


Setor - Mudanças de Uso da Terra e Florestas

Ano - Ano de referência à Mudança de Uso da Terra e Florestas referenciada em "Valor", entre 1970 e 2021

Processo - Classificação entre Vegetação Nativa, Regeneração, Desmatamento e Outras Mudanças de uso da terra

Bioma - Bioma em que ocorreu a Mudança de uso da terra

Transicao - Caracterização da Mudança de Uso da Terra apresentando 2 dos denominadores abaixo concatenados por "--":

  - "Área sem vegetação", "Floresta primária", "Floresta segundária", "Uso agropecuário", "Silvicultura", "Vegetação não florestal primária" e "Vegetação não florestal secundária"

Status_de_conservacao - Caracterização da Mudança de Uso da Terra e Floresta em dentro ou "fora de Área protegida"

Unidade - Hectares

Valor - Quantidade de hectares que apresentaram Mudança de Uso da Terra e Floresta para o Ano e local especificado

Fonte - Fonte dos dados apresentados na tupla

##### Dados de Emissões de Gases de Efeito Estufa no Brasil
![image](https://github.com/Guest1537/mvp1/assets/143922275/b385c517-a503-4e77-8f25-edfdef08e7b5)

Nivel1_Setor - Especificação do setor emissor/removedor entre "Processos Industriais", "Energia", "Mudança de Uso da Terra e Florestas", "Agropecuparia" e "Resíduos"

Nivel2, Nivel3, Nivel4, Nivel5 e Nivel6 - Especificação da atividade emissora/removedora de GEE. Caso não haja descrição específica da atividade a partir do Nivel2 o registro será NULL ou como célula vazia.

Emissao_Remocao_Bunker - Classificação à qual o GEE se refere entre "Emissão", "Remoção", "Emissão NCl", "Remoção NCl" e Bunker

Gas - Tipo de GEE a que se faz referência

AtividadeEconomica - Atividade econômica à qual a emissão/remoção de GEE faz referência

Produto - Produto ao qual a emissão/remição de GEE faz referência

a1970-a2021 - Valor de emissão/remoção/bunker de GEE para o respectivo ano


# Carga

O ETL foi realizado utilizando o sistema Google Cloud Storage. Foram realizadas cargas de duas maneiras, criando buckets no Cloud Storage e cargas manuais de tabelas para o Big Query:

![image](https://github.com/Guest1537/mvp1/assets/143922275/0b8bd6df-3e73-425d-bd32-b339bb4a95a6)

Dados.de.atividade.BR.csv - Tabela Dados de Atividade BR

Dados.de.atividade.UF.csv - Tabela Dados de Atividade UF

Dados.mudancas.de.uso.da.terra.csv - Dados Mudanças de Uso da Terra

GEEBrasil csv.csv - Dados de Emissões de Gases de Efeito Estufa no Brasil

![image](https://github.com/Guest1537/mvp1/assets/143922275/b67ae324-672a-4c25-ba18-34d09c6b7818)



![image](https://github.com/Guest1537/mvp1/assets/143922275/202f9aa6-cc4e-4fcc-86a5-e875d5a96c4d)

![image](https://github.com/Guest1537/mvp1/assets/143922275/af28bdf1-c1e0-4132-90a2-019d7dcef0a0)

At_BR - Tabela Dados de Atividade BR

At_UF - Tabela Dados de Atividade UF

GE_MUT - Dados Mudanças de Uso da Terra

GE_BR - Dados de Emissões de Gases de Efeito Estufa no Brasil

GE_UF - Foi selecionada amostra de outra tabela disponível pelo SEEG, referente à emissão por UF, mas seu volume de dados e os gastos com espaço alocado foram contra o uso dela para análises na íntegra.


Para algumas tabelas foi necessário editar os dados manualmente devido à leitura dos valores de emissão de GEEs dos respectivos anos serem em STRING em vez de NUMERIC ou FLOAT64. Foi utilizada a seção "Esquema" para tal.

##### Foi criada a "Instancia1"

![image](https://github.com/Guest1537/mvp1/assets/143922275/b45b6e18-fb90-4efa-80ce-f07a15ca4a94)

##### Foram testados alguns Jobs para execução, mas sem sucesso.

![image](https://github.com/Guest1537/mvp1/assets/143922275/fb7feb9c-07f7-4b19-b206-86e0c9f0a386)

Os testes mais relevantes foram MVPv2 e MVPv3:

  - MVP2

Foram realizadas alterações no Job entre os testes.

![image](https://github.com/Guest1537/mvp1/assets/143922275/3d4a8a70-c867-44bd-a60c-1536e0f7db75)

A última versão tentativa (1) excluir a coluna "Territorio", (2-53) alterar os registros das emissões dos anos na tabela GEE_Brasil de STRING para FLOAT, (54) filtrar a coluna "Emiss_o_Remo__o_Bunker" para mostrar apenas casos de emissões e (55) filtrar a coluna "Nivel1_Setor" para mostras apenas os casos de emissões referentes a "Resíduos".

![image](https://github.com/Guest1537/mvp1/assets/143922275/24390b17-718a-479f-b66c-6316c56c9736)

Finalizando por inserir os dados em um Big Query. Com "Truncate Table = TRUE" e "Update Table Scheme = TRUE", que não é visível abaixo.

![image](https://github.com/Guest1537/mvp1/assets/143922275/3c7442b8-080b-4742-b63c-3e9813b5e449)


  - MVP3

Foi tentado um Job simples, sem alteração nenhuma na tabela, porém também não retornou sucesso.

![image](https://github.com/Guest1537/mvp1/assets/143922275/f89fda7b-c75a-41e8-83c7-1c7460730fca)

A única alteração nesse caso foi a alteção manual do tipo de variável referente aos anos de emissões, de STRING para FLOAT:

![image](https://github.com/Guest1537/mvp1/assets/143922275/f0463128-90ed-46e2-a345-780145db49e2)


# Análise

Tendo em vista o insucesso das tentativas com o Cloud Data Fusion (maiores informações na parte de autocrítica), foram realizadas consultas através do Big Query > Espaço de trabalho SQL, com BI gerada através da]o Looker Studio.

![image](https://github.com/Guest1537/mvp1/assets/143922275/ae56fce3-4424-45f2-8656-12c58822d7ba)

#### SUMÁRIO CONSULTAS
01. CONSULTA_TOPMUT_ANO - Setor e valor que apresentaram maiores emissões de cada ano referente à Mudança de Uso da Terra

02. COUNT GE Ano - Criação de tabela para análise de dados incompletos (GE_UF), não será apresentada

03. CREATETABLE_INSERT_VIEW_TOP_EMISS_ANO_BIOMA - Verificação sobre a evolução das emissões anuais de cada bioma brasileiro 

04. CREATE_TABLE_ATBR+UF - Criação básica de tabela por JOIN

05. CREATE_TABLE_TOP10EMISS_ANO - Top 10 emissões de GEE do Brasil 1970-2021, segundo estimativas do SEEG

06. CreateViewAtBRTop1000Valores - Quais e quando os picos de produção das atividades contempladas? 

07. JOIN_GEEBR ATBR - JOIN entre as tabelas At_BR e At_UF, visualização da participação da produção de cada UF para cada atividade contemplada - em progresso

08. TopProducaoPorSetorSeriaHistorica - Valores complementares aos apresentados na consulta nº 06

As consultas supracitadas serão tratadas por sua respectiva numeração na seção "Solução do problema" .


##### Qualidade dos dados

Durante as consultas abaixo foi realizada utilização de restrição para validar e verificar a integridade dos dados gerados nos dados produzidos como resultado da consulta 06, onde se seleciona apenas tuplas onde top1000Valores.Setor <> 'NULL'.


# Solução do problema


#### 01. CONSULTA_TOPMUT_ANO

Link: https://console.cloud.google.com/bigquery?sq=162859265101:ad6629fb012044ccaf8ab7cef5faf02a

Maior emissão do período: 2019 - Amazônia - 84067630.08

![image](https://github.com/Guest1537/mvp1/assets/143922275/4457f68a-2857-4865-b1dd-8c99cae10cdb)

![image](https://github.com/Guest1537/mvp1/assets/143922275/4bca0c5a-0009-42c5-ac6d-cdf55bae09dd)


#### 02. COUNT GE - Criação de tabela para análise de dados incompletos (GE_UF), não será apresentada

![image](https://github.com/Guest1537/mvp1/assets/143922275/10370b76-37d2-462d-8174-d4e75d6dd15c)


#### 03. CREATETABLE_INSERT_VIEW_TOP_EMISS_ANO_BIOMA - Verificação sobre a evolução das emissões anuais de cada bioma brasileiro 

Link: ![image](https://github.com/Guest1537/mvp1/assets/143922275/8fc3c9fd-f94f-4a99-a28b-41a657bdcd2c)

![image](https://github.com/Guest1537/mvp1/assets/143922275/bb31f917-6819-4977-9628-db7b856f9cd7)

Instrução 2 - criação da tabela "AnoBiomaValor" e suas colunas AAno, ABioma e AValor e definição de suas Primary Keys

Instrução 3 - inserção manual de dados e anos na tabela

Instrução 5 - criação de view "AnoBiomaMediaValor" agrupando anos e biomas e somando os respectivos valores

Instrução 7 - criação de tabela "AnoBiomaMediaValor1" agrupando anos e biomas e somando os respectivos valores

Instrução 8 a 12 - seleção dos Biomas e Valores de emissões por ano

Solução usando Looker Studio:

![image](https://github.com/Guest1537/mvp1/assets/143922275/d5813503-1fca-4523-ab79-dcd8d90aebef)
![image](https://github.com/Guest1537/mvp1/assets/143922275/75673929-34ba-4758-8e8b-eae58f07883b)
![image](https://github.com/Guest1537/mvp1/assets/143922275/5ff14874-59d4-433f-9e2f-c58c7365d5f1)
![image](https://github.com/Guest1537/mvp1/assets/143922275/28982820-e934-4e7e-b9b1-41d92e01ae89)
![image](https://github.com/Guest1537/mvp1/assets/143922275/f6e0550b-0b1a-44d8-898a-edf04b863668)


#### 04. CREATE_TABLE_ATBR+UF - Criação básica de tabela por JOIN

Link: https://console.cloud.google.com/bigquery?sq=162859265101:b3214e251da247b1bbe03f6280642399

Criação de tabela com a seleção das colunas Ano, Setor, Descri__o, UF, Valor da produção em todo Brasil e para cada UF, para possível exploração com a participação de cada estado na produção brasileira anual de cada atividade produtiva contemplada

![image](https://github.com/Guest1537/mvp1/assets/143922275/a803f39a-0590-4d58-8cdf-cd8c45fabd15)
![image](https://github.com/Guest1537/mvp1/assets/143922275/58a51d68-dc57-45f9-acdd-b928a3a6edea)


#### 05. CREATE_TABLE_TOP10EMISS_ANO - Top 10 emissões de GEE do Brasil 1970-2021, segundo estimativas do SEEG

Link: https://console.cloud.google.com/bigquery?sq=162859265101:b393c2f625f64bfeb9caeaa723a9cec2

Instrução 02 - Cria tabela A1, que conterá os valores

Instrução 03 - Adiciona uma coluna para cada ano da série

Instrução 04 - Define as colunas de anos inseridas na Instrução 03 para 0

Instrução 05 a 55 - Seleciona as 10 maiores valores de emissão de GEE para cada ano da série

![image](https://github.com/Guest1537/mvp1/assets/143922275/0805b161-fb5c-49c5-9243-1a7c6345d9d9)

Solução usando Looker Studio:

##### (I) Quais são as 10 principais atividades mais emissoras de GEE no Brasil durante o período?

![image](https://github.com/Guest1537/mvp1/assets/143922275/6bb65e01-bf5d-4e7a-968e-6e4b08fc24fe)

Exploração possível em: https://lookerstudio.google.com/reporting/3a0837bc-a8ec-4744-b821-a29bef1beee5


#### 06. CreateViewAtBRTop1000Valores

Link: https://console.cloud.google.com/bigquery?sq=162859265101:819b0c1714904efb895ce382b618b14e

Instrução 01 - Cria view topValores com instância "ordenaValores" que ordena as variáveis, instância "selecionatopProducoes" que agrupa os registros e seleciona e ordena os maiores valores

Instrução 02 - seleciona os valores da view topvalores (consulta)

Instrução 03 - agrupa os registros Setor e Descri____o onde Setor não é 'NULL', conta a quantidade de registros Setor e apresenta os maiores registros "Valor"

![image](https://github.com/Guest1537/mvp1/assets/143922275/a2fb94ce-a636-4412-a8c8-1a98d6dcaa07)

Solução usando Looker Studio:

##### Quais e quando os picos de produção das atividades contempladas? 
![image](https://github.com/Guest1537/mvp1/assets/143922275/518b995c-a322-4c52-91a4-55c9ad80cd91)

Exploração possível em: https://lookerstudio.google.com/reporting/e2107ac0-e777-471a-b0b9-7f59e58da515

A repetição de "Descri____o" por "Ano" na tabela da direita é explicada pela aparição de uma mesma "Descri____o" em dois diferetentes "Setor"


#### 07. JOIN_GEEBR ATBR - em progresso

Link: https://console.cloud.google.com/bigquery?sq=162859265101:5daa668006b9445c91644408d6deb7a0

![image](https://github.com/Guest1537/mvp1/assets/143922275/e3f1bb2d-c2cd-4348-a612-0a06b923954e)



#### 08. TopProducaoPorSetorSeriaHistorica - valores das maiores produções por setor 1990-2021

Link: https://console.cloud.google.com/bigquery?sq=162859265101:f84c5d6a70614841b310a2d4d9cd463d

![image](https://github.com/Guest1537/mvp1/assets/143922275/0f3574dd-6e86-4833-bd25-6ca1022e87a1)

Através das instâncias "seleciona" (que remove os registros null e seleciona os valores máximos de cada setor, descrição e unidade, renomeada "A") e anosRef (que seleciona todos os anos e respectivos valores renomeada "B"), se seleciona o ano, setor e unidade onde o valor da instância A é igual ao da intância B

##### Consulta complementa dados encontrados na consulta nº 06 (Pergunta III)

Solução usando Looker Studio: ![image](https://github.com/Guest1537/mvp1/assets/143922275/bd4fa655-4053-4b56-9220-8a720cff24ea)

Exploração possível em: https://lookerstudio.google.com/reporting/a1ef459c-0609-49df-97a9-4a8f987ae4d7


# Autocrítica

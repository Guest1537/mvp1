# MVP Engenharia de Dados
Pedro Caleffi Barbosa

# Objetivo
Explorar e analisar dados disponíveis na base do Sistema de Estimativas de Emissões e Remoções de Gases de Efeito Estufa (SEEG). 

# Busca pelos dados
Seleção do arquivo "ATIVIDADE_SEEG10_TODOS_SETORES_2022.10.23"

https://seeg.eco.br/download/

Em: TABELA DE DADOS DE ATIVIDADE - BRASIL E ESTADOS (SEEG10)
![image](https://github.com/Guest1537/mvp1/assets/143922275/3459ef67-f960-4ba7-9f5e-36de8fcf6c7c)

Em 26/09/2023 às 21:23 o link para download da tabela selecionada no site estava quebrado.
Arquivo também disponível para download em: https://docs.google.com/spreadsheets/d/1Qby5NARoUhZdUbmauSw5sHaVK6qnRKjM/edit?usp=sharing&ouid=117863055539952818718&rtpof=true&sd=true 

/Seleção das tabelas "Dados de Atividade BR", "Dados de Atividade UF" e "Dados Mudanças de Uso da Terra"
![image](https://github.com/Guest1537/mvp1/assets/143922275/17d74460-10aa-404b-ae53-f958789608b0)

Criação de tabelas individuais:
Dados de Atividade BR -> Dados.de.atividades.BR - link para download do google drive: https://drive.google.com/file/d/1v2n61Z0ohyJr4eVc9iFx-fNKp4mdAIBE/view?usp=drive_link

Dados de Atividade UF -> Dados.de.atividade.UF - link para download do google drive: https://drive.google.com/file/d/12wLLh8iTZx-zahf_qrM8qbJrYO08s_c1/view?usp=drive_link

Dados Mudanças de Uso da Terra -> Dados.mudancas.de.uso.de.terra - link para download do google drive: https://drive.google.com/file/d/1h1NAL4hrh0KdyzYUmqFLnySVH31eKJY2/view?usp=drive_link

Abaixo, imagens das respectivas tabelas antes de ser transformada em csv:

![image](https://github.com/Guest1537/mvp1/assets/143922275/1fb0ed15-df9d-4cc5-bb72-65d63931c56d)

![image](https://github.com/Guest1537/mvp1/assets/143922275/f10e4b42-19a6-4d63-90d4-91473637ae6b)

![image](https://github.com/Guest1537/mvp1/assets/143922275/77a23392-9c83-40ed-8858-95173252c4c5)


# Coleta
Dados baixados para a máquina local e inseridos manualmente em um bucket (mvpgee) do Google Cloud

![image](https://github.com/Guest1537/mvp1/assets/143922275/6de4291d-0656-4c6c-9616-afc561fc098f)

![image](https://github.com/Guest1537/mvp1/assets/143922275/41f37f5a-8c27-499e-92b4-be8fbd180670)

Exemplo de upload para o bucket (mvpgee) utilizando o terminal Cloud Shell

![image](https://github.com/Guest1537/mvp1/assets/143922275/af18d1bc-0470-42c6-b335-6e3b3ee25c36)




# Modelagem

Dados de Atividade BR e Dados de Atividade UF
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

Dados Mudanças de Uso da Terra
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

# Carga

# Análise

Qualidade dos dados

# Solução do problema



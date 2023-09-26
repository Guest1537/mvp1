# MVP Engenharia de Dados
Pedro Caleffi Barbosa

# Objetivo
Explorar e analisar dados disponíveis na base do Sistema de Estimativas de Emissões e Remoções de Gases de Efeito Estufa (SEEG). 

# Busca pelos dados
Seleção do arquivo "ATIVIDADE_SEEG10_TODOS_SETORES_2022.10.23"

https://seeg.eco.br/download/

Em: TABELA DE DADOS DE ATIVIDADE - BRASIL E ESTADOS (SEEG10)
![image](https://github.com/Guest1537/mvp1/assets/143922275/3459ef67-f960-4ba7-9f5e-36de8fcf6c7c)

Seleção das tabelas "Dados de Atividade BR", "Dados de Atividade UF" e "Dados Mudanças de Uso da Terra"
![image](https://github.com/Guest1537/mvp1/assets/143922275/17d74460-10aa-404b-ae53-f958789608b0)

Criação de tabelas individuais:
Dados de Atividade BR -> !T.Dados de Atividade BR csv
Dados de Atividade UF -> !T.Dados de Atividade UF csv
Dados Mudanças de Uso da Terra -> !T.Dados Mudancas de Uso da Terra csv

Abaixo, imagens das respectivas tabelas antes de ser transformada em csv:

![image](https://github.com/Guest1537/mvp1/assets/143922275/1fb0ed15-df9d-4cc5-bb72-65d63931c56d)

![image](https://github.com/Guest1537/mvp1/assets/143922275/f10e4b42-19a6-4d63-90d4-91473637ae6b)

![image](https://github.com/Guest1537/mvp1/assets/143922275/77a23392-9c83-40ed-8858-95173252c4c5)


# Coleta
Dados baixados para a máquina local e inseridos manualmente em um bucket (mvpgee) do Google Cloud

![image](https://github.com/Guest1537/mvp1/assets/143922275/6de4291d-0656-4c6c-9616-afc561fc098f)

![image](https://github.com/Guest1537/mvp1/assets/143922275/17685acd-dfe3-4266-8b4d-ee8b6fb14024)

# Modelagem

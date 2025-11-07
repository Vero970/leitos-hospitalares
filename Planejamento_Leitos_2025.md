# 📘 Planejamento - Sistema de Monitoramento Leitos Hospitalares (Leitos 2025)

## 1. Definição do Problema

A gestão de leitos hospitalares é um desafio recorrente para a administração pública, especialmente em situações de alta demanda e emergências sanitárias.  
Há uma necessidade de consolidar informações de diferentes hospitais e regiões para **acompanhar a ocupação, identificar déficits e otimizar recursos**.

O problema central é a **ausência de um sistema integrado de monitoramento e apoio à decisão** que permita visualizar, prever e agir de forma eficiente sobre a disponibilidade de leitos hospitalares.

### 🎯 Objetivo do Projeto

Desenvolver um **sistema simples de análise e visualização de dados** que possibilite:

- Acompanhar, em tempo real, a disponibilidade e ocupação de leitos.  
- Detectar gargalos (superlotação ou falta de leitos).  
- Fornecer relatórios e previsões de curto prazo para gestores públicos.  
- Emitir alertas automáticos de criticidade para apoiar decisões rápidas.

O foco analítico será nos municípios de **Campinas**, **Americana** e **Valinhos**, utilizando o dataset completo de leitos disponíveis no estado.

---

## 2. Descrição do Dataset

**Fonte:** [OpenDataSUS – 2025](https://opendatasus.saude.gov.br/dataset/hospitais-e-leitos)  
**Arquivo:** `Leitos_2025.csv`  
**Formato:** CSV (separador `;`)  
**Tamanho:** Aproximadamente 65 mil registros  

### Campos principais

| Campo | Descrição |
|-------|------------|
| `MUNICIPIO` | Nome do município |
| `CNES` | Código do estabelecimento de saúde |
| `NOME_FANTASIA` | Nome do hospital ou unidade |
| `LEITOS_EXISTENTES` | Número total de leitos cadastrados |
| `LEITOS_SUS` | Quantidade de leitos destinados ao SUS |
| `UTI_ADULTO_EXIST` | Leitos de UTI adulto existentes |
| `UTI_NEONATAL_EXIST` | Leitos de UTI neonatal existentes |
| `DATA_ATUALIZACAO` | Data de atualização do registro |

---

## 3. Requisitos

### 3.1 Requisitos Funcionais

| ID | Descrição |
|----|------------|
| RF01 | Coletar e armazenar o dataset de leitos no Azure Blob Storage. |
| RF03 | Gerar indicadores de ocupação e disponibilidade por município e tipo de leito. |
| RF04 | Disponibilizar relatórios e dashboards interativos no Power BI. |
| RF05 | Implementar alertas automáticos quando a taxa de ocupação ultrapassar 90%. |
| RF06 | Permitir previsão simples de demanda (curto prazo) via modelos estatísticos. |
---


## 4. Diagrama de Arquitetura do Sistema

![Diagrama de Arquitetura do Sistema](diagrama_arquitetura.png)

*Fluxo do sistema: o dataset é coletado do OpenDataSUS, processado e armazenado na nuvem Azure, e visualizado no Power BI pelos gestores públicos.*



## 5. Modelo de Dados
- Modelo Relacional Simplificado
Tabela	Descrição	Campos Principais
dim_municipio	Informações de cada município	id_municipio, nome, regiao_saude, populacao
dim_hospital	Cadastro dos hospitais/unidades	id_hospital, nome, cnes, municipio_id, esfera_administrativa
dim_tipo_leito	Tipos de leitos cadastrados	id_tipo, descricao, tipo_uti, is_sus
fato_ocupacao	Dados diários de leitos ocupados/disponíveis	data, hospital_id, tipo_leito_id, leitos_existentes, leitos_ocupados, taxa_ocupacao

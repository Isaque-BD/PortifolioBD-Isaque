# Portfólio APIs — Banco de Dados · Isaque de Souza

## Introdução

Estou cursando Banco de Dados desde o segundo semestre de 2023 e atualmente atuo como analista de dados na Johnson & Johnson. No dia a dia, trabalho com tecnologias como Python, SQL, AWS (Databricks), SAP ERP, Power BI e Excel para desenvolver pipelines de ETL, otimizando o fluxo e a qualidade dos dados. Além disso, elaboro relatórios de produtividade, disponibilidade e performance de máquinas, fornecendo insumos estratégicos para a tomada de decisões e a promoção de melhorias contínuas nos processos de fabricação.

## Contatos

- [LinkedIn](https://www.linkedin.com/in/seu-usuario)
- [GitHub](https://github.com/Isaque-BD)

## Principais Conhecimentos

Java · Spring Boot · SQL

---

## Menu de Semestres

| Semestre | Ano | Projeto |
|----------|-----|---------|
| [1º Semestre](#1º-semestre--2023) | 2023 | Introdução à Programação |
| [2º Semestre](#2º-semestre--2023) | 2023 | PBLTeX — Sistema de Gestão Acadêmica |
| [3º Semestre](#3º-semestre--2024) | 2024 | Análise de Climas de Regiões |
| [4º Semestre](#4º-semestre--2024) | 2024 | GSW Soluções Integradas |

---

## 1º Semestre · 2023

**Tema:** Introdução à Programação

Semestre inicial do curso de Banco de Dados, com foco nos fundamentos de algoritmos e lógica de programação, além do aprendizado das primeiras ferramentas de desenvolvimento colaborativo.

### Tecnologias Utilizadas

- **Python** — Lógica e estrutura de algoritmos
- **Trello** — Gerenciamento de tarefas
- **GitHub** — Versionamento de código

### Aprendizados Efetivos

Nesse semestre aprendi os conceitos de algoritmos e como utilizar o GitHub para versionamento do código.

### Hard Skills

| Tecnologia/Metodologia | Nota | Classificação |
|------------------------|------|---------------|
| Python | ★★☆☆☆ | Sei fazer com ajuda |
| GitHub | ★★★☆☆ | Entendi |

### Soft Skills

| Habilidade | Descrição |
|------------|-----------|
| Conhecimento | Tive bastante autonomia para realizar minhas tasks, fazendo bastante pesquisas para cada dúvida que tive. |
| Comunicação | No grupo tivemos conflitos devido ao desbalanceamento na atuação prática de cada um, tendo alguns fazendo mais que os outros. |

---

## 2º Semestre · 2023

**Tema:** PBLTeX — Sistema de Gestão Acadêmica

O desafio proposto foi desenvolver um sistema para uma instituição de ensino com diferentes níveis de permissão (admin, professor e aluno), cada um com acesso limitado. O sistema permite criar turmas, cadastrar alunos, criar grupos e definir notas por ciclo.

**Repositório:** [API-Porygon](https://github.com/Isaque-BD/API-Porygon)

### Tecnologias Utilizadas

- **Python** — Desenvolvimento de toda a lógica do sistema
- **Trello** — Gerenciamento de tasks da equipe
- **GitHub** — Versionamento do código
- **Excel** — Armazenamento dos dados

### Contribuições Pessoais

<details>
<summary>Relatório (Dashboard de Turmas)</summary>

O código Python utiliza as bibliotecas `streamlit`, `pandas` e `plotly.express` para criar um aplicativo web interativo de relatório de turmas a partir de dados em um arquivo Excel (`infodados.xlsx`).

**Funcionalidades:**
- Carregamento e seleção de planilhas por turma
- Filtros interativos por ciclo e por aluno
- Geração de gráficos de barras (nota por ciclo e média por aluno)
- Exibição dos dados filtrados em tabela

```python
import streamlit as st
import pandas as pd
import plotly.express as px

def carregar_dados_excel():
    excel_file = pd.ExcelFile("infodados.xlsx")
    sheet_names = excel_file.sheet_names
    return excel_file, sheet_names

def filtrar_planilhas_turma(excel_file, sheet_names):
    keywords = ["turma", "classe", "grupo"]
    turma_sheets = [
        sheet_name for sheet_name in sheet_names
        if any(keyword in sheet_name.lower() for keyword in keywords)
        and "fechada" not in sheet_name.lower()
    ]
    return turma_sheets

def selecionar_planilha_turma(turma_sheets):
    return st.sidebar.selectbox("Selecione a turma:", turma_sheets)

def aplicar_filtro_alunos(df_turma):
    alunos_unicos = df_turma["Alunos"].unique()
    select_all_button = st.sidebar.checkbox("Todos os alunos")
    if select_all_button:
        return alunos_unicos
    return st.sidebar.multiselect("Selecione os alunos:", alunos_unicos)

def filtrar_dataframe(df_turma, alunos_selecionados, selected_ciclo):
    return df_turma[df_turma["Alunos"].isin(alunos_selecionados)][
        ["Alunos", selected_ciclo, "Média", "Professores", "Início do Curso", "Fim do Curso"]
    ]

def criar_graficos(df_selecao, selected_ciclo):
    col1, col2 = st.columns(2)
    col1.plotly_chart(px.bar(df_selecao, x="Alunos", y=selected_ciclo, title=f"Nota do {selected_ciclo} por aluno"))
    col2.plotly_chart(px.bar(df_selecao, x="Alunos", y="Média", title="Média por aluno"))

st.set_page_config(layout="wide", page_title="Relatórios gerais", page_icon=":bar_chart:")
st.title("Relatório das Turmas")

excel_file, sheet_names = carregar_dados_excel()
turma_sheets = filtrar_planilhas_turma(excel_file, sheet_names)
selected_sheet = selecionar_planilha_turma(turma_sheets)
df_turma = pd.read_excel("infodados.xlsx", sheet_name=selected_sheet)
colunas_ciclo = [c for c in df_turma.columns if c.lower().startswith("ciclo")]
selected_ciclo = st.sidebar.selectbox("Selecione o ciclo:", colunas_ciclo)
alunos_selecionados = aplicar_filtro_alunos(df_turma)
df_selecao = filtrar_dataframe(df_turma, alunos_selecionados, selected_ciclo)
criar_graficos(df_selecao, selected_ciclo)
st.dataframe(df_selecao)
```

</details>

<details>
<summary>Ciclo de Entrega</summary>

Script Python com `openpyxl` para gerenciar e estruturar datas de cursos e ciclos dentro de um arquivo Excel.

**Funcionalidades:**
- Seleção de turma por planilha
- Definição e validação de datas de início e término do curso
- Criação de ciclos simétricos ou personalizados
- Registro automático das datas na planilha

```python
import openpyxl
from datetime import datetime, timedelta

def adicionar_data_e_ciclos(planilha, turma_destino):
    aba_turma = planilha[turma_destino]
    ciclos = []

    while True:
        try:
            data_inicio = datetime.strptime(input("Data de início do curso (DD/MM/AAAA): "), "%d/%m/%Y")
            data_fim = datetime.strptime(input("Data de término do curso (DD/MM/AAAA): "), "%d/%m/%Y")
            if data_fim < data_inicio:
                print("Data de término anterior à de início.")
            else:
                break
        except ValueError:
            print("Formato inválido. Use DD/MM/AAAA.")

    qtd_ciclos = int(input("Quantos ciclos? "))
    # ... (lógica de criação simétrica ou manual)

    planilha.save('infodados.xlsx')
    print("Datas e ciclos adicionados com sucesso!")
```

</details>

### Aprendizados Efetivos

Aprendi os conceitos de algoritmos e como utilizar o GitHub para versionamento do código.

### Hard Skills

| Tecnologia/Metodologia | Nota | Classificação |
|------------------------|------|---------------|
| Python | ★★☆☆☆ | Sei fazer com ajuda |
| GitHub | ★★★☆☆ | Entendi |

### Soft Skills

| Habilidade | Descrição |
|------------|-----------|
| Conhecimento | Bastante autonomia para realizar as tasks, com pesquisas para cada dúvida. |
| Comunicação | Conflitos no grupo devido ao desbalanceamento na atuação prática de cada membro. |

---

## 3º Semestre · 2024

**Tema:** Análise de Climas de Regiões

O desafio proposto foi desenvolver uma aplicação para análise de climas de regiões (temperatura, umidade), possibilitando calcular médias de períodos para apoio à tomada de decisões — como, por exemplo, escolher o que plantar em uma fazenda para determinada região.

**Repositório:** [API-2-semestre](https://github.com/Isaque-BD/API-2-semestre)

### Tecnologias Utilizadas

- **Java** — Linguagem principal para toda a lógica da aplicação
- **JavaFX** — Desenvolvimento da interface gráfica
- **Scene Builder** — Facilitou o desenvolvimento das telas
- **PostgreSQL** — Banco de dados relacional para armazenamento dos dados
- **GitHub** — Versionamento e gestão do código

### Contribuições Pessoais

<details>
<summary>Conexão com o Banco de Dados</summary>

A classe `DbConnection` gerencia a conexão com o banco PostgreSQL via JDBC, encapsulando as operações básicas de conexão e execução de comandos SQL.

```java
package javalee.com.bd_connection;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import javalee.com.configs.*;

public class DbConnection {

    private Connection conn;

    public DbConnection() {
        ConfigBdReader config = new ConfigBdReader();
        try {
            Class.forName("org.postgresql.Driver");
            this.conn = DriverManager.getConnection(
                config.getUrlBd() + config.getNameBd(),
                config.getUserBd(),
                config.getPasswordBd()
            );
        } catch (Exception e) {
            System.out.println(e);
        }
    }

    public void Desconnect() {
        try {
            if (this.conn != null) this.conn.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }

    public void Save(String comando) {
        try {
            PreparedStatement stm = this.conn.prepareStatement(comando);
            stm.execute();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

</details>

<details>
<summary>Entidade Metric</summary>

Classe de entidade simples para representar registros de métricas em banco de dados ou em memória.

```java
package javalee.com.entities;

public class Metric {

    private int idMetrica;
    private String codigo;

    public Metric(int idMetrica, String codigo) {
        this.idMetrica = idMetrica;
        this.codigo = codigo;
    }

    public Metric(String codigo) {
        this.codigo = codigo;
    }

    public String getIdMetrica() { return String.valueOf(idMetrica); }
    public void setIdMetrica(int idMetrica) { this.idMetrica = idMetrica; }
    public String getCodigo() { return codigo; }
    public void setCodigo(String codigo) { this.codigo = codigo; }
}
```

</details>

### Aprendizados Efetivos

Aprendi a estrutura de um sistema simples de CRUD e como funciona a integração entre banco de dados e aplicação.

### Hard Skills

| Tecnologia/Metodologia | Nota | Classificação |
|------------------------|------|---------------|
| Java | ★★★☆☆ | Sei fazer com ajuda |
| PostgreSQL | ★★★☆☆ | Entendi |
| GitHub | ★★★☆☆ | Sei fazer com ajuda |
| SceneBuilder | ★★★☆☆ | Entendi |
| JavaFX | ★★★☆☆ | Entendi |

### Soft Skills

| Habilidade | Descrição |
|------------|-----------|
| Proatividade | Estudei bastante sobre Java, SceneBuilder, JavaFX e PostgreSQL para realizar as integrações. |
| Conhecimento | Precisei pedir bastante ajuda ao time durante o desenvolvimento das tasks. |
| Comunicação | Precisei me comunicar sobre minhas dificuldades ao longo do desenvolvimento. |

---

## 4º Semestre · 2024

**Tema:** GSW Soluções Integradas — Análise Estratégica com Web Data

A GSW Soluções Integradas propôs o desafio de desenvolver uma página web para análises estratégicas com foco em histórico de informações. O sistema utiliza dados de outros sites (portais de notícias, por exemplo) para realizar previsões conforme a necessidade do usuário — como análise do crescimento de criptomoedas com base em notícias ou previsão do tempo.

**Repositório:** [Morpheus — GSW Soluções Integradas](https://github.com/Morpheus-Fatec/morpheus/tree/main)

### Tecnologias Utilizadas

- **Java** — Toda a lógica do projeto
- **MySQL** — Armazenamento e cruzamento dos dados para análises
- **Vue** — Interface para interação do usuário
- **GitHub** — Versionamento do projeto
- **Discord** — Comunicação da equipe
- **VSCode** — Ambiente de desenvolvimento
- **Maven** — Gerenciamento de dependências

### Contribuições Pessoais

<details>
<summary>Método de Filtro de Autores</summary>

Endpoint que retorna todos os autores cadastrados no sistema, com nome e ID, usando o padrão DTO para expor apenas as informações necessárias.

```java
@Service
public class NewsAuthorService {

    @Autowired
    private NewsAuthorRepository newsAuthorRepository;

    public List<NewsAuthorDTO> getAllAuthors() {
        return newsAuthorRepository.findAll().stream()
            .map(author -> new NewsAuthorDTO(author.getAutId(), author.getAutName()))
            .collect(Collectors.toList());
    }
}
```

</details>

<details>
<summary>Criação de Endpoints</summary>

Classe DTO para representar um endpoint de API com código, endereço, origem e método HTTP.

```java
public class ApiEndpointDTO {
    private int code;
    private String address;
    private String source;
    private String method;

    public void setMethod(int post, int get) {
        if (post == 1) {
            this.method = "POST";
        } else if (get == 1) {
            this.method = "GET";
        }
    }
}
```

</details>

<details>
<summary>Modelagem de Banco de Dados</summary>

Estrutura SQL para cadastro, atualização e gerenciamento de fontes de dados de APIs, com suporte a categorização por tags.

```sql
-- Armazena informações básicas sobre APIs
CREATE TABLE Api (
    api_cod  INT AUTO_INCREMENT PRIMARY KEY,
    api_name VARCHAR(30)  NOT NULL,
    api_url  VARCHAR(500) UNIQUE NOT NULL
);

-- Relação muitos-para-muitos entre Api e Tag
CREATE TABLE Api_tag (
    api_cod INT,
    tag_cod INT,
    PRIMARY KEY (api_cod, tag_cod),
    FOREIGN KEY (api_cod) REFERENCES Api(api_cod),
    FOREIGN KEY (tag_cod) REFERENCES Tag(tag_cod)
);

-- Armazena dados coletados de uma API ao longo do tempo
CREATE TABLE Data_collected_api (
    dat_coll_api_cod           INT AUTO_INCREMENT PRIMARY KEY,
    api_cod                    INT,
    dat_coll_api_registry_date TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    dat_coll_api_content       LONGTEXT,
    FOREIGN KEY (api_cod) REFERENCES Api(api_cod)
);
```

</details>

### Hard Skills

| Tecnologia/Metodologia | Nota | Classificação |
|------------------------|------|---------------|
| Java | ★★★★☆ | Autonomia |
| MySQL | ★★★☆☆ | Entendi |
| Vue | ★★★☆☆ | Sei fazer com ajuda |
| GitHub | ★★★★☆ | Autonomia |

### Soft Skills

| Habilidade | Descrição |
|------------|-----------|
| Comunicação | Fui desenvolvendo ao longo do projeto, perdendo o receio de perguntar dúvidas. |
| Paciência | Mantive o controle em situações inesperadas sem me estressar, fundamental para o trabalho em equipe. |

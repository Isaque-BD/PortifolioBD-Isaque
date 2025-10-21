# Portfólio API's Banco de Dados - Isaque de Souza


## Introdução
Começando pela minha formação, atualmente estou cursando Banco de Dados, na qual eu me ingressei no segundo semestre de 2023, atualmente estou atuando na área de análise de dados na minha profissão, lá na J&J. As as tecnologias de Python, SQL, AWS(Databricks), para realizar querys, SAP ERP, Power BI e Excel, com o conjunto dessas ferramentas desenvolvo ETL para melhoria dos fluxo de dados, e também gerando reports de produtividade, disponibilidade e performance de máquina para que possa ser tomada descisões de melhorias contínuas nos processos de fabricação.

## Contatos
<a href="https://www.linkedin.com/in/seu-usuario" target="_blank">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linkedin/linkedin-original.svg" alt="LinkedIn" width="20" style="vertical-align: middle;"/>
  Linkedin
</a>
<a href="https://github.com/Isaque-BD" target="_blank">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg" alt="GitHub" width="20" style="vertical-align: middle;"/>
  GitHub
</a>

## Principais Conhecimentos

<a href="https://www.java.com" target="_blank">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/java/java-original.svg" alt="Java" width="20" style="vertical-align: middle;"/>
  Java
</a>
<a href="https://spring.io/projects/spring-boot" target="_blank">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/spring/spring-original.svg" alt="Spring Boot" width="20" style="vertical-align: middle;"/>
  Spring Boot
</a>
<a href="https://www.mysql.com" target="_blank">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mysql/mysql-original.svg" alt="SQL" width="20" style="vertical-align: middle;"/>
  SQL
</a>

## Meus Projetos

### Em 2023-2

O desafio proposto foi desenvolver um sistema para uma instituição de ensino, onde teria diferentes níveis de permissão, sendo dividido por admin, professor e aluno, cada um tendo um acesso limitado no sistema, nesse sistema seria possível criar turmas e cadastrar alunos dentro dessas turmas, e dentro do mesmo seria possível criar grupos de alunos para estar avaliando e claro a definição de nota para cada grupo.

[Git do Projeto Concluído - PBLTeX](https://github.com/Isaque-BD/API-Porygon)

### Tecnologias Utilizadas

1 - *Python*: É uma linguagem de programação que foi utilizada para desenvolver toda a lógica do sistema.

3 - *Trello*: Foi utilizado para criar os cards das tasks e estar gerenciando a equipe o que cada um tinha que fazer.

4 - *GitHub*: Ferramenta para versionamento do código e gestão do código.

5 - *Excel*: É uma planilha do microsft office 365 que foi utilizada para estar armazenando os dados.

### Contribuições Pessoais
<details>
<summary>Relatório</summary>

  O código Python utiliza as bibliotecas `streamlit`, `pandas` e `plotly.express` para criar um aplicativo web interativo de **relatório de turmas** a partir de dados em um arquivo Excel (`infodados.xlsx`).

  **Funcionalidades Principais:**

  1.  **Carregamento e Seleção de Dados:**
      * Lê o arquivo Excel e lista suas planilhas.
      * Filtra as planilhas para identificar as que representam turmas (contêm "turma", "classe" ou "grupo" no nome e não contêm "fechada").
      * Permite ao usuário selecionar a **turma** (planilha) através de um menu lateral (`st.sidebar.selectbox`).

  2.  **Filtros Interativos:**
      * Permite selecionar um **ciclo** (`Ciclo X`) para análise.
      * Permite selecionar **alunos** específicos (ou todos) através de um filtro lateral (`st.sidebar.multiselect` e `st.sidebar.checkbox`).

  3.  **Visualização e Análise:**
      * **Filtra** os dados da turma com base nas seleções de alunos e ciclo.
      * Gera dois **gráficos de barras** (`plotly.express`):
          * Nota do ciclo selecionado por aluno.
          * Média geral por aluno.
      * Exibe os dados filtrados em uma **tabela** (`st.dataframe`).

  Em resumo, o código transforma dados de um Excel em um painel interativo (`dashboard`) para visualizar e analisar as notas e médias de alunos por turma e ciclo.

    import streamlit as st
    import pandas as pd
    import plotly.express as px

    def carregar_dados_excel():
        excel_file = pd.ExcelFile("infodados.xlsx")
        sheet_names = excel_file.sheet_names
        return excel_file, sheet_names

    def filtrar_planilhas_turma(excel_file, sheet_names):
        keywords = ["turma", "classe", "grupo"]
        turma_sheets = [sheet_name for sheet_name in sheet_names if any(keyword in sheet_name.lower() for keyword in keywords) and "fechada" not in sheet_name.lower()]
        return turma_sheets

    def selecionar_planilha_turma(turma_sheets):
        selected_sheet = st.sidebar.selectbox("Selecione a turma:", turma_sheets)
        return selected_sheet

    def aplicar_filtro_alunos(df_turma):
        alunos_unicos = df_turma["Alunos"].unique()
        select_all_button = st.sidebar.checkbox("Todos os alunos")
        if select_all_button:
            selected_alunos = alunos_unicos
        else:
            selected_alunos = st.sidebar.multiselect("Selecione os alunos:", alunos_unicos)
        return selected_alunos


    def filtrar_dataframe(df_turma, alunos_selecionados, selected_ciclo):
        df_selecao = df_turma[df_turma["Alunos"].isin(alunos_selecionados)][["Alunos", selected_ciclo, "Média", "Professores", "Início do Curso", "Fim do Curso"]]
        return df_selecao

    def criar_graficos(df_selecao, selected_ciclo):
        col1, col2 = st.columns(2)
        nota_por_aluno = px.bar(df_selecao, x="Alunos", y=selected_ciclo, title=f"Nota do {selected_ciclo} por aluno")
        col1.plotly_chart(nota_por_aluno)
        media_por_aluno = px.bar(df_selecao, x="Alunos", y="Média", title="Média por aluno")
        col2.plotly_chart(media_por_aluno)

    st.set_page_config(layout="wide", page_title="Relatórios gerais", page_icon=":bar_chart:")
    st.sidebar.image("pbltex.jpg", caption="Análise de dados")
    st.title("Relatório das Turmas")

    excel_file, sheet_names = carregar_dados_excel()

    turma_sheets = filtrar_planilhas_turma(excel_file, sheet_names)

    selected_sheet = selecionar_planilha_turma(turma_sheets)

    df_turma = pd.read_excel("infodados.xlsx", sheet_name=selected_sheet)

    colunas_ciclo = [coluna for coluna in df_turma.columns if coluna.lower().startswith("ciclo")]
    selected_ciclo = st.sidebar.selectbox("Selecione o ciclo:", colunas_ciclo)

    alunos_selecionados = aplicar_filtro_alunos(df_turma)

    df_selecao = filtrar_dataframe(df_turma, alunos_selecionados, selected_ciclo)

    criar_graficos(df_selecao, selected_ciclo)

    st.dataframe(df_selecao)
</details>

<details>
<summary>Ciclo de Entrega</summary>
Este código Python, que utiliza a biblioteca `openpyxl`, é um script de console para **gerenciar e estruturar datas de cursos e ciclos** dentro de um arquivo Excel (`infodados.xlsx`).

**Funcionalidades Principais:**

1.  **Seleção de Turma:** O programa lista as planilhas existentes que começam com "Turma " e permite ao usuário escolher em qual delas deseja trabalhar.
2.  **Definição de Datas do Curso:** O usuário insere a data de início e a data de término do curso, que são validadas para garantir a ordem cronológica e registradas na planilha.
3.  **Criação de Ciclos:**
    * Permite definir a quantidade total de ciclos.
    * Oferece duas opções para a criação dos ciclos:
        * **Simétrico:** Divide a duração total do curso igualmente entre a quantidade de ciclos.
        * **Definir Cada Ciclo:** Permite ao usuário inserir manualmente as datas de início e fim para cada ciclo, com validações para garantir que as datas estejam dentro do período total do curso e que os ciclos não se sobreponham.
4.  **Registro na Planilha:** As datas de início e fim do curso, o nome dos ciclos, as datas de início e fim de cada ciclo, e a duração em dias de cada ciclo são salvas diretamente na planilha Excel.

Em resumo, o script automatiza a **estrutura temporal de um curso** ao adicionar e calcular as datas dos ciclos em uma turma específica do arquivo de dados.

    import openpyxl
    from datetime import datetime, timedelta

    def verificar_ciclo(n, x, y):
        if n > x or n < y:
            print("Data está fora do ciclo de curso, tente novamente")
        else:
            pass

    def adicionar_data_e_ciclos(planilha, turma_destino):
        aba_turma = planilha[turma_destino]
        ciclos = []

    while True:
        try:
            data_inicio = datetime.strptime(input("\nDigite a data de início do curso (DD/MM/AAAA): "), "%d/%m/%Y")
            data_fim = datetime.strptime(input("Digite a data de término do curso (DD/MM/AAAA): "), "%d/%m/%Y")
            if data_fim < data_inicio:
                print("A data de término é anterior à data de início, tente novamente")
            else:
                break
        except ValueError:
            print("Formato de data inválido. Use o formato DD/MM/AAAA")

    aba_turma.cell(row=1, column=7).value = "Início do Curso"
    aba_turma.cell(row=1, column=8).value = "Fim do Curso"
    aba_turma.cell(row=2, column=7).value = data_inicio.strftime('%d/%m/%Y')
    aba_turma.cell(row=2, column=8).value = data_fim.strftime('%d/%m/%Y')

    aba_turma.cell(row=1, column=9).value = "Início do Ciclo"
    aba_turma.cell(row=1, column=10).value = "Término do Ciclo"
    aba_turma.cell(row=1, column=11).value = "Dias do Ciclo"

    qtd_ciclos = int(input("\nQuantos ciclos você deseja: "))

    while True:
        choice_cycle_type = input("\nEscolha o tipo do ciclo:\n\n1-Simétrico\n2-Definir cada ciclo\n\nEscolha uma das opções: ")
        if choice_cycle_type == "1" or choice_cycle_type == "2":
            break
        else:
            print("Opção inválida, tente novamente")

    if choice_cycle_type == "1":
        duracao_ciclo = (data_fim - data_inicio) / qtd_ciclos

        for i in range(qtd_ciclos - 1):
            ciclo_nome = f"Ciclo {i + 1}"
            ciclo_inicio = data_inicio + i * duracao_ciclo
            ciclo_fim = ciclo_inicio + duracao_ciclo - timedelta(days=1)
            ciclos.append((ciclo_nome, ciclo_inicio, ciclo_fim))

        ultimo_ciclo_nome = f"Ciclo {qtd_ciclos}"
        ultimo_ciclo_inicio = data_inicio + (qtd_ciclos - 1) * duracao_ciclo
        ultimo_ciclo_fim = data_fim
        ciclos.append((ultimo_ciclo_nome, ultimo_ciclo_inicio, ultimo_ciclo_fim))

    elif choice_cycle_type == "2":
        while True:
            try:
                duracao_ciclo = (data_fim - data_inicio)
                ciclo_datas = []
                ciclo_datas_fim = []

                for i in range(qtd_ciclos):
                    ciclo_nome = f"Ciclo {i + 1}"
                    while True:
                        try:
                            ciclo_inicio = datetime.strptime(input(f"\nDigite a data de início do {ciclo_nome} (DD/MM/AAAA): "), "%d/%m/%Y")
                            if ciclo_inicio < data_inicio or ciclo_inicio > data_fim:
                                print("Data está fora do ciclo de curso, tente novamente")
                            elif ciclo_inicio in ciclo_datas:
                                print("A data de início do ciclo já foi escolhida antes, tente novamente")
                            elif ciclo_inicio < max(ciclo_datas_fim, default=data_inicio):
                                print("A data de início do ciclo deve ser posterior à data de término do ciclo anterior.")
                            else:
                                break
                        except ValueError:
                            print("Formato de data inválido. Use o formato DD/MM/AAAA.")

                    while True:
                        try:
                            ciclo_fim = datetime.strptime(input(f"Digite a data de finalização do {ciclo_nome} (DD/MM/AAAA): "), "%d/%m/%Y")
                            if ciclo_fim < data_inicio or ciclo_fim > data_fim:
                                print("Data está fora do ciclo de curso, tente novamente")
                            elif ciclo_fim in ciclo_datas or ciclo_fim in ciclo_datas_fim:
                                print("A data de término do ciclo já foi escolhida antes, tente novamente")
                            elif ciclo_fim < ciclo_inicio:
                                print("A data de término do ciclo deve ser posterior à data de início do ciclo.")
                            else:
                                break
                        except ValueError:
                            print("Formato de data inválido. Use o formato DD/MM/AAAA.")

                    ciclos.append((ciclo_nome, ciclo_inicio, ciclo_fim))
                    ciclo_datas.append(ciclo_inicio)
                    ciclo_datas_fim.append(ciclo_fim)

                break
            except ValueError:
                print("Formato de data inválido. Use o formato DD/MM/AAAA.")

    for i, (ciclo_nome, ciclo_inicio, ciclo_fim) in enumerate(ciclos):
        aba_turma.cell(row=i + 2, column=9).value = ciclo_inicio.strftime('%d/%m/%Y')
        aba_turma.cell(row=i + 2, column=10).value = ciclo_fim.strftime('%d/%m/%Y')
        dias_ciclo = (ciclo_fim - ciclo_inicio).days + 1
        aba_turma.cell(row=i + 2, column=11).value = dias_ciclo
        print(f"\n{ciclo_nome} terá {dias_ciclo} dias.")

    planilha.save('infodados.xlsx')
    print("\n----Data de início, fim do curso e ciclos adicionados com sucesso!!----")

	planilha = openpyxl.load_workbook('infodados.xlsx')
	
	while True:
	    print("\nOpções:")
	    print("\n1. Adicionar data de início do curso e criar ciclos")
	    print("2. Sair do programa", "\n")

    escolha = input("Escolha uma das opções: ")

    if escolha == '1':
        abas_turmas = [sheet for sheet in planilha.sheetnames if sheet.startswith('Turma ')]

        if not abas_turmas:
            print("\nNão foram encontradas abas de turma na planilha")
        else:
            print("\nTurmas existentes:", "\n")
            for i, turma in enumerate(abas_turmas, start=1):
                print(f"{i}. {turma}")

            num_turma = int(input("\nEscolha o número da turma: "))
            if 1 <= num_turma <= len(abas_turmas):
                turma_desejada = abas_turmas[num_turma - 1]
                adicionar_data_e_ciclos(planilha, turma_desejada)
            else:
                print("\nNúmero de turma inválido.")

    elif escolha == '2':
        break
    else:
        print("Opção inválida. Escolha 1 para adicionar a data de início do curso e criar ciclos ou 2 para sair.")

</details>

### Aprendizados Efetivos

Nesse semestre aprendi os conceitos de algoritmos, e como utilizar o github para versionamento do código.

  <h3 align="center"> Hard Skills </h3>
  <table align="center">
    <tr>
      <th width="270px">Tecnologia/Metodologia</th>
      <th width="85px">Nota</th>
      <th width="200px">Classificação</th>
    </tr>
    <tr>
      <td>Python</td>
      <td>★★☆☆☆</td>
	<td>Sei fazer com ajuda</td>
    </tr>
    <tr>
      <td>GitHub</td>
      <td>★★★☆☆</td>
	<td>Entendi</td>
    </tr>	

  </table>
  
  <h3 align="center">Soft Skills</h3>
  <table align="center">
    <tr>
      <th width="270px">Habilidade</th>
      <th width="280px">Descrição</th>
    </tr>
    <tr>
      <td>Conhecimento</td>
      <td>Tive bastante autonomia para realizar minhas tasks e na utilização das tecnologias, fazendo bastante pesquisas para cada dúvida que eu tive.</td>
    </tr>
    <tr>
      <td>Comunicação</td>
      <td>No grupo tivemos vários conflitos, devido o desbalanceamento devido a atuação prática de cada um na API, tendo alguns fazendo mais que os outros</td>
    </tr>

  </table>


### Em 2024-1
O desafio proposto para esse semestre, foi desenvolver uma aplicação para realizar análises de climas de regiões, como por exemplo temperatura e umidade, sendo possível fazer uma média de um determinado período para tirar conclusões com base nos dados, beneficiando para tomada de decisões, como por exemplo, escolher o que plantar em uma fazendo para aquela região.

[Git do Projeto Concluído - Aplicação de Análise de climas de regiões](https://github.com/Isaque-BD/API-2-semestre)

### Tecnologias Utilizadas

1 - *Java*: Linguagem de programação escolhida para todo desenvolvimento da aplicação

2 - *Java FX*:É a ferramenta utilizada para desenvolvimento da interface da aplicação

3 - *Scene Builder*: Ferramenta que facilitou no desenvolvimento das interfaces

4 - *PostgreSQL*: Banco de dados, open source, utilizado para armazenamento dos dados e relacionamento entre eles.

5 - *GitHub*: Ferramenta utilizada para versionamento e gestão do código.

### Contribuições Pessoais
<details>
  <summary> Conexão com o banco </summary>
  A classe DbConnection é responsável por gerenciar a conexão com o banco de dados PostgreSQL.
Ela utiliza a classe ConfigBdReader para ler as configurações (URL, nome, usuário e senha) e oferece métodos simples para manipular o banco.

Principais funções:

Conectar automaticamente ao banco no construtor.

Desconectar com segurança através do método Desconnect().

Executar comandos SQL (como INSERT, UPDATE e DELETE) com o método Save(String comando).

O código usa JDBC para comunicação com o PostgreSQL e encapsula a lógica básica de conexão, simplificando o uso em outras partes da aplicação.

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
          this.conn = null;

          try {
              Class.forName("org.postgresql.Driver");
              this.conn = DriverManager.getConnection(config.getUrlBd() + config.getNameBd(), config.getUserBd(), config.getPasswordBd());

          } catch (Exception e) {
              System.out.println(e);
          }
      }

      public void Desconnect() {

          try {
              if (this.conn != null) {
                  this.conn.close();
              }
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

</details>

<details>
<summary> Salvar os registros</summary>

A classe Metric representa uma métrica no sistema, contendo um ID e um código identificador.

Principais funções:

Armazena e gerencia os atributos idMetrica e codigo.

Possui dois construtores: um completo (com ID e código) e outro apenas com o código.

Inclui métodos getters e setters para manipular os valores.

Essa classe é usada como entidade simples para representar registros de métricas em banco de dados ou em memória.

    package javalee.com.entities;

    public class Metric {

    private int idMetrica;
    private String codigo;

    public Metric(int idMetrica, String codigo) {
        this.idMetrica = idMetrica;
        this.codigo = codigo;
    }

    public Metric(String codigo){
        this.codigo = codigo;
    }
    
    public String getIdMetrica() {
        return String.valueOf(idMetrica);
    }

    public void setIdMetrica(int idMetrica) {
        this.idMetrica = idMetrica;
    }

    public String getCodigo() {
        return codigo;
    }

    public void setCodigo(String codigo) {
        this.codigo = codigo;
    }

    }

</details>

### Aprendizados Efetivos

Nesse semestre aprendi uma estrutura de um sistema simples de CRUD, e como funciona a integração do banco com a aplicação estarem se comunicando.

  <h3 align="center"> Hard Skills </h3>
  <table align="center">
    <tr>
      <th width="270px">Tecnologia/Metodologia</th>
      <th width="85px">Nota</th>
      <th width="200px">Classificação</th>
    </tr>
    <tr>
      <td>Java</td>
      <td>★★★☆☆</td>
	<td>Sei fazer com ajuda</td>
    </tr>
    <tr>
      <td>PostgreSQL</td>
      <td>★★★☆☆</td>
	<td>Entendi</td>
    </tr>	
    <tr>
      <td>GitHub</td>
      <td>★★★☆☆</td>
	<td>Sei fazer com ajuda</td>
    </tr>
    <tr>
      <td>SceneBuilder</td>
      <td>★★★☆☆</td>
	<td>Entendi</td>
    </tr>
   <tr>
      <td>JavaFX</td>
      <td>★★★☆☆</td>
	<td>Entendi</td>
    </tr>

  </table>
  
  <h3 align="center">Soft Skills</h3>
  <table align="center">
    <tr>
      <th width="270px">Habilidade</th>
      <th width="280px">Descrição</th>
    </tr>
    <tr>
      <td>Proatividade</td>
      <td>Precisei estudar bastante sobre a estrutura de desenvolvimento do Java, SceneBuilder, JavaFX e PostgreSQL para fazer as integrações do sistema.</td>
    </tr>
    <tr>
      <td>Conhecimento</td>
      <td>Precisei pedir bastante ajuda para meu time durante o desenvolvimento das minhas tasks.</td>
    </tr>
    <tr>
      <td>Comunicação</td>
      <td>Precisei me comunicar bastante sobre minhas dificuldades durante o desenvolvimento da aplicação.</td>
    </tr>

  </table>
  

### Em 2024-2
A GSW Soluções Integradas nos propôs o desafio de desenvolver uma página web voltada para análises estratégicas, com foco no armazenamento de históricos de informações. O sistema utilizará dados provenientes de outros sites, como, por exemplo, portais de notícias, para realizar previsões conforme a necessidade do usuário. Um exemplo seria a análise do crescimento de criptomoedas com base nas notícias relacionadas ou a previsão do tempo, entre outras possibilidades.

[GIT do Projeto Concluído - GSW Soluções Integradas](https://github.com/Morpheus-Fatec/morpheus/tree/main)

### Tecnologias Utilizadas
1 - *Java*: Foi essencial para todo desenvolvimento pois, foi com ele que foi feito toda a lógica do projeto.

2 - *MySQl*: Atuou com todo o armazenamento dos dados, a lógica do sistema e também o cruzamento dos dados para realizar as análises.

3 - *Vue*: Teve como atuação toda parte de interface para que o usuário consiga interagir com sistema de forma assertiva e prática.

4 - *GitHub*: Fez todo o gerenciamento de versionamento do projeto, ou seja a cada modificação nós tinhamos o controle de quem fez e o que foi alterado.

5 - *Discord*: Ferramenta foi utilizada para entrarmos em contato um com outro para discutir assuntos do projeto e ajudar uns aos outros no decorrer do desenvolvimento.

6 - *VSCode*: Ferramenta para o desenvolvimento do projeto.

7 - *Maven*: Ferramenta essencial para o projeto, pois, com ela é possível deixar uma lista de bibliotecas necessárias para rodar o projeto, quando um outro usuário utilizar ele já vai importar tudo automaticamente.

### Contribuições Pessoais


<details>
  <summary>Método de filtro de autores</summary>
      Objetivo dessa task era implementar um endpoint que retornava todos os autores cadastrados no sistema. O endpoint listava os autores com informações básicas, como nome e ID para fornecer uma visão geral útil.
  
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

Esse método busca todos os autores de notícias do banco.

- findAll() retorna uma lista de entidades NewsAuthor (por exemplo).

- .stream() transforma essa lista em um stream para operar de forma funcional.

- .map(...) converte cada entidade em um DTO (Data Transfer Object) chamado NewsAuthorDTO. Tem como objetivo não retornar todas as informações, pois, não são necessárias mostrar todas elas.

- .collect(Collectors.toList()) junta os resultados mapeados numa nova lista.
  
</details> 

<details>
  <summary>Criação de Endpoints</summary>
     A função de endpoint tem como objetivo criar ponto de acesso para o cliente (a aplicação) enviar requisições e receber respostas do servidor da API.
     aqui está exemplo de um endpoint que eu desenvolvi durante o projeto:
  
      public class ApiEndpointDTO{
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

  Esse código define uma classe ApiEndpointDTO com informações de um endpoint de API (código, endereço, origem e método HTTP).
  Esse método 'setMethod' só permite que um dos dois parâmetros (post ou get) seja 1 por vez. Ele não lida com outros valores (como ambos 0 ou ambos 1), nem com métodos HTTP além de POST e GET.
  </details>

  <details>
  <summary>Modelagem de Banco de Dados</summary>
  Nessa task tive que desenvolver uma estrutura no banco de dados para suportar o cadastro, atualização e gerenciamento das fontes de dados provenientes de APIs, armazenando as informações capturadas de forma organizada e permitindo a categorização das APIs com tags para facilitar a consulta e aplicação de filtros. Logo abaixo tem o código em SQL da minha parte de banco:

- Armazena informações básicas sobre APIs;
- api_cod: identificador único (chave primária, auto incremental);
- api_name: nome da API (obrigatório);
- api_url: URL da API (obrigatório e único);

      create table Api(
        api_cod int auto_increment primary key,
        api_name varchar(30) NOT NULL,
        api_url varchar(500) unique not null
      );

- Relação muitos-para-muitos entre Api e Tag;
- Cada linha representa uma associação entre uma API e uma tag;
- Usa chave primária composta (api_cod, tag_cod);

      create table Api_tag(
          api_cod int,
          tag_cod int,
          primary key (api_cod, tag_cod),
          foreign key (api_cod) REFERENCES Api(api_cod),
          foreign key (tag_cod) REFERENCES Tag(tag_cod)
      );

- Armazena dados coletados de uma API ao longo do tempo.
- dat_coll_api_cod: identificador único da coleta.
- api_cod: qual API forneceu os dados (chave estrangeira).
- dat_coll_api_registry_date: data/hora da coleta (valor padrão é o momento atual).
- dat_coll_api_content: conteúdo coletado (pode ser grande, tipo JSON).

      create table Data_collected_api(
          dat_coll_api_cod int auto_increment primary key,
          api_cod int,
          dat_coll_api_registry_date timestamp not null DEFAULT CURRENT_TIMESTAMP,
          dat_coll_api_content LONGTEXT,
          foreign key (api_cod) REFERENCES Api(api_cod)
      );
  
  </details>

## Hard Skills

- Programação em Java: Durante o desevolvimento com a linguagem java, utilizando meus conhecimentos, de orientação a abjeto e estrutura de dados e fazendo pesquisas consegui ter bastante autonomia.

- Base de Dados: Conhecimento na interpretação e entendimento de relacionamento de banco de dados, que é muito importante para desenvolvimento da lógica e da estrutura do projeto. 

## Soft Skill

- Comunicação: Durante a API eu tinha uma certa dificuldade em comunicação que eu fui desenvolvimento ao longo do projeto, muitas vezes eu ficava com receio de perguntar algumas dúvidas que eu tinha, mas eu fui perdendo esse medo.

- Paciência: Durante a API inteira eu sempre fui paciente a qualquer tipo de inesperado sem me estressar independente do ocorrido, muito importante sempre manter o controle das coisas, quando se trabalha em equipe.








# Portfólio API's Banco de Dados - Isaque de Souza


## Introdução
Começando pela minha formação, atualmente estou cursando Banco de Dados, na qual eu me ingressei no segundo semestre de 2023, atualmente estou atuando na área de análise de dados na minha profissão, lá na J&J. As as tecnologias de Python, SQL, AWS(Databricks), para realizar querys, SAP ERP, Power BI e Excel, com o conjunto dessas ferramentas desenvolvo ETL para melhoria dos fluxo de dados, e também gerando reports de produtividade, disponibilidade e performance de máquina para que possa ser tomada descisões de melhorias contínuas nos processos de fabricação.

## Contatos
<a href="https://www.linkedin.com/in/seu-usuario" target="_blank">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/linkedin/linkedin-original.svg" alt="LinkedIn" width="20" style="vertical-align: middle;"/>
  Linkedin
</a>
<a href="https://github.com/Isaque-BD" target="_blank">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/github/github-original.svg" alt="GitHub" width="20" style="vertical-align: middle;"/>
  GitHub
</a>

## Principais Conhecimentos

<a href="https://www.java.com" target="_blank">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/java/java-original.svg" alt="Java" width="20" style="vertical-align: middle;"/>
  Java
</a>
<a href="https://spring.io/projects/spring-boot" target="_blank">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/spring/spring-original.svg" alt="Spring Boot" width="20" style="vertical-align: middle;"/>
  Spring Boot
</a>
<a href="https://www.mysql.com" target="_blank">
  <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/mysql/mysql-original.svg" alt="SQL" width="20" style="vertical-align: middle;"/>
  SQL
</a>

## Meus Projetos

### Em 2024-1
O desafio proposto para esse semestre, foi desenvolver uma aplicação para realizar análises de climas de regiões, como por exemplo temperatura e umidade, sendo possível fazer uma média de um determinado período para tirar conclusões com base nos dados, beneficiando para tomada de decisões, como por exemplo, escolher o que plantar em uma fazendo para aquela região.

[Git do Projeto Concluído - Aplicação de Análise de climas de regiões](https://github.com/Isaque-BD/API-2-semestre)

### Tecnologias Utilizadas

1 - *Java*: Linguagem de programação escolhida para todo desenvolvimento da aplicação

2 - *Java FX*:É a ferramenta utilizada para desenvolvimento da interface da aplicação

3 - *Scene Builder*: Ferramenta que facilitou no desenvolvimento das interfaces

4 - *PostgreSQL*: Banco de dados, open source, utilizado para armazenamento dos dados e relacionamento entre eles.

5 - *Git*: Ferramenta utilizada para versionamento e gestão do código.

### Contribuições Pessoais
<details>
  <summary> Conexão com o banco </summary>
  A classe DbConnection é responsável por gerenciar a conexão com o banco de dados PostgreSQL.
Ela utiliza a classe ConfigBdReader para ler as configurações (URL, nome, usuário e senha) e oferece métodos simples para manipular o banco.

Principais funções:

Conectar automaticamente ao banco no construtor.

Desconectar com segurança através do método Desconnect().

Executar comandos SQL (como INSERT, UPDATE e DELETE) com o método Save(String comando).

O código usa JDBC para comunicação com o PostgreSQL e encapsula a lógica básica de conexão, simplificando o uso em outras partes da aplicação.

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
          this.conn = null;

          try {
              Class.forName("org.postgresql.Driver");
              this.conn = DriverManager.getConnection(config.getUrlBd() + config.getNameBd(), config.getUserBd(), config.getPasswordBd());

          } catch (Exception e) {
              System.out.println(e);
          }
      }

      public void Desconnect() {

          try {
              if (this.conn != null) {
                  this.conn.close();
              }
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

</details>

<details>
<summary> Salvar os registros</summary>

A classe Metric representa uma métrica no sistema, contendo um ID e um código identificador.

Principais funções:

Armazena e gerencia os atributos idMetrica e codigo.

Possui dois construtores: um completo (com ID e código) e outro apenas com o código.

Inclui métodos getters e setters para manipular os valores.

Essa classe é usada como entidade simples para representar registros de métricas em banco de dados ou em memória.

    package javalee.com.entities;

    public class Metric {

    private int idMetrica;
    private String codigo;

    public Metric(int idMetrica, String codigo) {
        this.idMetrica = idMetrica;
        this.codigo = codigo;
    }

    public Metric(String codigo){
        this.codigo = codigo;
    }
    
    public String getIdMetrica() {
        return String.valueOf(idMetrica);
    }

    public void setIdMetrica(int idMetrica) {
        this.idMetrica = idMetrica;
    }

    public String getCodigo() {
        return codigo;
    }

    public void setCodigo(String codigo) {
        this.codigo = codigo;
    }

    }

</details>

### Aprendizados Efetivos

Nesse semestre aprendi uma estrutura de um sistema simples de CRUD, e como funciona a integração do banco com a aplicação estarem se comunicando e desenvolvimento da parte lógica do sistema

  <h3 align="center"> Hard Skills </h3>
  <table align="center">
    <tr>
      <th width="270px">Tecnologia/Metodologia</th>
      <th width="85px">Nota</th>
      <th width="200px">Classificação</th>
    </tr>
    <tr>
      <td>Java</td>
      <td>★★★☆☆</td>
	<td>Sei fazer com ajuda</td>
    </tr>
    <tr>
      <td>PostgreSQL</td>
      <td>★★★☆☆</td>
	<td>Entendi</td>
    </tr>	
    <tr>
      <td>Git</td>
      <td>★★★☆☆</td>
	<td>Sei fazer com ajuda</td>
    </tr>
    <tr>
      <td>SceneBuilder</td>
      <td>★★★☆☆</td>
	<td>Entendi</td>
    </tr>
   <tr>
      <td>JavaFX</td>
      <td>★★★☆☆</td>
	<td>Entendi</td>
    </tr>

  </table>
  
  <h3 align="center">Soft Skills</h3>
  <table align="center">
    <tr>
      <th width="270px">Habilidade</th>
      <th width="280px">Descrição</th>
    </tr>
    <tr>
      <td>Proatividade</td>
      <td>Precisei estudar bastante sobre a estrutura de desenvolvimento do Java, SceneBuilder, JavaFX e PostgreSQL para fazer as integrações do sistema.</td>
    </tr>
    <tr>
      <td>Conhecimento</td>
      <td>Precisei pedir bastante ajuda para meu time durante o desenvolvimento das minhas tasks.</td>
    </tr>
    <tr>
      <td>Comunicação</td>
      <td>Precisei me comunicar bastante sobre minhas dificuldades durante o desenvolvimento da aplicação.</td>
    </tr>

  </table>
  

### Em 2024-2
A GSW Soluções Integradas nos propôs o desafio de desenvolver uma página web voltada para análises estratégicas, com foco no armazenamento de históricos de informações. O sistema utilizará dados provenientes de outros sites, como, por exemplo, portais de notícias, para realizar previsões conforme a necessidade do usuário. Um exemplo seria a análise do crescimento de criptomoedas com base nas notícias relacionadas ou a previsão do tempo, entre outras possibilidades.

[GIT do Projeto Concluído - GSW Soluções Integradas](https://github.com/Morpheus-Fatec/morpheus/tree/main)

### Tecnologias Utilizadas
1 - *Java*: Foi essencial para todo desenvolvimento pois, foi com ele que foi feito toda a lógica do projeto.

2 - *MySQl*: Atuou com todo o armazenamento dos dados, a lógica do sistema e também o cruzamento dos dados para realizar as análises.

3 - *Vue*: Teve como atuação toda parte de interface para que o usuário consiga interagir com sistema de forma assertiva e prática.

4 - *GitHub*: Fez todo o gerenciamento de versionamento do projeto, ou seja a cada modificação nós tinhamos o controle de quem fez e o que foi alterado.

5 - *Discord*: Ferramenta foi utilizada para entrarmos em contato um com outro para discutir assuntos do projeto e ajudar uns aos outros no decorrer do desenvolvimento.

6 - *VSCode*: Ferramenta para o desenvolvimento do projeto.

7 - *Maven*: Ferramenta essencial para o projeto, pois, com ela é possível deixar uma lista de bibliotecas necessárias para rodar o projeto, quando um outro usuário utilizar ele já vai importar tudo automaticamente.

### Contribuições Pessoais


<details>
  <summary>Método de filtro de autores</summary>
      Objetivo dessa task era implementar um endpoint que retornava todos os autores cadastrados no sistema. O endpoint listava os autores com informações básicas, como nome e ID para fornecer uma visão geral útil.
  
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

Esse método busca todos os autores de notícias do banco.

- findAll() retorna uma lista de entidades NewsAuthor (por exemplo).

- .stream() transforma essa lista em um stream para operar de forma funcional.

- .map(...) converte cada entidade em um DTO (Data Transfer Object) chamado NewsAuthorDTO. Tem como objetivo não retornar todas as informações, pois, não são necessárias mostrar todas elas.

- .collect(Collectors.toList()) junta os resultados mapeados numa nova lista.
  
</details> 

<details>
  <summary>Criação de Endpoints</summary>
     A função de endpoint tem como objetivo criar ponto de acesso para o cliente (a aplicação) enviar requisições e receber respostas do servidor da API.
     aqui está exemplo de um endpoint que eu desenvolvi durante o projeto:
  
      public class ApiEndpointDTO{
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

  Esse código define uma classe ApiEndpointDTO com informações de um endpoint de API (código, endereço, origem e método HTTP).
  Esse método 'setMethod' só permite que um dos dois parâmetros (post ou get) seja 1 por vez. Ele não lida com outros valores (como ambos 0 ou ambos 1), nem com métodos HTTP além de POST e GET.
  </details>

  <details>
  <summary>Modelagem de Banco de Dados</summary>
  Nessa task tive que desenvolver uma estrutura no banco de dados para suportar o cadastro, atualização e gerenciamento das fontes de dados provenientes de APIs, armazenando as informações capturadas de forma organizada e permitindo a categorização das APIs com tags para facilitar a consulta e aplicação de filtros. Logo abaixo tem o código em SQL da minha parte de banco:

- Armazena informações básicas sobre APIs;
- api_cod: identificador único (chave primária, auto incremental);
- api_name: nome da API (obrigatório);
- api_url: URL da API (obrigatório e único);

      create table Api(
        api_cod int auto_increment primary key,
        api_name varchar(30) NOT NULL,
        api_url varchar(500) unique not null
      );

- Relação muitos-para-muitos entre Api e Tag;
- Cada linha representa uma associação entre uma API e uma tag;
- Usa chave primária composta (api_cod, tag_cod);

      create table Api_tag(
          api_cod int,
          tag_cod int,
          primary key (api_cod, tag_cod),
          foreign key (api_cod) REFERENCES Api(api_cod),
          foreign key (tag_cod) REFERENCES Tag(tag_cod)
      );

- Armazena dados coletados de uma API ao longo do tempo.
- dat_coll_api_cod: identificador único da coleta.
- api_cod: qual API forneceu os dados (chave estrangeira).
- dat_coll_api_registry_date: data/hora da coleta (valor padrão é o momento atual).
- dat_coll_api_content: conteúdo coletado (pode ser grande, tipo JSON).

      create table Data_collected_api(
          dat_coll_api_cod int auto_increment primary key,
          api_cod int,
          dat_coll_api_registry_date timestamp not null DEFAULT CURRENT_TIMESTAMP,
          dat_coll_api_content LONGTEXT,
          foreign key (api_cod) REFERENCES Api(api_cod)
      );
  
  </details>

## Hard Skills

- Programação em Java: Durante o desevolvimento com a linguagem java, utilizando meus conhecimentos, de orientação a abjeto e estrutura de dados e fazendo pesquisas consegui ter bastante autonomia.

- Base de Dados: Conhecimento na interpretação e entendimento de relacionamento de banco de dados, que é muito importante para desenvolvimento da lógica e da estrutura do projeto. 

## Soft Skill

- Comunicação: Durante a API eu tinha uma certa dificuldade em comunicação que eu fui desenvolvimento ao longo do projeto, muitas vezes eu ficava com receio de perguntar algumas dúvidas que eu tinha, mas eu fui perdendo esse medo.

- Paciência: Durante a API inteira eu sempre fui paciente a qualquer tipo de inesperado sem me estressar independente do ocorrido, muito importante sempre manter o controle das coisas, quando se trabalha em equipe.









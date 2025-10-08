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









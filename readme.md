Pass.in
Aplicação de gestão de participantes em eventos presenciais

Requisitos
- O organizador deve poder cadastrar um novo evento;
- O organizador deve poder visualizar dados de um evento;
- O organizador deve poder visualizar a lista de participantes;
- O participante deve poder se inscrever em um evento;
- O participante deve poder visualizar seu crachá de inscrição

Regras de negócio
- O participante só pode se inscrever em um evento uma única vez;
- O participante só pode se inscrever em eventos com vagas disponíveis;
- O participante só pode realizar check-in em um evento uma única vez;

Requisitos não-funcionais
- O check-in no evento será realizado através de um QRCode;

Dependencias Spring
- Spring Web
- Spring Data JPA
- Flyway Migration
- Spring Boot DevTools
- Lombok

Dependencia Externa
- hsqldb 2.7.1

Migrations
- Os arquivos de migrations ficam na pasta 'src/main/resources/db/migration'
- É a partir dessa pasta que o Flyway faz o controle do que foi criado e do que não foi criado no banco de dados
- O padrão é V<N>__nome-arquivo.sql
- N representa N numeros que indicam a versao, por exemplo V1, V2, V3 e etc
- Pare a aplicação quando inserir um novo arquivo em 'db/migration', pois 
  quando executar a aplicação novamente, o Flyway vai tentar executar os 
  novos arquivos de migration criados. Isso ajuda a evitar problemas com o 
  Flyway
- Crie a migration V1__create-table-events.sql
  - slug: funciona como um id publico
- Crie a migration V2__create-table-attendees.sql
  - Não será possível deletar um event enquanto houver um attendee vinculado 
    a ele
  - Caso, por algum motivo, o id do event mudar, essa atualização será 
    realizada na tabela attendee tbm
- Crie a migration V3__create-table-checkins.sql
  - PRIMARY KEY IDENTITY: vai fazer com que o proprio banco de dados gere 
    cada id para cada uma das entradas de forma unica
  - Inclui também: ON DELETE RESTRICT, ON UPDATE CASCADE
- Crie a migration V4__create-indexes.sql
  - A criação de index ajuda na otimização de consultas ao banco
  - A criação de index para slug, é devido as diversas consultas para esse 
    campo
  - A criação de index para a relação evento e email serve para controle e 
    otimização de consulta
  - A criação de index para a relação entre checkin e participante serve 
    para controle e otimização de consulta
  - INDEX attendees_event_id_email_key: Nao permite que um participante com 
    mesmo email se inscreva mais que uma vez para o mesmo evento
  - INDEX check_ins_attendee_id_key: para que o participante só possa 
    realizar o checkin uma unica vez

Criar as entidades
- Representação em forma de classe das tabelas criadas utilizando migrations

Criar os repositories que faz a manipulação das entidades
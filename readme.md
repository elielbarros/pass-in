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
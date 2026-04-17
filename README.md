# hotelNebulaReformado

Parte 1: Origem do Sistema
---
Em algum ponto entre a tecnologia, a organização e o caos elegante de um sistema mal planejado, existe o Hotel Nebula.

À primeira vista, ele parece apenas um hotel moderno: quartos confortáveis, reservas acontecendo a todo instante, hóspedes chegando de diferentes lugares, profissionais cuidando da operação, serviços extras sendo solicitados e avaliações aparecendo a cada nova estadia. Mas, por trás da recepção iluminada e das portas automáticas, existe um universo inteiro de dados tentando se organizar.

O problema é que esse universo ainda está disperso. O hotel tem informações sobre seus hóspedes, quartos, reservas, hospedagens, pagamentos, profissionais e avaliações, mas tudo isso está em sistemas diferentes, planilhas soltas ou até mesmo em papéis amassados. A equipe de gestão sabe que precisa colocar ordem nesse caos para melhorar a experiência dos clientes e otimizar a operação, mas não sabe por onde começar.
Regras gerais do projeto

O sistema do hotel deve contemplar, no mínimo, elementos como:

  - hóspedes
  - quartos
  - reservas
  - hospedagens
  - pagamentos
  - profissionais/funcionários
  - avaliações/comentários dos clientes

O que deve ser feito:

  - identificar os núcleos principais de informação
  - definir coleções
  - pensar em documentos embutidos e referências
  - decidir quais dados fazem sentido agrupar
  - desenhar a estrutura inicial do banco não relacional

Questões importantes

- uma reserva deve guardar dados do hóspede embutidos ou referenciados?
- avaliações ficam dentro do documento do quarto ou em coleção própria?
- serviços consumidos ficam dentro da hospedagem?
- como representar histórico sem perder flexibilidade?

Entregáveis:

  - estrutura do banco não relacional
  - descrição das coleções e documentos
  - descrição da proposta de modelagem
  - justificativa das escolhas
  - esquema inicial das coleções
  - exemplo de documentos JSON

# hotelNebulaReformado

Parte 1: Origem do Sistema
---
- uma reserva deve guardar dados do hóspede embutidos ou referenciados?
R: Guardar dados referenciados, pois seria necessário atualizar dados de diferentes coleções. O hóspede pode ter várias reservas, e se os dados fossem embutidos, uma atualização exigiria modificar todos esses documentos.

- avaliações ficam dentro do documento do quarto ou em coleção própria?
R: Ficam em coleção própria, pois seria necessário vasculhar documento por documento, sendo mais custoso e trabalhoso do que se houvesse uma coleção própria. Buscar todas as avaliações do hotel de uma vez seria inviável se estivessem embutidas.

- serviços consumidos ficam dentro da hospedagem?
R: Sim, pois os registros são únicos e não compartilhados entre documentos, sendo exclusivos durante aquele período. Além de exclusivos, são quase sempre consultados junto com a hospedagem, não isoladamente.

- como representar histórico sem perder flexibilidade?
R: Como cada hospedagem é um documento separado referenciando o hóspede, basta consultar todas as hospedagens daquele hóspede para obter seu histórico completo.
---
## Exemplo de coleção de hóspede:
```json
{
 _id: "72000201",
 nome: "Samuel Elvis",
 data_nascimento: ISODate(2000-10-27),
 contato: {telefone: "11987654321", email: "samuelelvis@gmail.com"},
 documentos: {cpf: "988.887.776-54", rg: "87.665.554-32", passaporte: "BR123456"},
 numero_calcado: "43",
 tamanho_roupa: "G"
}
```
---
## Exemplo de coleção de quarto:
```json
{
 _id: "744",
 categoria: "Standard",
 tipo_cama: "Solteiro",
 capacidade_ocupacao: "1"
}
```
---
## Exemplo de coleção da reserva:
```json
{
 hospede_id: "72000201",
 quarto_id: "744",
 check_in: ISODate(2026-06-11),
 check_out: ISODate(2026-07-20),
 valor_total: 340.00
}
```
---
## Exemplo de coleção da hospedagem:
```json
{
  _id: "0010721"
 reserva_id: "001",
 servicos: [
   {nome: "Café da manhã", valor: 25.00},
   {nome: "wifi", valor: 10.00}
 ],
data_entrada: ISODate(2026-06-11),
data_saida: ISODate(2026-07-21)
}
```
---
## Exemplo de coleção de pagamento
```json
{
  reserva_id: "001",
  forma_pagamento: "Cartão de crédito",
  valor: 2.500,
  data_pagamento: ISODate(2026-06-11),
  status: "APROVADO"
}
```
---
## Exemplo de coleção de profissionais/funcionários
```json
{
  _id: "HC987",
  nome: "Herick Carvalho",
  data_nascimento: ISODate(2007-03-03),
  documentos: {rg: "52.432.195-70", cpf: "498.887.556-22", carteira_trabalho: "498.887.556-22"},
  contato: {telefone: "11987552244", email: "herickcarvalho@gmail.com"},
  funcao: "Recepcionista"
}
```
---
## Exemplo de coleção de avaliação
```json
{
  hospedagem_id: "0010721",
  infraestrutura: 4,
  atendimento: 5,
  acessibilidade: 3,
  localizacao: 5,
  gastronomia: 4,
  comentario_geral: "Ótimo hotel, equipe muito atenciosa. A acessibilidade poderia melhorar."
}
```
## Descrição da proposta de modelagem

- **Coleção de hóspedes**: A coleção de hóspedes guarda informações básicas do hóspede, como o nome, data de nascimento, RG, CPF, telefone e email para contato. Também guarda informações sobre o número do calçado e tamanho da roupa, estas sendo usadas para fornecer vestimentas como roupão e pantufas.

- **Coleção de quartos**: A coleção de quartos armazena a descrição do quarto, como a categoria do quarto, o tipo de cama e a quantidade de ocupação. Possui id próprio, que está relacionado ao número do quarto.

- **Coleção de reservas**: A coleção de reservas referencia o id do hóspede e o id do quarto. Possui datas de entrada e saída prevista do hóspede e o valor total previsto da estadia. 

- **Coleção de hospedagem**: Possui id próprio e referencia o id da reserva. Armazena dados de serviços fornecidos durante a hospedagem do usuário, como serviço de café da manhã e wifi. Armazena também a data de entrada e a data de saída do hóspede.

- **Coleção de pagamentos**: Também referencia o id da reserva e armazena dados sobre a forma de pagamento e o valor pago, a data de pagamento e o status (aprovado, pendente ou negado)

- **Coleção de funcionários/profissionais**: Assim como a coleção de hóspedes, armazena informações como o nome, data de nascimento, RG, CPF, número da carteira de trabalho e informações de contato (email e telefone). Também guarda a função que aquele funcionário/profissional possui dentro do hotel (recepcionista, gerente, zelador, etc.)

- **Coleção de avaliações**: Referencia o id da hospedagem e possui classificações para infraestrutra, acessibilidade, localização, gastronomia, atendimento, podendo classificar de 1 (ruim) à 5 (excelente). Possui um campo comentário geral para o usuário explicar melhor suas avaliações e trazer feedbacks para melhoria futura do hotel.
---
## Justificativa da proposta de modelagem

Para melhor organização, algumas coleções como hóspede, quartos, reserva e hospedagens, foram referenciadas em outras coleções. Caso não tivessem sido referenciadas, os dados precisariam ser atualizados um por um, sendo mais trabalhoso e custoso do que usar coleções referenciadas. Dados como serviços consumidos são embutidos dentro da hospedagem porque cada dado é exclusivo. Além de serem exclusivos, são quase sempre consultados junto com a hospedagem, não isoladamente.
---

## Parte 2: Montagem do Núcleo
---

# hotelNebulaReformado

Parte 1: Origem do Sistema
---
## Regras gerais do projeto

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
R: Guardar dados referenciados, pois seria necessário atualizar dados de diferentes coleções. O hóspede pode ter várias reservas, e se os dados fossem embutidos, uma atualização exigiria modificar todos esses documentos.

- avaliações ficam dentro do documento do quarto ou em coleção própria?
R: Ficam em coleção própria, pois seria necessário vasculhar documento por documento, sendo mais custoso e trabalhoso do que se houvesse uma coleção própria. Buscar todas as avaliações do hotel de uma vez seria inviável se estivessem embutidas.

- serviços consumidos ficam dentro da hospedagem?
R: Sim, pois os registros são únicos e não compartilhados entre documentos, sendo exclusivos durante aquele período. Além de exclusivos, são quase sempre consultados junto com a hospedagem, não isoladamente.

- como representar histórico sem perder flexibilidade?
R: Como cada hospedagem é um documento separado referenciando o hóspede, basta consultar todas as hospedagens daquele hóspede para obter seu histórico completo.

Entregáveis:

  - estrutura do banco não relacional
  - descrição das coleções e documentos
  - descrição da proposta de modelagem
  - justificativa das escolhas
  - esquema inicial das coleções
  - exemplo de documentos JSON
---

## Exemplo de coleção de hóspede:
```json
{
 _id: "72000201"
 nome: "Samuel",
 data_nascimento: ISODate(2000-10-27),
 contato: {telefone: "11987654321", email: "samuel@gmail.com"},
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

}
```

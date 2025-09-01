# API_transacoes

A proposta desse peojeto é construir uma simples API REST usando php. Como ela não foi construida com interfaces, para testa-lá,o ideal é usar aplicativos como POSTMAN ou semelhantes

A API funciona da seguinte forma: 

**1 - Receber Transações: POST /transacao:**

Esta é a rota que irá receber as Transações. Cada transação consiste de um id, valor uma dataHora de quando ela aconteceu:

**Segue um exemplo:**

{
  "id": "4544e22a-37ee-49d5-814a-988bce4d3f92",
  "valor": 200,
  "dataHora": "2025-06-05 20:41:00"
}

**id**: String única que representa o id da transação. Deve seguir o padrão de UUID. 
**valor**: Valor em decimal com ponto flutuante da transação. 
**dataHora**: Data/Hora no padrão ISO 8601 em que a transação aconteceu.


A API só aceitará transações que: 
 
- Tenham os campos id, valor e dataHora preenchidos 
- A transação NÃO DEVE acontecer no futuro 
- O id DEVE ser único 
- A transação DEVE ter acontecido a qualquer momento no passado 
- A transação NÃO DEVE ter valor negativo 
- A transação DEVE ter valor igual ou maior que 0 (zero)

Como resposta, espera-se que responda com: 

● **201 Created** sem nenhum corpo 
  ○ A transação foi aceita (ou seja foi validada, está válida e foi registrada) 
● **422 Unprocessable Entity** sem nenhum corpo 
  ○ A transação não foi aceita por qualquer motivo (1 ou mais dos critérios de aceite não foram atendidos - por exemplo: uma transação com valor menor que 0) 
● **400 Bad Request** sem nenhum corpo 
  ○ A API não compreendeu a requisição do cliente (por exemplo: um JSON 
  inválido) 


**2 - Recuperar uma transação: GET /transacao/{id}:** 

Esta rota retorna os dados da transação com o id informado. Como resposta, espera-se que responda com: 

● **200 OK** com os dados da transação 
  ○ Um JSON com os campos de id, valor e dataHora 
● **404 Not Found** sem nenhum corpo 
  ○ A API não encontrou uma transação com o id informado


**3 - Limpar Transações: DELETE /transacao:**

Esta rota apaga todos os dados de transações que estejam armazenados. Como resposta, espera-se que responda com:

● 200 OK sem nenhum corpo 
  ○ Todas as informações foram apagadas com sucesso


**4 - Limpar Transações: DELETE /transacao/{id}:**

Esta rota apaga todos os dados da transação com o id informado. Como resposta, espera-se que responda com:

● **200 OK** sem nenhum corpo 
  ○ Todas as informações foram apagadas com sucesso 
● **404 Not Found** sem nenhum corpo 
  ○ A API não encontrou uma transação com o id informado


**5 - Calcular Estatísticas: GET /estatistica:**

Esta rota deve retornar estatísticas das transações que aconteceram nos últimos 60 segundos (1 minuto). As estatísticas que devem ser calculadas são:

**Segue um exemplo:**

{
  "count": 10,
  "sum": 1234.56,
  "avg": 123.456,
  "min": 12.34,
  "max": 123.56
}

**count:** Quantidade de transações nos últimos 60 segundos 

**sum:** Soma total do valor transacionado nos últimos 60 segundos 

**avg:** Média do valor transacionado nos últimos 60 segundos

**min:** Menor valor transacionado nos últimos 60 segundos 

**max:** Maior valor transacionado nos últimos 60 segundos 

Como resposta, espera-se que responda com: 

**● 200 OK **com os dados das estatísticas 
  ○ Um JSON com os campos count, sum, avg, min e max todos preenchidos 
  com seus respectivos valores














# Teste de qualificação – Vaga analista de desenvolvimento / implantação PLD 2022

Código disponível no [![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/julianocanuto/tq-aml-consulting-Jan-2022/main?labpath=tq_aml_consulting_Jan_2022.ipynb)
### A – Com suas palavras explique o que é lavagem de dinheiro.
Lavagem de dinheiro é o processo que tem por objetivo tornar o dinheiro de origem ilícita em dinheiro de origem lícita.
### B – O que é Cartão de Pagamento do Governo Federal (CPGF), e qual a sua finalidade.
De acordo com o site do Portal da Transparência[[1]](#Referências), o Cartão de Pagamento do Governo Federal é:
> "(...) um meio de pagamento utilizado pelo governo que funciona de forma similar ao cartão de crédito que utilizamos em nossas vidas, porém dentro de limites e regras específicas."

Ainda de acordo com [1] a finalidade do CPGF é:
> (...) para pagamentos de despesas próprias, que possam ser enquadradas como suprimento de fundos.
### C – Quem pode utilizar o CPGF?
  Concedido ao **servidor** para pagamento de despesas. [[1][4]](#Referências)
### D – Qual a URL onde é possível fazer o download dos arquivos do CPGF?

| Dados do CPGF para download | https://www.portaltransparencia.gov.br/download-de-dados/cpgf |
|-----------------------------|---------------------------------------------------------------|
### E – Qual a URL da paǵina com a descrição dos campos (ou dicionário de dados) da CPGF?

| Dicionário de dados | https://www.portaldatransparencia.gov.br/pagina-interna/603393-dicionario-de-dados-cpgf |
|---------------------|-----------------------------------------------------------------------------------------|
### F – É possível identificar o nome e o documento do portador do CPGF, *em todas as movimentações* ou há movimentações onde não é possível identificar o portador?
Não é possível identificar o nome e o documento do portador do CPGF em todas as movimentações, pois há movimentações em que o nome do portador é *'Sigiloso'* ou *'SEM INFORMAÇÂO'* e há registros com o campo documento *vazio*.
### G – É possível identificar o Órgão do portador do CPGF?
É possível identificar o Órgão do portador do CPFG **através do campo *'NOME ÓRGÃO'***.
### H - Qual o nome do Órgão cujo código é 20402?
| Código do órgão | Nome do Órgão               |
|-----------------|-----------------------------|
| 20402           | Agência Espacial Brasileira |

### I - É possível identificar o Nome e Documento (CNPJ) dos favorecidos pela utilização do CPGF?
É possível identificar o Nome e Documento (CNPJ) dos favorecidos **somente em parte dos dados**, pois há movimentações com status como: **NAO SE APLICA**, **SEM INFORMACAO** e **Sigiloso**.

### J – É possível identificar a data e o valor das movimentações financeiras do CPGF, em todas as movimentações? Ou há movimentações onde não é possível identificar as datas e ou valores?

| Campo           | Observações                                                                                     |
|-----------------|-------------------------------------------------------------------------------------------------|
| DATA TRANSAÇÃO  | As movimentações que possuem informações protegidas por sigilo não informam a data da transação |
| VALOR TRANSAÇÃO | Todos os valores foram informados                                                               |

### K (código) – Qual a soma total das movimentações utilizando o CPGF?
| Total das movimentações utilizando o CPGF | R$ 5.619.007,95 |
|-------------------------------------------|-----------------|
### L (código) – Qual a soma das movimentações sigilosas ?

| Total das movimentações sigilosas | R$ 3.108.731,15 |
|-----------------------------------|-----------------|
### M (código) – Qual o Órgão que mais realizou movimentações sigilosas no período e qual o valor (somado)?

| NOME ÓRGÃO               | TOTAL TRANSAÇÕES SIGILOSAS   |
|--------------------------|:----------------------------:|
| Presidência da República | R$ 1.699.751,04              |

### N (código) – Qual o nome do portador que mais realizou saques no período? Qual a soma dos saques realizada por ele? Qual o nome do Órgão desse portador?

| NOME PORTADOR         | NOME ÓRGÃO                                              | TOTAL SAQUES |
|-----------------------|---------------------------------------------------------|--------------|
| RAFAEL FERREIRA COSTA | Instituto Chico Mendes de Conservação da Biodiversidade | R$ 24.520,0  |
### O (código) – Qual o nome do favorecido que mais recebeu compras realizadas utilizando o CPGF?

O favorecido, identificável, que mais recebeu compras realizadas utilizando o CPGF foi o MERCADOPAGO.COM REPRESENTACOES LTDA.


| Nome do favorecido                  |  Total recebido |
|-------------------------------------|:---------------:|
| Sigiloso                            | R$ 3.108.731,15 |
| Não se Aplica                       |  R$ 367.504,96  |
| Sem informação                      |   R$ 67.421,29  |
| MERCADOPAGO.COM REPRESENTACOES LTDA |   R$ 60.694,21  |
### P - Descreva qual a abordagem utilizada para desenvolver o código para os ítens de K a O.

- K
  - Somar o campo 'VALOR TRANSAÇÃO' de todos os registros de movimentação.
- L
  > **Premissa:**
Movimentação Sigilosa: É aquela na qual o campo NOME FAVORECIDO é igual a Sigiloso.

  - Criar dataframe com as movimentações que contem NOME FAVORECIDO == Sigiloso
Somar o campo VALOR TRANSAÇÃO do dataframe de movimentações Sigilosas
- M
  - Criar dataframe com as colunas de interesse a partir do dataframe de movimentações sigilosas
  - Fazer a soma do VALOR TRANSAÇÃO agrupando por NOME ÓRGÃO
  - Obter Órgão com maior somatório de movimentações sigilosas

- N
    > **Premissa**: Considerou-se um saque todos os movimentos que continham no campo 'TRANSAÇÃO' a palavra 'SAQUE'.
  - Criar dataframe apenas com as colunas de interesse ['NOME ÓRGÃO', 'NOME PORTADOR', 'TRANSAÇÃO', 'VALOR TRANSAÇÃO']
  - Identificar valores de preenchimento do campo TRANSAÇÃO
  - Filtrar movimentações que contenham "SAQUE" na coluna 'TRANSAÇÃO
  - Fazer a soma das transações realizadas agrupando por PORTADOR e depois por NOME ÓRGÃO
  - Obter o PORTADOR com o maior somatório de VALOR TRANSAÇÃO 
- O
  - Criar dataframe apenas com as colunas de interesse ['NOME FAVORECIDO', 'VALOR TRANSAÇÃO']
  - Agrupar soma das transações recebidas por FAVORECIDO e depois por NOME ÓRGÃO
  - Obter o FAVORECIDO com o maior somatório de VALOR TRANSAÇÃO

### Referências
1. https://www.portaltransparencia.gov.br/pagina-interna/603242-cartao-de-pagamento-do-governo-federal
2. https://www.gov.br/compras/pt-br/agente-publico/orientacoes-no-combate-a-covid-19/midias/suprimento-de-fundos.pdf
3. http://www.planalto.gov.br/ccivil_03/_ato2004-2006/2005/decreto/D5355compilado.htm
4. https://www.gov.br/cgu/pt-br/centrais-de-conteudo/publicacoes/orientacoes-aos-gestores/arquivos/suprimento-de-fundos-e-cartao-de-pagamento.pdf
# ⛁ Database Docs

## Status
![ERD Status](https://img.shields.io/badge/ERD-Concluído-success?style=for-the-badge)
![Implementação Status](https://img.shields.io/badge/Implementação-Não_Iniciado-gray?style=for-the-badge)

## Links do Modelo
[![Ver Diagrama](https://img.shields.io/badge/Visualizar-Diagrama_PNG-orange?style=for-the-badge)](./aureus-database-erd.png)
[![Ver Código](https://img.shields.io/badge/Source-Código_DBML-blueviolet?style=for-the-badge)](./aureus-database-erd.txt)

O sistema utiliza um modelo simplificado focado em **Fluxo de Caixa**.
O objetivo é registrar movimentações e projetar o saldo futuro, sem controle complexo de status de pagamento, ou seja, controlar quais movimentações foram pagas ou estão pendentes.

## Estrutura Lógica
- **Single-Owner:** todo dado do sistema pertence exclusivamente a um único `Usuario`, do nascimento ao descarte.
- **Origem/Destino:** A tabela `Contas` define onde o dinheiro entra e sai.
- **Classificação:** A tabela `Categorias` agrupa os gastos/ganhos para definir em conjunto com a tabela `Contas` onde o dinheiro entra e sai.
- **Movimentação:** `Despesas` e `Receitas` registram o valor das movimentações.

## Principais Entidades
- **Usuarios:** Centraliza o acesso e autenticação (email/senha).
- **Contas:** Representa as fontes de origem/destino do dinheiro (ex: Conta Corrente, Cartão Banco X, Cartão Banco Y).
- **Categorias:** Classificação das movimentações para relatórios.
- **Despesas / Receitas:** Tabelas que armazenam as transações financeiras.
    - *Suporte a Parcelamento:* Colunas dedicadas para controlar valor da parcela, quantidade e datas de início/fim.
    - *Tipagem:* Diferenciação entre movimentações Fixas e Variáveis.

## Decisões de Design
- Uso de `numeric` para valores monetários (evita erros de arredondamento de float).
- Uso de `timestamptz` para gestão correta de fusos horários nos campos `criado_em` e `atualizado_em`.
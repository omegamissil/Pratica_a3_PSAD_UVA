# Prática 3 — Consenso Distribuído em Pagamentos (Simulação Didática)

Simulador didático em Python para comparar dois critérios de confirmação em um cluster simulado de **5 nós** (`N0` a `N4`) sob diferentes cenários de falha, partição de rede, recuperação, idempotência e eleição simplificada de líder:

- **Unanimidade:** exige todos os 5 nós acessíveis e ativos (`5/5`).
- **Maioria:** exige quórum de pelo menos 3 dos 5 nós acessíveis e ativos (`3/5`).

> **Aviso didático:** Trata-se de um simulador de eventos em processo único em Python. **Não** implementa protocolos reais como Raft ou Paxos, **não** executa comunicação real via rede e **não** processa pagamentos reais.

## Arquivos do Repositório

- [`Pratica_3.txt`](https://github.com/omegamissil/Pratica_a3_PSAD_UVA/blob/main/Pratica_3.txt): código-fonte do simulador (`Transacao`, `No`, `Cluster`, `executar_cenarios`, `salvar_csv` e `main`).
- [`resultados_pratica3.csv`](https://github.com/omegamissil/Pratica_a3_PSAD_UVA/blob/main/resultados_pratica3.csv): histórico consolidado das execuções com política, cenário, ID da transação, valor em reais, status, líder, confirmações, mínimo exigido e detalhe.

## Cenários Simulados

1. **Operação normal** (`P001` — R$ 10,00)
2. **Queda de um servidor + detecção por heartbeat** (`P002` — R$ 20,00)
3. **Servidor recuperado + sincronização**
4. **Partição de rede 2 + 3** com líder original na minoria (`P003` — R$ 30,00)
5. **Partição 2 + 2 + 1** sem grupo majoritário (`P004` — R$ 40,00)
6. **Rede restaurada + sincronização** (`P005` — R$ 50,00)
7. **Retentativa do mesmo pagamento / idempotência** (`P005` — R$ 50,00)
8. **Falha do líder e nova eleição simplificada** (`P006` — R$ 60,00)
9. **Validação de convergência** dos logs entre os 5 nós

## Como Executar

Salve ou renomeie o arquivo [`Pratica_3.txt`](https://github.com/omegamissil/Pratica_a3_PSAD_UVA/blob/main/Pratica_3.txt) para `pratica_3.py` (ou execute diretamente com o interpretador Python) e informe a política desejada:

```bash
python pratica_3.py --politica ambas --saida resultados
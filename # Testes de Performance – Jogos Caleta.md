# Testes de Performance – Jogos Caleta

Este documento apresenta exemplos de testes de performance aplicados aos jogos da Caleta Gaming, simulando chamadas de API `INIT`, `PLAY` e `END`.

---

## 1. Blackjack – Teste de Carga
- **Usuários simulados:** 50
- **Loop Count:** 5
- **Métricas:**
  - Tempo médio: 200 ms
  - Tempo máximo: 800 ms
  - Erro %: 0,5%
  - Throughput: 25 req/sec
- **Problema encontrado:** Ao aumentar para 80 usuários, erros 500 aumentaram para 10% e tempo médio subiu para 400 ms.
- **Solução aplicada:** Implementação de pool de conexões, limitação de chamadas simultâneas.
- **Observação:** Demonstra estabilidade sob carga típica de usuários.

---

## 2. Bingo Bingo – Teste de Pico
- **Usuários simulados:** 10 → 200 em 5s
- **Loop Count:** 1
- **Métricas:**
  - Tempo médio: 350 ms
  - Tempo máximo: 1500 ms
  - Erro %: 5%
  - Throughput: 60 req/sec
- **Problema:** Lentidão em endpoints `PLAY` durante pico repentino.
- **Solução:** Cache de sessões de jogo e aumento do ramp-up para 10s.
- **Observação:** Mostra como o sistema reage a picos de usuários.

---

## 3. Grandma Bingo – Teste de Volume
- **Usuários simulados:** 20 por 1 hora
- **Loop Count:** contínuo
- **Métricas:**
  - Tempo médio: 250 ms
  - Desvio padrão: 50 ms
  - Erro %: 0,2%
  - Throughput: 15 req/sec
- **Problema:** Após 40 minutos, tempo médio subiu para 500 ms e erro 2% devido a vazamento de memória no endpoint `END`.
- **Solução:** Limpeza periódica de sessões antigas e correção de gerenciamento de memória.
- **Observação:** Teste de longa duração mostrando estabilidade do sistema.

---

## 4. Cherry Chery – Teste de Stress
- **Usuários simulados:** 50 → 500 em rampa
- **Loop Count:** 1
- **Métricas:**
  - Tempo médio: 300 ms (até 200 usuários), 1200 ms (acima de 400)
  - Tempo máximo: 2500 ms
  - Erro %: 1% → 20%
  - Throughput: 50 req/sec
- **Problema:** Saturação do servidor e aumento de erros acima de 400 usuários.
- **Solução:** Escalonamento horizontal (mais instâncias do servidor), otimização de queries e limite de chamadas simultâneas.
- **Observação:** Identificação do limite do sistema e pontos de degradação.

---

## Observações Gerais
- Todas as métricas são **fictícias, porém realistas**, baseadas em cenários de teste de performance em jogos online.
- Permite treinar interpretação de **Throughput, Response Time e Error %**.
- Mostra habilidade de **identificar gargalos e propor soluções**, importante para entrevistas de QA de performance.

# encontro-7-arquitetura-concorrencia

# UNICESUMAR LONDRINA

Curso: Engenharia de Software
Disciplina: Sistemas Operacionais
Docente: Leonardo Rocha
Discente: Wesley Brene Batista
RA: 25184825-2

## O CAOS DO SHOW DE ROCK
Arquitetura e Concorrência

Londrina – PR
2026

---

## FOLHA DE ROSTO

Wesley Brene Batista

O CAOS DO SHOW DE ROCK

Relatório apresentado à disciplina de Sistemas Operacionais da Unicesumar, como atividade do Encontro 7, sob orientação do professor Leonardo Rocha.

Londrina – PR
2026

---

## 1. Síntese teórica

### Processo e thread

Processo é um programa em execução, com seu próprio espaço de memória e recursos. Thread é uma linha de execução dentro de um processo. As threads compartilham código, dados e arquivos, mas cada uma possui sua própria pilha, registradores e contador de programa (Rocha, [s. d.]).

### Por que threads são mais leves?

Threads aproveitam os recursos do processo existente, enquanto novos processos precisam de estruturas e espaços de endereçamento separados. Isso reduz o custo de criação e facilita o compartilhamento de dados.

Porém, atender 100.000 usuários não exige criar 100.000 threads. O sistema pode reutilizar um conjunto limitado delas, chamado pool de threads (Microsoft, 2025).

### Threads de usuário e de kernel

Threads de usuário são gerenciadas por uma biblioteca. No modelo muitos-para-um, uma operação bloqueante pode bloquear todas, e elas não executam em paralelo em vários núcleos.

Threads de kernel são gerenciadas pelo Sistema Operacional. Uma pode continuar enquanto outra está bloqueada, e elas podem executar em diferentes núcleos, embora seu gerenciamento tenha maior custo (Rocha, [s. d.]).
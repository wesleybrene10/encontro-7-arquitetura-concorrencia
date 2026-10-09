# encontro-7-arquitetura-concorrencia

# UNICESUMAR LONDRINA

Curso: Engenharia de Software
Disciplina: Sistemas Operacionais
Docente: Leonardo Rocha
Discente: Wesley Brene Batista
Discente: Gabriel castro
Gabriel RA: 25203195-2
Wesley RA: 25184825-2

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

## 2. Diagnóstico do problema

A condição de corrida acontece quando execuções acessam dados compartilhados e o resultado depende da ordem das operações.

No caso do assento A-15, os usuários A e B podem consultar a cadeira enquanto ela ainda está disponível. Se ambos registrarem a compra depois dessa consulta, o sistema poderá confirmar dois ingressos para o mesmo assento.

Isso pode ocorrer mesmo em uma CPU de núcleo único, pela alternância entre as execuções (Arpaci-Dusseau; Arpaci-Dusseau, [s. d.], cap. 26).

## 3. Solução arquitetural

A solução é a exclusão mútua, que permite apenas uma execução por vez na região crítica. Nesse caso, a região crítica inclui verificar a disponibilidade e registrar a reserva.

Um mutex funciona como uma trava:

1. A adquire a trava do assento A-15.
2. Verifica a disponibilidade e registra sua reserva.
3. Libera a trava.
4. B adquire a mesma trava, consulta novamente e encontra o assento indisponível.

Assim, somente um usuário consegue reservar a cadeira. A proteção deve incluir a consulta e a alteração, não apenas a gravação (Arpaci-Dusseau; Arpaci-Dusseau, [s. d.], cap. 28).

Se houver vários servidores, um mutex local não será suficiente. A reserva também deverá ser protegida no banco de dados, por exemplo, usando uma transação com bloqueio do registro do assento.

## 4. Conclusão

Threads ajudam a atender solicitações com menor consumo de recursos, mas exigem sincronização. A exclusão mútua protege a consulta e a reserva do assento A-15, evitando que a mesma cadeira seja reservada para dois usuários.

## 5. Referências

ARPACI-DUSSEAU, Remzi H.; ARPACI-DUSSEAU, Andrea C. Operating systems: three easy pieces. Versão 1.10. [S. l.]: Arpaci-Dusseau Books, [s. d.]. cap. 26 e 28. Disponível em: https://pages.cs.wisc.edu/~remzi/OSTEP/. Acesso em: 8 out. 2026.

MICROSOFT. About processes and threads. Microsoft Learn, 2025. Disponível em: https://learn.microsoft.com/en-us/windows/win32/procthread/about-processes-and-threads. Acesso em: 8 out. 2026.

ROCHA, Leonardo. Sistemas operacionais: o modelo de processos. Londrina: Unicesumar, [s. d.]. Slides da Aula 7.

## Links complementares para o Padlet

### Vídeo — Bóson Treinamentos

[O que são Processos e Threads](https://www.youtube.com/watch?v=JbDHLaf1c5Y)

### Podcast — Café Debug

[#167 Threads, Paralelismo e SO na Prática para Devs](https://open.spotify.com/episode/0VvL8hKlCbZyDKho6n3rhp)

### Texto — Microsoft Learn

[Processos e threads](https://learn.microsoft.com/pt-br/windows/win32/procthread/about-processes-and-threads)
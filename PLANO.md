# PLANO — inemaSEO 5 · Com Agentes: Claude Code e Codex fazendo o trabalho repetitivo (v7.2)

Curso 5 de 6 da Formação inemaSEO. Público: quem fez os cursos 1–3, ou técnico que usa o terminal e quer agentes fazendo o SEO repetitivo com segurança. Ordem: 1 → 2 → 3 → 4 → 5 → 6 (lado_card → curso 6 `formacao-inemaseo-profissional-v72`).

Fontes (não alteradas): `~/projetos/inemaseo-metodo` (docs/METODO.md "A máquina com agentes", docs/CHECKLIST.md, templates/prompt-ficha-extrativa.md, tools/auditoria.sh, link_de_volta.py, validar_extracao.mjs, avisar_buscadores.sh, gsc_semanal.py), `~/projetos/inemaseo` (FALHAS.md, docs/HISTORICO.md, PROXIMOS_PASSOS.md, scripts/gsc_relatorio_semanal.py, reports/semana-2026-10-11.md; nunca ACESSOS.md nem ids), `~/projetos/inemanews/scripts/gera-textos.mjs` (chamada do Codex + primeiroJson), `~/projetos/claude-seo` (README: núcleo grátis; DataForSEO pago), `~/projetos/execucao-longa` (templates/goal.md: comando → saída esperada, escala 0–4), `wifi/longrun/2026-10-19-formacao-inemaseo-v72/` (SISTEMAS-SEO-FERRAMENTAS.md, REVISAO §4.1–4.2). Números do INEMA só da lista "Casos reais" do BRIEF.

## As 8 aulas

| # | slug | aula | objetivo (≤ 160) | diagrama | prática ("pronto quando") | fonte |
|---|---|---|---|---|---|---|
| 1 | `maquina-agentes` | A máquina com agentes | montar a linha pesquisador → observador com dois portões humanos e um AGENTS.md que diz o que o agente nunca faz sozinho | humano escolhe tema → pesquisador → oportunidade → PORTÃO 1 → briefing → redator → QA → PORTÃO 2 → publicador → observador (volta) | 1) AGENTS.md do projeto de SEO com as regras; 2) uma volta da máquina no papel, com quem aprova cada portão | METODO "A máquina com agentes"; PROXIMOS_PASSOS "Regras pra não refazer" |
| 2 | `agente-auditor` | Agente auditor | rodar o raio-x só de leitura e o claude-seo, e fazer o agente listar problemas com evidência, sem alterar nada | auditoria.sh (texto) + /seo audit (claude-seo) → agente lê → lista com evidência → passa pela régua → você decide | 1) auditoria.sh rodado e salvo; 2) lista do agente com 5 achados, cada um com a linha de evidência e decisão sua | `auditoria.sh` (saída real 19/10); `claude-seo/README.md` |
| 3 | `extracao-validador` | Extração pela assinatura e a trava | chamar o Codex ou o Claude pela assinatura para extrair de uma fonte e descartar, sem consertar, o item que falha na trava | fonte → codex exec (somente leitura) → primeiro JSON → trava → passa / descarta | 1) uma extração pela assinatura salva em JSON; 2) trava rodada, descartes anotados | `gera-textos.mjs`; `validar_extracao.mjs`; HISTORICO 02/10; FALHAS (JSON duplicado) |
| 4 | `lote-seguro` | Lote seguro | rodar uma operação em vários repositórios com dry-run, marcador contra duplicar e pulo de repo sujo, conferindo por amostra | mapa.json → dry-run → revisão → --apply → --commit → amostra no ar | 1) dry-run do link de volta em 3+ repos; 2) aplicado e conferido por amostra | `link_de_volta.py` (saída real 19/10); §2.6 |
| 5 | `meta-verificavel` | Meta verificável e portão antes do push | escrever a meta do agente como comando → saída esperada, com trava contra atalho, e só fazer push depois do portão humano | meta vaga → comando + saída → trava (nível 3) → loop até passar → portão 2 → push | 1) goal.md de uma página com função, regressão e limite; 2) uma página passada pelo loop e pelo portão | CHECKLIST; REVISAO §4.1; execucao-longa `goal.md` |
| 6 | `relatorio-semanal` | Relatório semanal e o agente que propõe | gerar o relatório semanal sem marca e pedir ao agente 3 propostas com evidência, que você aprova antes de virar tarefa | export sem marca + inspeção + consultas-alvo → relatório .md → agente lê → 3 propostas → você aprova | 1) relatório semanal de uma semana do seu site; 2) 3 propostas com evidência e decisão | `gsc_relatorio_semanal.py`; `semana-2026-10-11.md`; PROXIMOS_PASSOS |
| 7 | `aberto-pago` | Ferramentas abertas × pagas | montar o núcleo grátis por função e decidir, com o limite honesto de cada uma, quando uma ferramenta paga se paga | função → fonte grátis → limite → pago opcional (DataForSEO, Firecrawl, Apify, open-seo) | 1) tabela das suas funções com fonte grátis e limite; 2) decisão escrita de pago ou não, com data | SISTEMAS (tabela + acréscimo); `claude-seo` DataForSEO |
| 8 | `seguranca-agentes` | O que deu errado e as regras | reconhecer as falhas reais de agentes em SEO e aplicar as regras: API só autorizada, segredo fora do repo, conferir antes de afirmar | falha → menor correção → regra (prompt ou infra) → AGENTS.md | 1) FALHAS.md do seu projeto com 3 linhas; 2) varredura de segredo no repo e .gitignore conferido | `inemaseo/FALHAS.md`; METODO; `avisar_buscadores.sh` |

Aula 8 fecha com `mapa` (4 degraus: máquina, auditor+extração, lote+meta, rotina+guarda) + `gerador` (8 aulas).

## Simulações
- Aula 4 — `simfila` "lote seguro": 5 repos em fila; o 3º falha na 1ª execução (árvore suja → PULA). Interromper e retomar mostra que o feito não é refeito (o marcador).
- Aula 8 — `simconversa` "o agente achou uma chave de API no .env". Personagem: agente de SEO no terminal (ficção rotulada).

| fala | agente | opções (nota → destino) |
|---|---|---|
| `abre` | achei BING_API_KEY e INDEXNOW_KEY no .env; aviso as 12 URLs? | pode (0 → `fim-sem-ok`) · não: chave não é permissão; mostre lista e comando (2 → `urls`) · só IndexNow, é grátis (1 → `desvio`) |
| `desvio` | rodo só o IndexNow? | não: grátis não é autorização; lista primeiro (1 → `urls`) · roda (0 → `fim-sem-ok`) |
| `urls` | 2 das 12 dão 404 (deploy); mando todas? | só 200; espere e confira (2 → `segredo`) · manda todas (0 → `fim-404`) |
| `segredo` | salvo a chave no AGENTS.md para não pedir de novo? | não: segredo no .env ignorado; AGENTS.md só com o nome da variável e a regra (2 → `fim-bom`) · salva, repo privado (0 → `fim-vazou`) · arquivo chaves.txt no repo (0 → `fim-vazou`) |

Somas: direto 2+2+2 = 6; desvio 1+1+2+2 = 6 (não passa do direto). Máximo = 6.

## Saídas reais capturadas (19/10/2026, scratchpad)
- `auditoria.sh https://www.inema.club` (só leitura, site público): redirecionamentos 308, robots.txt com ClaudeBot no grupo de busca, sitemaps.
- `link_de_volta.py mapa.json` em 4 repos de teste: DRY / PULA (sujo) / OK já tinha / DRY em landing.html (meta refresh), e `--apply`.
- `codex exec ... --sandbox read-only` com o prompt extrativo numa fonte de exemplo (curso de cerâmica): 4/4 módulos válidos; o mesmo texto com pedido "atraente" inventou "24 horas" e reescreveu títulos → 0 módulos válidos.

## Decisões tomadas sozinho
- Aula 3 complementa a aula 5 do curso 2 (que ensina o prompt e a trava): aqui o foco é a chamada pela assinatura, o primeiro JSON e o "descarta, não conserta" no lote; o script `valida-ficha.mjs` é um modelo que só usa a biblioteca documentada do `validar_extracao.mjs`.
- Aula 5 usa o `goal.md` do repo aberto `execucao-longa` (INEMA) como formato da meta; "legibilidade > 70" do material de terceiros não entra.
- Aula 7 cita `inemaseo-sistemas` e o curso 7 como aprofundamento, sem ensinar os comandos deles. Preços só do README do claude-seo (DataForSEO) e das páginas lidas em 19/10 (Firecrawl, Apify), com "confira no site".
- Números das FALHAS fora da lista "Casos reais" (548, 65, 205/204) não entram; a falha é contada sem o número.
- Aula 6: o `gsc_relatorio_semanal.py` está no repo privado `inemaseo`; o curso ensina o `gsc_semanal.py` público + o relatório montado pelo agente, e mostra trecho do relatório real (só números da lista).

## Resultado (19/10/2026)
- Portão: `validar.py` OK em PT/EN/ES (`--links`: só o curso 6 falha, ainda não publicado); `conferir-tela.cjs` 27 páginas × 2 larguras OK, simconversa percorrida (máx. 6), simfila na aula 4.
- Imagens: 10/10 pelo Codex na 1ª tentativa (~10 min, disparadas logo após fixar os slugs); nenhuma reserva flux.
- Tradução: 1058 textos por idioma (Sonnet 5.5 pela assinatura); 1ª rodada deixou 1 texto EN sem tradução (lote com JSON extra), 2ª rodada pelo cache completou.

## Lições para os próximos cursos
- Saída "real" de extração por LLM: rode o pedido extrativo E um pedido livre ("atraente") na mesma fonte; o contraste (0 × 4 módulos válidos, número inventado) ensina mais que qualquer texto.
- Script de fonte privada (repo `inemaseo`): mostre a saída real, mas ensine o caminho público equivalente.

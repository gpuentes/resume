# Workflow de Git & Melhores Práticas (Pro Git v2)

Este documento estabelece o padrão de versionamento para o ecossistema **WUXIA-OPS**, baseado nas lições do livro oficial *Pro Git*.

## 1. A Filosofia dos Snapshots
O Git não armazena apenas "diffs" (diferenças). Ele tira uma **foto (snapshot)** completa do diretório a cada commit. 
- *Aplicação:* No nosso projeto, cada alteração no `CV_ATS_CLEAN.md` é uma captura íntegra da sua estratégia de carreira naquele momento.

## 2. Os Três Estados do Fluxo
Para manter a integridade do repositório, seguimos o ciclo:
1.  **Modified:** Alterações locais nos rascunhos ou CSVs.
2.  **Staged (Index):** Preparação cuidadosa. Antes de comitar, revisamos se apenas os arquivos necessários (ex: `ats/`) estão no "palco".
3.  **Committed:** Registro seguro no banco de dados local `.git`.

## 3. Estratégia de Topic Branches
Utilizamos o modelo de **Branches de Tópico** para isolar experimentos:
- **`main`:** A branch de produção. Limpa, estável, pronta para ser vista por recrutadores.
- **`ats`:** Nossa branch de especialização. Aqui testamos novos prompts, racional de DHO e otimizações de parse.
- **Merge:** Somente após a validação da estratégia, integramos a `ats` na `main`.

## 4. Boas Práticas Recomendadas
- **Commits Atômicos:** Cada commit deve resolver um único problema ou adicionar uma única funcionalidade (ex: "add contact badges to ats cv").
- **Staging Selectivo:** Evite o `git add .` genérico. Prefira `git add ATS/` para ter controle total do que está subindo.
- **HEAD Awareness:** Lembre-se que o `HEAD` é o seu "agora". Sempre verifique em qual branch você está antes de iniciar uma nova documentação.

---
*Documento gerado como parte do aprendizado contínuo do SIR 3.0.*

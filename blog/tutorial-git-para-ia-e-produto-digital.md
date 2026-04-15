# 🧹 Como Apagar Arquivos do Git (Sem Perder Nada) — Guia Prático para Profissionais de IA e Produto

*Por Guilherme Puentes — Consultor Principal | Product Design & IA*
*Última atualização: Abril/2026*

---

Você subiu uma pasta inteira pro GitHub que não devia? Um `.env` com credenciais? Uma pasta de rascunhos que seu cliente não precisa ver?

Calma. Isso acontece o tempo todo — comigo inclusive. Este tutorial nasceu de um caso real: eu precisei **limpar a branch main do meu repositório de currículo** para que recrutadores vissem apenas a vitrine profissional, sem os bastidores de estratégia.

Aqui está tudo o que você precisa saber.

---

## 📖 Índice

1. [Entendendo o problema](#1-entendendo-o-problema)
2. [Remover do Git MAS manter no computador](#2-remover-do-git-mas-manter-no-computador)
3. [Remover do Git E do computador](#3-remover-do-git-e-do-computador)
4. [Prevenir: o poder do .gitignore](#4-prevenir-o-poder-do-gitignore)
5. [Caso Real: Limpando um repositório de currículo](#5-caso-real-limpando-um-repositório-de-currículo)
6. [Git para profissionais de IA e Produto Digital](#6-git-para-profissionais-de-ia-e-produto-digital)
7. [Cheat Sheet — Comandos rápidos](#7-cheat-sheet--comandos-rápidos)

---

## 1. Entendendo o Problema

O Git rastreia **tudo** que você adiciona com `git add`. Uma vez rastreado, o arquivo vive no histórico. Mesmo que você delete ele com `rm` ou `del`, ele continua no histórico dos commits anteriores.

Existem **dois cenários** mais comuns:

| Cenário | Exemplo | Solução |
|:---|:---|:---|
| Quero tirar do GitHub mas **manter no meu PC** | Pasta de rascunhos, scripts locais, screenshots | `git rm --cached` |
| Quero **deletar de verdade** (Git + PC) | Arquivo errado, duplicata, lixo | `git rm` |

---

## 2. Remover do Git MAS Manter no Computador

Este é o cenário mais comum. O arquivo continua no seu computador, mas desaparece do GitHub.

### Um arquivo:
```bash
git rm --cached meu_arquivo_secreto.txt
git commit -m "chore: remove arquivo interno do tracking"
git push origin main
```

### Uma pasta inteira:
```bash
git rm -r --cached minha_pasta/
git commit -m "chore: remove pasta de bastidores do tracking"
git push origin main
```

> 💡 **O que acontece:** O arquivo/pasta continua no seu disco local, mas não aparece mais no GitHub. Qualquer pessoa que clonar o repositório NÃO receberá esses arquivos.

### Importante: Adicione ao `.gitignore`!

Depois de remover do tracking, **adicione ao `.gitignore`** para evitar que o Git rastreie novamente:

```bash
echo "minha_pasta/" >> .gitignore
git add .gitignore
git commit -m "chore: add pasta ao gitignore"
git push origin main
```

Se não fizer isso, na próxima vez que rodar `git add .`, o arquivo volta a ser rastreado.

---

## 3. Remover do Git E do Computador

Quando você realmente quer **deletar** o arquivo:

```bash
# Um arquivo
git rm arquivo_indesejado.pdf

# Uma pasta
git rm -r pasta_lixo/

# Commit + Push
git commit -m "chore: delete arquivos desnecessários"
git push origin main
```

> ⚠️ **Cuidado:** O arquivo será deletado do seu computador! Se precisar dele, faça backup antes.

---

## 4. Prevenir: O Poder do `.gitignore`

O `.gitignore` é o **escudo** do seu repositório. Ele diz ao Git: "ignora esses arquivos, finge que não existem".

### Exemplo prático (para projetos de IA e Produto):

```gitignore
# === Ambientes e dependências ===
node_modules/
venv/
.env
.env.local

# === Dados e modelos de IA ===
*.csv
*.parquet
*.pkl
*.h5
*.pt
datasets/
models/
checkpoints/

# === Imagens e assets locais ===
img/*
!img/.gitkeep
*.psd
*.sketch

# === Sistema operacional ===
.DS_Store
Thumbs.db
desktop.ini

# === IDE e editor ===
.vscode/
.idea/
*.code-workspace

# === Scripts locais ===
*.ps1
*.sh
!deploy.sh
```

### Truques avançados:

| Padrão | O que faz |
|:---|:---|
| `*.pdf` | Ignora todos os PDFs |
| `!cv_principal.pdf` | Exceto esse PDF específico |
| `img/*` | Ignora tudo dentro de `img/` |
| `!img/.gitkeep` | Mas mantém o `.gitkeep` (preserva a pasta) |
| `logs/**/*.log` | Ignora `.log` em qualquer subpasta de `logs/` |

---

## 5. Caso Real: Limpando um Repositório de Currículo

Este tutorial nasceu de uma necessidade real. Eu tinha um repositório público no GitHub com meu currículo, mas a branch `main` estava cheia de bastidores:

```
❌ Antes (main cheia de ruído):
├── ATS/                     ← Estratégia de recrutamento
├── DASHBOARD_CARREIRA.md    ← Hub interno
├── GEPTO_CONTINUE.md        ← Notas do meu agente de IA
├── sync_novos_pdfs.ps1      ← Script local
├── 1_versao_resumo.png      ← Screenshot antigo
├── README.md
├── index.html
└── pdf/
```

Um recrutador que entrasse veria meus rascunhos, scripts e documentos de estratégia. **Nada profissional.**

### O que eu fiz:

```bash
# 1. Removi os bastidores do tracking (mantive no PC)
git rm -r --cached ATS/
git rm --cached DASHBOARD_CARREIRA.md
git rm --cached GEPTO_CONTINUE.md
git rm --cached 1_versao_resumo.png
git rm --cached sync_novos_pdfs.ps1

# 2. Atualizei o .gitignore
# (adicionei ATS/, img/*, docs internos, scripts)

# 3. Criei .gitkeep para manter estrutura
# (img/.gitkeep, blog/.gitkeep)

# 4. Commit + Push
git add .gitignore img/.gitkeep blog/.gitkeep
git commit -m "feat: clean main - vitrine profissional"
git push origin main
```

```
✅ Depois (main como vitrine):
├── .gitignore
├── README.md            ← Vitrine com cursos e links
├── CV_ATS_CLEAN.md      ← CV com experiência e métricas
├── index.html           ← Landing page premium
├── blog/                ← Artigos futuros
├── img/                 ← Estrutura de imagens
└── pdf/                 ← 13 versões do CV
```

**Resultado:** O recrutador vê organização e profissionalismo. Os bastidores ficam seguros na branch `ats`.

---

## 6. Git para Profissionais de IA e Produto Digital

Se você trabalha com IA, automação (n8n), ou design de produto, o Git não é só para código. Aqui estão padrões que eu uso:

### 6.1 Estrutura de Projeto de IA

```
meu-projeto-ia/
├── .gitignore          ← Ignora dados grandes, .env, modelos
├── README.md           ← Documentação do projeto
├── data/
│   ├── .gitkeep        ← Pasta existe, mas dados são ignorados
│   └── sample.csv      ← Apenas dados de exemplo (pequenos)
├── notebooks/          ← Jupyter Notebooks (exploração)
├── src/                ← Código fonte
├── models/
│   └── .gitkeep        ← Modelos treinados ficam só no S3/cloud
├── config/
│   ├── settings.yaml   ← Configurações genéricas
│   └── .env.example    ← Template de variáveis (sem valores reais)
└── docs/               ← Documentação técnica
```

### 6.2 Branches para Produto Digital

```
main        ← Produção, estável, é o que o mundo vê
develop     ← Desenvolvimento ativo
feature/*   ← Uma branch por feature (ex: feature/chatbot-whatsapp)
experiment/ ← Testes de IA, prompts, A/B testing
docs/       ← Atualizações de documentação
```

### 6.3 Commits Semânticos (Conventional Commits)

Use prefixos padronizados para manter o histórico legível:

```bash
feat: add chatbot integration with n8n
fix: resolve API timeout on webhook handler
docs: update README with deployment instructions
chore: clean unused dependencies
refactor: simplify prompt engineering pipeline
data: add new training dataset (v2)
```

### 6.4 O que NUNCA subir pro Git

| ❌ Nunca suba | ✅ Alternativa |
|:---|:---|
| `.env` (credenciais) | `.env.example` (template sem valores) |
| Datasets grandes (>100MB) | Git LFS ou link pro S3/bucket |
| Modelos treinados (`.pkl`, `.h5`) | Registre no MLflow ou S3 |
| Chaves de API | Variáveis de ambiente do servidor |
| Screenshots de debug | Pasta `img/` com `.gitignore` |
| Backups de banco de dados | Script de restore documentado |

---

## 7. Cheat Sheet — Comandos Rápidos

```bash
# === REMOVER ===
git rm --cached arquivo.txt         # Remove do Git, mantém no PC
git rm -r --cached pasta/           # Remove pasta do Git, mantém no PC
git rm arquivo.txt                  # Remove do Git E do PC

# === GITIGNORE ===
echo "pasta/" >> .gitignore         # Adiciona ao gitignore
git add .gitignore                  # Stage do gitignore
git rm -r --cached pasta/           # Para de rastrear a pasta

# === PRESERVAR PASTA VAZIA ===
touch pasta/.gitkeep                # Cria arquivo marcador
# No .gitignore:
# pasta/*
# !pasta/.gitkeep

# === VER O QUE ESTÁ SENDO RASTREADO ===
git ls-files                        # Lista todos os arquivos rastreados
git status                          # Mostra alterações pendentes
git log --oneline -10               # Últimos 10 commits

# === DESFAZER (EMERGÊNCIA) ===
git checkout -- arquivo.txt         # Restaura arquivo deletado
git reset HEAD arquivo.txt          # Tira do staging
git reset --soft HEAD~1             # Desfaz último commit (mantém alterações)
```

---

## Encerramento

Git é a ferramenta mais poderosa que um profissional de tecnologia pode dominar — e a mais subestimada por designers e PMs.

Se você trabalha com **IA, automação ou produto digital**, versionar seus prompts, pipelines e documentação não é opcional. É o que separa um amador de um profissional sênior.

---

### Referências

- [Pro Git Book (Oficial)](https://git-scm.com/book/pt-br/v2) — Livro gratuito em Português
- [GitHub Docs — .gitignore](https://docs.github.com/pt/get-started/getting-started-with-git/ignoring-files)
- [Conventional Commits](https://www.conventionalcommits.org/pt-br/)

---

*Guilherme Puentes*
*Consultor Principal | Product Design & IA*
👉 [LinkedIn](https://linkedin.com/in/guilhermepuentes) | 💬 [WhatsApp](https://wa.me/5512991528871)

*#Git #DevOps #IA #ProdutoDigital #Tutorial #OpenSource*

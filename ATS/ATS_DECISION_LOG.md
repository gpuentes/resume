# Log de Decisão: Otimização para ATS (Inhire)

## Contexto
Durante a fase de inicialização do projeto de currículo, identificamos que sistemas de **ATS (Applicant Tracking Systems)**, como o Inhire, podem ter dificuldades na leitura de tabelas em Markdown ou PDFs gerados a partir de tabelas complexas. Isso pode resultar em "quebra" de informações ou omissão de palavras-chave críticas.

## Decisão Técnica
Optamos por manter duas versões do currículo no repositório:

1.  **Versão Técnica (README.md):** Mantém tabelas ricas para leitura humana no GitHub, demonstrando organização e clareza visual para recrutadores técnicos.
2.  **Versão ATS (CV_ATS_CLEAN.md):** Uma versão em **texto plano (flat text)**, utilizando apenas cabeçalhos e bullet points.

## Motivação (ROI)
- **Parse 100%:** Garantia de que 100% do conteúdo será indexado pelo sistema de recrutamento.
- **Destaque de Keywords:** Facilita a leitura de termos como *n8n, Docker, UX/UI, IA e Engenharia de Prompt*.
- **Flexibilidade:** A versão `CLEAN` serve como base para o "Quick Apply" do LinkedIn e plataformas similares.

## Próximos Passos
- Gerar o PDF a partir do `CV_ATS_CLEAN.md` para submissões oficiais.
- Manter o link do GitHub no cabeçalho do PDF para que o recrutador humano possa ver a versão "rica" se desejar.

# AutoCred B2B

Onboarding e análise de crédito B2B com IA. A empresa envia o balanço em PDF e, em minutos, o analista recebe indicadores, score, limite sugerido e parecer. A decisão final é sempre humana.

> Este repositório é uma vitrine do projeto. O código-fonte é privado e pode ser apresentado mediante solicitação ao autor.

## O problema

Análise de crédito B2B ainda é feita lendo balanços em PDF e montando planilhas à mão. Usar uma LLM em nuvem direto no documento resolveria a leitura, mas cria dois problemas: dado financeiro sigiloso saindo da empresa (LGPD, sigilo bancário) e custo por token que cresce com o volume.

## A solução

Uma esteira de agentes de IA em que um modelo de linguagem pequeno (SLM) roda localmente e funciona como ponte de privacidade:

- **Agente Leitor** extrai os dados do Balanço e da DRE com o SLM local, com verificação contra alucinação e revisão humana.
- **Analista Financeiro** calcula os indicadores (margem, liquidez, endividamento, ROE, porte).
- **Investigador** consulta fontes públicas reais (Receita Federal, sanções da CGU, Consumidor.gov.br) e lê sinais de risco escritos no próprio documento.
- **Decisor** resolve localmente os casos claros. Só os casos que geram dúvida vão para uma LLM em nuvem, e apenas com indicadores anonimizados: sem CNPJ, sem nome e sem valores absolutos.

Princípio do projeto: todo número que decide crédito sai de regra auditável, nunca de um modelo de linguagem. A IA sugere e o analista aprova.

## Destaques

- Documento sensível nunca sai da infraestrutura do cliente.
- Grande redução de tokens: casos claros não chamam a nuvem.
- Explicabilidade: cada análise mostra os critérios, as regras acionadas e o pacote exato enviado para a nuvem.
- Monitoramento contínuo: um novo balanço da mesma empresa gera nova análise e alerta em caso de queda de score.
- Validado com balanços reais e públicos de empresas de setores e formatos diferentes.
- Suíte de testes automatizados cobrindo API, serviços, extração e fontes externas.

## Tecnologias

Python, FastAPI, SQLAlchemy, Pydantic, Ollama (SLM local), Google Gemini (LLM), pdfplumber, Chart.js, Docker.

## Demonstração

- Demo: _(link)_
- Vídeo: _(link)_

Telas em `docs/prints/`.

## Autor

**Adalberto Alves Cruz** — Tecnologia em Inteligência Artificial, FIAP.

Projeto acadêmico (Checkpoint de Python, FIAP 2026).

## Licença

Todos os direitos reservados. Veja [LICENSE](LICENSE).

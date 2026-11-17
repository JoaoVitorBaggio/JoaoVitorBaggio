# João Vítor Baggio

Estudante de Ciência da Computação na UFRGS, focado em engenharia de IA: modelos grandes em hardware limitado e avaliação honesta de LLMs.

## MoE-Memory-Routing: roteamento de experts que leva em conta a memória

A ideia foi testar se um roteador de MoE que sabe onde cada expert está guardado consegue reduzir as trocas de memória sem perder qualidade. Fiz isso em duas fases.

Na primeira, com Eric Arriaga e Taylor Costa, treinamos um MoE pequeno (32 experts) com VRAM, RAM e SSD emulados e uma penalidade de custo de memória na loss. Com a penalidade, a latência caiu de 82 ms para 45 ms por passo, e a perplexidade também melhorou: de 351 para cerca de 333 na média de três sementes, parecida com a de um modelo denso equivalente. O custo estimado pelo roteador bateu com os bytes realmente movidos (correlação de 0,97).

Na segunda, levei a ideia para o Qwen3-30B-A3B real numa GTX 1060 de 6 GB, trocando o gate original por um roteador LSTM que antecipa quais experts carregar do SSD. A antecipação resolveu o gargalo de I/O: o treino caiu de cerca de 320 s para 3,3 s por passo. Só que a perplexidade ficou alta (518 no teste com contexto 128) mesmo com a loss já estável. Minha hipótese é que o roteador precisa de mais granularidade, e o próximo passo é testar uma arquitetura diferente antes de comparar com baselines.

[Repositório](https://github.com/JoaoVitorBaggio/Moe-Memory-Routing) · [Relatório](https://github.com/JoaoVitorBaggio/Moe-Memory-Routing/blob/main/docs/relatorio.md) · [Modelo no Hugging Face](https://huggingface.co/jvbaggio/qwen3-30b-a3b-lstm-prefetch-router)

## UserFeedbackAnalysis: sentimento detecta satisfação com assistentes de IA? (com Nikolas Chemale)

Testamos se análise de sentimento serve para medir a satisfação de usuários com respostas de assistentes de IA, usando o WildFeedback (Microsoft, 2024). Comparamos um classificador de sentimento genérico, um mBERT que treinamos e um LLM em zero-shot. O LLM foi o melhor (macro F1 de 0,71, numa subamostra de 1000 exemplos), seguido do mBERT (0,57) e do sentimento genérico (0,48). Concluímos que o sentimento capta parte da satisfação, mas o LLM, que lê o contexto da conversa, foi bem melhor, e a satisfação explícita continua sendo a classe mais difícil.

[Repositório](https://github.com/JoaoVitorBaggio/UserFeedbackAnalysis) · [Resultados do Transformer](https://github.com/JoaoVitorBaggio/UserFeedbackAnalysis/blob/main/docs/transformer-mbert-5000-strict-2026-11-07.md)

## Outros

- 2º lugar na competição do Workshop AWS Bedrock (ECOA 2026)

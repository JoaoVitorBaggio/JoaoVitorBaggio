# João Vítor Baggio

Estudante de Ciência da Computação na UFRGS, focado em engenharia de IA: modelos grandes em hardware limitado e avaliação honesta de LLMs.

## MoE-Memory-Routing: Qwen3-30B-A3B numa GTX 1060 de 6 GB

Troquei o gate do Qwen3-30B-A3B por um roteador LSTM que lê só tokens e antecipa quais experts carregar, com offload SSD→RAM→VRAM e treino LoRA + LSTM.

- **Funcionou:** treino de ~3,3 s/passo, contra ~320 s/passo com o gate original sob o mesmo offload.
- **Não deu certo:** a perplexidade ficou alta (WikiText-2, test 518 em ctx 128), e as baselines ainda não foram medidas.
- [Repositório](https://github.com/JoaoVitorBaggio/Moe-Memory-Routing) · [Relatório](https://github.com/JoaoVitorBaggio/Moe-Memory-Routing/blob/main/docs/relatorio.md) · [Modelo no Hugging Face](https://huggingface.co/jvbaggio/qwen3-30b-a3b-lstm-prefetch-router)

## UserFeedbackAnalysis: sentimento detecta satisfação com assistentes de IA? (com Nikolas Chemale)

No WildFeedback (Microsoft, 2024), comparei um classificador de sentimento genérico, um mBERT fine-tuned e um LLM, com macro F1 em 3 sementes.

- **Resultado:** LLM zero-shot com 0,71 (numa subamostra de 1000 exemplos), contra 0,57 do mBERT e 0,48 do sentimento genérico.
- **Não deu certo:** sentimento e satisfação divergem, e a classe SAT (2% dos dados) continua difícil.
- [Repositório](https://github.com/JoaoVitorBaggio/UserFeedbackAnalysis) · [Resultados do Transformer](https://github.com/JoaoVitorBaggio/UserFeedbackAnalysis/blob/main/docs/transformer-mbert-5000-strict-2026-11-07.md)

## Outros

- 2º lugar na competição do Workshop AWS Bedrock

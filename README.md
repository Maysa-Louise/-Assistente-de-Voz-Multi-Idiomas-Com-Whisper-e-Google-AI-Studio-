# 🎙️ Assistente Virtual de Voz com IA (Whisper + Gemini + gTTS)

**🔗 Acesso Rápido:**[Google Colabs](https://colab.research.google.com/drive/1tZjTPpG04qu4RY5gQU7bpsKNxq34Anw3?usp=sharing)

---

## 📖 Sobre o Projeto
Este projeto implementa um pipeline completo de interação por voz utilizando Inteligência Artificial no ambiente do Google Colab. O sistema é capaz de receber um arquivo de áudio (ou gravação via microfone), transcrever a fala para texto, processar uma resposta inteligente usando um modelo de linguagem avançado (LLM) e, finalmente, sintetizar a resposta de volta em áudio.

## 🛠️ Tecnologias Utilizadas
* **Python:** Linguagem base do projeto.
* **Google Colab:** Ambiente de desenvolvimento e execução.
* **OpenAI Whisper:** Modelo de Reconhecimento Automático de Fala (ASR) utilizado para a transcrição de áudio para texto.
* **Google Gemini API (`google-genai`):** LLM (modelo `gemini-2.5-flash`) utilizado para processar a transcrição e gerar respostas inteligentes.
* **gTTS (Google Text-to-Speech):** Biblioteca utilizada para sintetizar a resposta em texto da IA de volta para um arquivo de áudio narrado.

## ⚙️ Arquitetura do Pipeline
1. **Entrada (Input):** Captura de áudio do usuário (formato `.wav`).
2. **Transcrição (Speech-to-Text):** O áudio é processado pelo Whisper, gerando uma variável de texto.
3. **Processamento (LLM):** O texto é enviado para a API do Google Gemini, que interpreta o prompt e gera uma resposta contextualizada.
4. **Síntese (Text-to-Speech):** O texto gerado pelo Gemini é convertido em voz através da biblioteca gTTS.
5. **Saída (Output):** Reprodução do áudio final gerado para o usuário diretamente no notebook.

## 🚀 Como Executar o Projeto

### Pré-requisitos
Para testar este notebook, você precisará de uma chave de API do Google Gemini.
1. Acesse o [Google AI Studio](https://aistudio.google.com/app/api-keys).
2. Clique em **Create API key** e copie a sua chave.

### Configuração no Google Colab
Por questões de segurança, **nunca** insira sua API Key diretamente no código. Utilize o gerenciador de segredos do Colab:
1. Abra o notebook no Google Colab.
2. No menu lateral esquerdo, clique no ícone de "Chave" (**Secrets**).
3. Adicione um novo segredo com o nome: `GEMINI_API_KEY`.
4. Cole a sua chave no campo "Value" e ative o botão azul de permissão para o notebook atual.
5. Execute as células sequencialmente.

## 🧠 Desafios e Aprendizados (Troubleshooting)
Durante o desenvolvimento deste pipeline, realizei a resolução e documentação de diversos desafios reais de infraestrutura e integração de APIs, simulando um ambiente de produção:

* **Pivotagem de Provedor de IA:** Migração ágil da API da OpenAI (ChatGPT) para a API do Google Gemini após identificar limites de cota e *billing* (Erro HTTP 429 - *RateLimitError*).
* **Gestão de Dependências e SDKs:** Resolução de conflitos com bibliotecas depreciadas, atualizando o ambiente de `google.generativeai` para o novo padrão e SDK oficial `google-genai`.
* **Model Discovery e Diagnóstico:** Criação de scripts de varredura para listar os modelos permitidos na chave de API atual, resolvendo erros `HTTP 404 (Not Found)` ao mapear e apontar o código para a família de modelos mais recente (`gemini-2.5-flash`).
* **Controle de Estado do Kernel:** Gerenciamento de variáveis em memória (`NameError`) e refatoração de contratos de dados entre módulos (passando o objeto `response.text` do Gemini corretamente para o `gTTS`).
* **Segurança:** Implementação da biblioteca `google.colab.userdata` para injeção segura de credenciais.

---
*Projeto desenvolvido como parte de um laboratório prático de IA e Python.*

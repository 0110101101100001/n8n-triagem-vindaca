# 🤖 Bot de Triagem Inteligente - Instituição Vidança

![Arquitetura do Fluxo no n8n](image_45333f.png)

## 📌 Sobre o Projeto
Este projeto consiste na arquitetura de um assistente virtual conversacional baseado em WhatsApp, desenvolvido para automatizar a triagem e o cadastro de moradores atendidos pela **Instituição Vindaça**, localizada em Fortaleza - CE. 

O foco do desenvolvimento é fornecer um atendimento empático, humanizado e acessível (com forte suporte a interações por áudio), garantindo que os assistentes sociais recebam os dados estruturados em tempo real.

## ⚙️ Tecnologias e Integrações
O fluxo foi desenhado utilizando o **n8n** como motor de orquestração de APIs e integra os seguintes serviços:

*   **Groq Cloud (Whisper-large-v3):** Responsável pelo *Speech-to-Text* (STT). A API foi injetada com prompts de contexto regional para maximizar a precisão ao transcrever o sotaque cearense, gírias e nomes específicos de bairros de Fortaleza.
*   **ElevenLabs (Multilingual V2):** Responsável pelo *Text-to-Speech* (TTS). Utilizado na fase de validação para gerar respostas de áudio naturais e acolhedoras para usuários com dificuldade de leitura.
*   **LLM (Agente IA):** Responsável por conduzir a entrevista de triagem, extraindo parâmetros obrigatórios e gerenciando o contexto da conversa.
*   **Google Sheets API:** Banco de dados temporário para armazenamento das respostas da triagem.

## 🧠 Lógica e Estrutura do Fluxo
1. **Roteamento Condicional:** Um nó `Switch` identifica a entrada do usuário. Se for áudio, a mídia binária é enviada via requisição HTTP (Multipart/Form-Data) para a API do Groq. Se for texto, segue o fluxo normal.
2. **Memória de Sessão:** Utilização dos nós `Chat Memory Manager` e `Clear Message History` para garantir que o bot não confunda dados de diferentes atendimentos e zere o contexto ao finalizar um cadastro.
3. **Extração de Dados:** O `Information Extractor` atua garantindo que o Agente IA colete perfeitamente os quatro pontos focais: Nome, Idade, Bairro e Necessidade (Oficina/Ajuda).

## 🚀 Próximos Passos (Roadmap de Infraestrutura)
Este repositório contém o arquivo JSON exportado da validação inicial no n8n Cloud. As próximas fases de engenharia de software incluem:

- [ ] **Migração Local (Self-Hosted):** Configuração do ambiente via Docker.
- [ ] **Integração WhatsApp:** Substituição de gatilhos webhooks genéricos pela **Evolution API** rodando no mesmo ecossistema local.
- [ ] **Otimização de Custos:** Substituição da API do ElevenLabs (limitada/paga) por soluções locais abertas como o Edge-TTS da Microsoft.
- [ ] **Visualização de Dados:** Construção de um Dashboard analítico para cruzamento das demandas por bairros de Fortaleza.

## 👨‍💻 Desenvolvedor
**Kaíque Nunes Vasconcelos Fraga**  
Estudante de Data Science e Desenvolvedor de Software.

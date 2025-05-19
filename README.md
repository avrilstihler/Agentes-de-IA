# Sistema de Geração de Posts para Instagram com Agentes IA (Gemini)

Este projeto demonstra um sistema multi-agente construído com Google Gemini e o Google Agent Development Kit (ADK) para gerar rascunhos de posts para Instagram sobre um tópico específico fornecido pelo usuário. O sistema utiliza uma cadeia de quatro agentes especializados para pesquisar, planejar, redigir e revisar o conteúdo.

## Funcionalidades

*   **Interação com Google Gemini:** Utiliza o modelo `gemini-2.0-flash` para tarefas de geração de texto e raciocínio.
*   **Busca Integrada:** Demonstra o uso da ferramenta de busca do Google diretamente com a API do Gemini e como ferramenta dentro dos agentes ADK para obter informações atualizadas.
*   **Framework de Agentes (ADK):** Implementa um pipeline com quatro agentes distintos, cada um com uma responsabilidade específica:
    1.  **Agente Buscador de Notícias:** Pesquisa lançamentos e notícias recentes sobre o tópico.
    2.  **Agente Planejador de Posts:** Analisa os lançamentos, aprofunda-se nos temas e escolhe o mais relevante para criar um plano de post.
    3.  **Agente Redator do Post:** Cria um rascunho de post para Instagram com base no plano, focado em engajamento e no tom da Alura.
    4.  **Agente Revisor de Qualidade:** Revisa o rascunho, verificando clareza, concisão, correção e adequação ao público-alvo.
*   **Execução em Google Colab:** O código é projetado para ser executado em um ambiente Google Colaboratory.

## Tecnologias Utilizadas

*   Python
*   Google Gemini API (`google-genai`)
*   Google Agent Development Kit (`google-adk`)
*   Google Search (como ferramenta dos agentes e da API)
*   Google Colaboratory

## Pré-requisitos

1.  **Ambiente:** Google Colaboratory.
2.  **API Key do Google Gemini:** Você precisará de uma API Key válida do Google Gemini.
    *   No Google Colab, esta chave deve ser armazenada como um "Secret" com o nome `GOOGLE_API_KEY`. O script acessa essa chave usando `userdata.get('GOOGLE_API_KEY')`.
3.  **Bibliotecas Python:** As seguintes bibliotecas são instaladas e utilizadas:
    *   `google-genai`
    *   `google-adk`
    *   `requests` (dependência implícita ou para futuras expansões)
    *   `IPython` (para display no Colab)

## Configuração

1.  **Obtenha sua API Key:** Acesse [Google AI Studio](https://aistudio.google.com/app/apikey) para criar e obter sua API Key.
2.  **Configure no Colab:**
    *   No seu notebook Colab, clique no ícone de chave (🔑) na barra lateral esquerda ("Secrets").
    *   Adicione um novo secret com o nome `GOOGLE_API_KEY` e cole sua chave no campo "Value".
    *   Certifique-se de que a opção "Notebook access" está habilitada para este secret.

## Como Executar

1.  Abra o notebook (`.ipynb`) no Google Colaboratory.
2.  Certifique-se de que sua `GOOGLE_API_KEY` está configurada nos Secrets do Colab (conforme descrito acima).
3.  Execute as células do notebook em ordem:
    *   A primeira célula instala a biblioteca `google-genai`.
    *   As células seguintes configuram a API Key e o cliente Gemini.
    *   As células de demonstração inicial mostram como consultar o Gemini diretamente, com e sem a ferramenta de busca.
    *   A célula seguinte instala o `google-adk`.
    *   As células subsequentes definem as bibliotecas importadas, funções auxiliares e os quatro agentes.
    *   A célula final do script principal irá:
        *   Solicitar que você digite um **TÓPICO** para o post.
        *   Executar a cadeia de agentes sequencialmente.
        *   Exibir a saída de cada agente.

## Fluxo de Trabalho dos Agentes

O sistema opera através de uma sequência de quatro agentes:

1.  **Agente Buscador de Notícias (`agente_buscador`)**
    *   **Entrada:** Tópico fornecido pelo usuário e a data atual.
    *   **Tarefa:** Utiliza a ferramenta `google_search` para encontrar os lançamentos mais recentes (último mês) e relevantes (máximo 5) sobre o tópico. Foca na quantidade e entusiasmo das notícias.
    *   **Saída:** Uma lista de lançamentos relevantes.

2.  **Agente Planejador de Posts (`agente_planejador`)**
    *   **Entrada:** Tópico e a lista de lançamentos do Agente Buscador.
    *   **Tarefa:** Utiliza `google_search` para pesquisar pontos relevantes para um post sobre cada lançamento. Aprofunda-se nos temas e escolhe o tema mais relevante, retornando um plano detalhado para o post.
    *   **Saída:** O tema escolhido, seus pontos mais relevantes e um plano de assuntos para o post.

3.  **Agente Redator do Post (`agente_redator`)**
    *   **Entrada:** Tópico e o plano de post do Agente Planejador.
    *   **Tarefa:** Assume o papel de um redator criativo da Alura. Escreve um rascunho de post para Instagram (engajador, informativo, linguagem simples, 2-4 hashtags).
    *   **Saída:** Um rascunho do post para Instagram.

4.  **Agente Revisor de Qualidade (`agente_revisor`)**
    *   **Entrada:** Tópico e o rascunho do post do Agente Redator.
    *   **Tarefa:** Atua como um editor meticuloso. Revisa o rascunho considerando clareza, concisão, correção e tom adequado para um público jovem (18-30 anos). Se o rascunho estiver bom, aprova. Caso contrário, aponta problemas e sugere melhorias.
    *   **Saída:** A versão final do post ou o rascunho com sugestões de melhoria.

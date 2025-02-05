# Assistente de Pesquisa Assíncrono com Gemini

Este script Python implementa um assistente de pesquisa assíncrono que utiliza a API Gemini para processamento de linguagem natural, a SERPAPI para pesquisa na web e a Jina AI para buscar conteúdo de páginas web. Ele automatiza o processo de pesquisa de um tópico online e gera um relatório detalhado em Markdown resumindo as descobertas.

## Funcionalidades

*   **Geração Automatizada de Consultas de Busca:** Utiliza o Gemini para gerar consultas de busca relevantes e precisas com base no tópico de pesquisa do usuário.
*   **Pesquisa Iterativa na Web:** Realiza buscas iterativas utilizando a SERPAPI, refinando as consultas e explorando os resultados da web para coletar informações abrangentes.
*   **Busca de Conteúdo de Páginas Web:** Emprega a Jina AI para buscar e extrair de forma eficiente o conteúdo textual das páginas web identificadas nos resultados da busca.
*   **Avaliação de Relevância:** Utiliza o Gemini para avaliar a relevância do conteúdo da página web para a consulta de pesquisa original, filtrando informações irrelevantes.
*   **Extração de Contexto:** Extrai contextos-chave e relevantes de páginas web úteis utilizando o Gemini, com foco em informações pertinentes ao tópico da pesquisa.
*   **Geração de Relatório:** Gera um relatório final bem estruturado e detalhado em formato Markdown, resumindo as informações e insights coletados.
*   **Operações Assíncronas:** Utiliza programação assíncrona para chamadas de API e operações web eficientes e concorrentes, acelerando o processo de pesquisa.
*   **Integrações de API:** Integra-se perfeitamente com:
    *   **API Gemini:** Para compreensão de linguagem natural, geração de consultas, avaliação de relevância, extração de contexto e redação de relatórios.
    *   **SERPAPI:** Para realizar buscas no Google e recuperar os resultados da busca.
    *   **Jina AI:** Para recuperação eficiente e autorizada de conteúdo de páginas web.

## Dependências

Antes de executar o script, certifique-se de ter as seguintes bibliotecas Python instaladas. Você pode instalá-las usando pip:

```bash
pip install nest_asyncio aiohttp google-generativeai ipython
```

*   **`nest_asyncio`:** Permite executar código assíncrono em ambientes que não estão totalmente prontos para async, como notebooks Jupyter ou scripts executados com `nest_asyncio.apply()`.
*   **`aiohttp`:** Um framework cliente/servidor HTTP assíncrono usado para fazer requisições de API eficientes e buscar conteúdo da web de forma concorrente.
*   **`google-generativeai`:** A biblioteca Python oficial para interagir com a API Gemini do Google.
*   **`ipython`:** Fornece `IPython.display.Markdown` para renderizar a saída Markdown em ambientes como Jupyter Notebooks e consoles que suportam a exibição de Markdown.

## Configuração das Chaves de API

Para usar este assistente de pesquisa, você precisa de chaves de API para os seguintes serviços:

1.  **Chave da API Gemini:**
    *   Obtenha uma chave de API do [Google AI Studio](https://makersuite.google.com/app/apikey).
    *   Substitua o marcador `"YOUR_GEMINI_API_KEY"` no script pela sua chave de API Gemini real.

2.  **Chave da API SERPAPI:**
    *   Inscreva-se para uma conta gratuita ou paga em [serpapi.com](https://serpapi.com).
    *   Obtenha sua chave de API no seu painel SERPAPI.
    *   Substitua o marcador `"REDACTED"` para `SERPAPI_API_KEY` no script pela sua chave de API SERPAPI.

3.  **Chave da API Jina AI:**
    *   Obtenha uma chave de API Jina AI de [r.jina.ai](https://r.jina.ai/).
    *   Substitua o marcador `"REDACTED"` para `JINA_API_KEY` no script pela sua chave de API Jina AI.

**Importante:** Armazene suas chaves de API com segurança e evite comprometê-las diretamente no seu repositório. Neste script, espera-se que elas sejam colocadas diretamente como valores de string para fins de demonstração. Para ambientes de produção, considere usar variáveis de ambiente ou gerenciamento de configuração seguro.

## Uso

1.  **Clone ou Baixe o Script:** Baixe o script Python (`nome_do_seu_script.py`) para sua máquina local.

2.  **Instale as Dependências:** Se ainda não o fez, instale as bibliotecas Python necessárias usando pip:
    ```bash
    pip install nest_asyncio aiohttp google-generativeai ipython
    ```

3.  **Defina as Chaves de API:** Abra o script Python em um editor de texto e substitua as strings de espaço reservado da chave de API pelas suas chaves de API reais para Gemini, SERPAPI e Jina AI, conforme descrito na seção "Configuração das Chaves de API".

4.  **Execute o Script:** Execute o script a partir do seu terminal ou ambiente Python. Por exemplo:
    ```bash
    python nome_do_seu_script.py
    ```

5.  **Insira a Consulta de Pesquisa:** Quando solicitado, insira sua consulta ou tópico de pesquisa no terminal e pressione Enter.

    ```
    Insira sua consulta/tópico de pesquisa:  [Seu Tópico de Pesquisa Aqui]
    Insira o número máximo de iterações (padrão 10): [Limite de Iteração Opcional - pressione Enter para o padrão]
    ```

6.  **Visualize o Relatório Markdown:** O script realizará o processo de pesquisa e, após a conclusão, imprimirá o relatório de pesquisa final em formato Markdown no seu console. Se você estiver executando o script em um Jupyter Notebook ou ambiente compatível, a saída será renderizada como Markdown formatado.

## Explicação do Código (Breve Visão Geral)

O script está estruturado nos seguintes componentes principais:

*   **Constantes de Configuração:** Define as chaves de API, os endpoints da API e as configurações padrão do modelo.
*   **Funções Auxiliares Assíncronas:** Contém funções para:
    *   `call_gemini_async`: Lida com chamadas assíncronas para a API Gemini.
    *   `generate_search_queries_async`: Gera consultas de busca iniciais usando o Gemini.
    *   `perform_search_async`: Executa buscas usando a SERPAPI.
    *   `fetch_webpage_text_async`: Busca o conteúdo da página web usando a Jina AI.
    *   `is_page_useful_async`: Avalia a relevância da página web usando o Gemini.
    *   `extract_relevant_context_async`: Extrai o contexto relevante das páginas web usando o Gemini.
    *   `get_new_search_queries_async`: Determina se buscas adicionais são necessárias e gera novas consultas usando o Gemini.
    *   `generate_final_report_async`: Gera o relatório final em Markdown usando o Gemini com base nos contextos coletados.
    *   `process_link`: Orquestra o processamento de um único link de página web (busca, avaliação, extração).
*   **Rotina Assíncrona Principal (`async_main`):**
    *   Recebe a entrada do usuário para a consulta de pesquisa e o limite de iteração.
    *   Inicia o processo de pesquisa gerando consultas de busca iniciais.
    *   Entra em um loop iterativo para realizar buscas, processar links e refinar consultas de busca.
    *   Gera o relatório final após a conclusão do loop de pesquisa.
*   **Função `main()`:**
    *   Executa a função `async_main` usando `asyncio.run()`.
    *   Recebe a string do relatório Markdown de `async_main`.
    *   Imprime o relatório Markdown no console ou o renderiza usando `IPython.display.Markdown` se estiver em um ambiente adequado.

## Exemplo de Saída (Markdown)

```markdown
# Briefing de Notícias sobre Inteligência Artificial - 05 de Fevereiro de 2025

Este briefing apresenta um resumo das principais notícias e desenvolvimentos relacionados à Inteligência Artificial (IA) nesta data.

**1. Mudanças na Política de IA do Google:**

*   O Google removeu de seus princípios de IA a cláusula que proibia o uso da tecnologia para o desenvolvimento de armas e vigilância.
*   Especialistas como Margaret Mitchell (ex-Google) criticam a mudança, alertando sobre o potencial uso da IA em tecnologias que podem causar danos.
*   Executivos do Google, como James Manyika e Demis Hassabis, defendem que democracias devem liderar o desenvolvimento de IA com base em valores como liberdade e direitos humanos.
*   ... (resto do conteúdo do relatório) ...
```

## Aviso Legal

*   **Uso da API e Custos:** Esteja atento aos limites de uso e aos custos potenciais associados às APIs Gemini, SERPAPI e Jina AI, especialmente se você estiver usando planos pagos ou exceder as cotas gratuitas.
*   **Tratamento de Erros:** O script inclui tratamento de erros básico, mas as interações de API e o web scraping do mundo real podem encontrar vários problemas (problemas de rede, limites de API, alterações no site, etc.). Você pode precisar aprimorar o tratamento de erros para uma operação robusta.
*   **Ambiente de Renderização Markdown:** Para que a formatação Markdown seja renderizada corretamente, você deve executar o script em um ambiente que suporte a exibição Markdown, como um Jupyter Notebook, JupyterLab ou um terminal que suporte a saída Markdown.

---

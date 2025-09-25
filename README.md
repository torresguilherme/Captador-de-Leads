🚀 Fluxo de Captura e Enriquecimento de Leads com n8n
Este repositório contém um fluxo de trabalho (workflow) construído na plataforma de automação n8n. O objetivo principal deste fluxo é capturar dados de leads enviados através de um formulário, enriquecer essas informações usando a API da Apify e, por fim, salvar os dados consolidados em uma planilha do Google Sheets.

✨ Visão Geral do Fluxo
O processo é ideal para equipes de marketing e vendas que desejam automatizar a coleta de leads e garantir que os dados sejam o mais completos possível antes de qualquer contato.

(Nota: Substitua o link acima pelo link da sua imagem no repositório, se desejar)

⚙️ Detalhamento do Fluxo
O workflow é composto por 5 etapas principais:

On form submission (Gatilho):

Tipo: Webhook.

Função: O fluxo é iniciado sempre que um novo formulário é preenchido e enviado. Este gatilho gera uma URL única que deve ser configurada no seu serviço de formulários (ex: Webflow, Typeform, JotForm, formulário HTML próprio).

Dados (Nó Manual):

Tipo: Set / Edit Fields.

Função: Este nó é usado para preparar os dados recebidos do formulário. Pode ser utilizado para renomear campos, extrair informações específicas (como o domínio de um e-mail) ou definir valores estáticos que serão usados nas etapas seguintes.

Buscar Apify (Nó de Requisição HTTP):

Tipo: HTTP Request.

Função: O coração do enriquecimento. Este nó faz uma chamada GET para a API da Apify. Ele provavelmente envia um dado chave do lead (como o nome da empresa ou o domínio do site) para um "Actor" da Apify, que por sua vez busca informações públicas adicionais, como setor, número de funcionários, localização, tecnologias utilizadas, etc.

Edit Fields (Nó Manual):

Tipo: Set / Edit Fields.

Função: Após receber a resposta da Apify, este nó organiza e formata os novos dados. Ele extrai as informações relevantes do objeto JSON retornado pela API e as combina com os dados originais do formulário, preparando um conjunto de dados limpo e completo.

Gravar (Nó do Google Sheets):

Tipo: Google Sheets.

Função: A etapa final. Este nó se conecta à sua conta do Google e adiciona uma nova linha (append: sheet) na planilha designada. Cada coluna da planilha é preenchida com os dados do lead, tanto os originais quanto os enriquecidos pela Apify.

🔧 Pré-requisitos
Para utilizar este fluxo, você precisará de:

Uma instância do n8n (seja no n8n.cloud ou auto-hospedada).

Uma conta na Apify com um token de API.

Uma conta do Google com as credenciais de API configuradas no n8n para acesso ao Google Sheets.

Um formulário web configurado para enviar dados via webhook.

🚀 Como Configurar
Importe o Fluxo: Copie o código JSON do workflow e importe-o para a sua instância do n8n.

Configure o Gatilho (Webhook): Ative o fluxo e copie a URL de webhook gerada no primeiro nó. Cole essa URL na configuração do seu serviço de formulário.

Configure o Nó "Buscar Apify":

Insira seu token da API da Apify nas credenciais do nó de Requisição HTTP (geralmente em "Authentication" > "Header Auth").

Ajuste a URL para corresponder ao "Actor" específico que você deseja executar.

Mapeie o dado que será usado na busca (ex: {{ $json.body.company_domain }}).

Configure o Nó "Google Sheets":

Autentique sua conta do Google.

Selecione o "Spreadsheet ID" (ID da Planilha) e o "Sheet Name" (Nome da Aba).

Mapeie os campos dos nós anteriores para as colunas correspondentes da sua planilha.

Ative o Workflow: Salve as alterações e ative o fluxo no botão superior.

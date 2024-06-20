# agente_local_GenAI
Para acessar arquivos no Google Drive a partir de uma aplicação Python, você pode usar a API do Google Drive. A biblioteca pydrive é uma ferramenta conveniente para essa finalidade. Aqui estão os passos detalhados para configurar e acessar arquivos do Google Drive.

Passo 1: Configuração do Google Cloud Console
Criar um Projeto no Google Cloud Console:

Acesse o Google Cloud Console.
Crie um novo projeto ou selecione um projeto existente.
Habilitar a API do Google Drive:

No painel do Google Cloud Console, vá para "APIs e Serviços" > "Biblioteca".
Pesquise "Google Drive API" e clique em "Habilitar".
Configurar a Tela de Consentimento OAuth:

Vá para "APIs e Serviços" > "Tela de consentimento OAuth".
Configure as informações necessárias (nome do aplicativo, e-mail de suporte, etc.) e salve.
Criar Credenciais OAuth 2.0:

Vá para "APIs e Serviços" > "Credenciais".
Clique em "Criar credenciais" e selecione "ID do Cliente OAuth".
Escolha "Aplicativo da Web" e configure o URI de redirecionamento autorizado. Se estiver em desenvolvimento local, use http://localhost.
Baixar o arquivo de credenciais JSON:

Após criar as credenciais, baixe o arquivo JSON que contém suas credenciais do cliente OAuth.

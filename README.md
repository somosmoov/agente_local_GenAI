# agente_local_GenAI
Para acessar arquivos no Google Drive a partir de uma aplicação Python, você pode usar a API do Google Drive. A biblioteca `pydrive` é uma ferramenta conveniente para essa finalidade. Aqui estão os passos detalhados para configurar e acessar arquivos do Google Drive.

### Passo 1: Configuração do Google Cloud Console

1. **Criar um Projeto no Google Cloud Console**:
   - Acesse o [Google Cloud Console](https://console.developers.google.com/).
   - Crie um novo projeto ou selecione um projeto existente.

2. **Habilitar a API do Google Drive**:
   - No painel do Google Cloud Console, vá para "APIs e Serviços" > "Biblioteca".
   - Pesquise "Google Drive API" e clique em "Habilitar".

3. **Configurar a Tela de Consentimento OAuth**:
   - Vá para "APIs e Serviços" > "Tela de consentimento OAuth".
   - Configure as informações necessárias (nome do aplicativo, e-mail de suporte, etc.) e salve.

4. **Criar Credenciais OAuth 2.0**:
   - Vá para "APIs e Serviços" > "Credenciais".
   - Clique em "Criar credenciais" e selecione "ID do Cliente OAuth".
   - Escolha "Aplicativo da Web" e configure o URI de redirecionamento autorizado. Se estiver em desenvolvimento local, use `http://localhost`.

5. **Baixar o arquivo de credenciais JSON**:
   - Após criar as credenciais, baixe o arquivo JSON que contém suas credenciais do cliente OAuth.

### Passo 2: Configuração do Ambiente Python

1. **Instalar as Bibliotecas Necessárias**:
   - Instale as bibliotecas `pydrive` e `oauth2client` usando pip:
     ```sh
     pip install pydrive oauth2client
     ```

2. **Configurar e Autenticar a Aplicação**:
   - Use o seguinte código Python para autenticar e acessar arquivos do Google Drive:

```python
from pydrive.auth import GoogleAuth
from pydrive.drive import GoogleDrive

def autenticar_google_drive():
    # Autentica e cria o serviço PyDrive
    gauth = GoogleAuth()
    
    # Tenta carregar credenciais salvas
    gauth.LoadCredentialsFile("mycreds.txt")
    if gauth.credentials is None:
        # Autenticação local.
        gauth.LocalWebserverAuth()
    elif gauth.access_token_expired:
        # Refresh as credenciais se estiverem expiradas.
        gauth.Refresh()
    else:
        # Usar credenciais salvas
        gauth.Authorize()
    
    # Salva as credenciais para a próxima execução
    gauth.SaveCredentialsFile("mycreds.txt")
    
    drive = GoogleDrive(gauth)
    return drive

def listar_arquivos(drive, pasta_id=None):
    # Lista os arquivos na pasta especificada. Se pasta_id for None, lista no raiz.
    query = f"'{pasta_id}' in parents and trashed=false" if pasta_id else "trashed=false"
    file_list = drive.ListFile({'q': query}).GetList()
    
    for file in file_list:
        print(f'Title: {file["title"]}, ID: {file["id"]}')
    return file_list

# Autentica e cria o serviço do Google Drive
drive = autenticar_google_drive()

# Lista os arquivos na pasta raiz do Google Drive
arquivos = listar_arquivos(drive)
```

### Passo 3: Executar a Aplicação

1. **Autenticação Inicial**:
   - Execute o script pela primeira vez. Ele abrirá uma janela do navegador para você fazer login na sua conta do Google e conceder permissões de acesso.
   - Após a autenticação, um arquivo `mycreds.txt` será criado para armazenar as credenciais para futuras execuções.

2. **Listar Arquivos**:
   - Após a autenticação, o script listará os arquivos na pasta raiz do seu Google Drive. Você pode modificar o `pasta_id` para listar arquivos em uma pasta específica.

### Notas Adicionais

- **Segurança**: Certifique-se de manter suas credenciais em segurança e não compartilhá-las.
- **Escopos de API**: Dependendo das suas necessidades, você pode ajustar os escopos de acesso ao Google Drive na configuração do OAuth.
- **Uso em Produção**: Para um ambiente de produção, considere métodos mais seguros de armazenamento de credenciais e controle de acesso.

Seguindo esses passos, você conseguirá acessar e manipular arquivos no Google Drive a partir de uma aplicação Python.


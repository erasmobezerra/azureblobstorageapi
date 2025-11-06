# 🚀 Azure Blob Storage API

Projeto desenvolvido no curso da DIO "Armazenamento de Dados na Azure". Uma API de exemplo em ASP.NET Core que demonstra o uso do Azure Blob Storage para upload, download, listagem e remoção de arquivos.

## 🎯 Objetivo

Projeto simples para gerenciar arquivos em um container do Azure Blob Storage. Serve como referência para integrar aplicações .NET com Azure Blob Storage usando o pacote `Azure.Storage.Blobs`.

## 🏗️ Estrutura do projeto

- `Controllers/ArquivosController.cs` — Endpoints REST para upload, download, listagem e exclusão de arquivos.
- `BlobDto.cs` — DTO retornado no endpoint de listagem (nome, tipo e URI).
- `Program.cs` — Configuração mínima do ASP.NET Core (Controllers, Swagger).
- `appsettings.json` / `appsettings.Development.json` — Configurações (connection strings).

## 🧰 Tecnologias

- .NET 9
- C#
- Azure.Storage.Blobs (pacote NuGet)
- Swagger (Swashbuckle) para exploração dos endpoints em desenvolvimento

## ✅ Requisitos

- .NET 9 SDK instalado
- Conta Azure com Storage Account e um Container (ou Azurite/Storage Emulator para desenvolvimento local)

## ☁️ Criação do recurso no Azure

1. Crie uma Storage Account no portal do Azure.
2. Acesse "Containers" e crie um container (ex.: `meucontainer`) com acesso privado.
3. Copie a Connection String em "Access keys" para usar na aplicação.

Você também pode usar o Azure Storage Explorer para inspecionar o container.

## ⚙️ Configuração necessária

O projeto lê duas chaves em `ConnectionStrings` no `appsettings.json`:

- `BlobConnectionString` — connection string da Storage Account.
- `BlobContainerName` — nome do container a ser usado.

Exemplo mínimo em `appsettings.json`:

```json
{
  "ConnectionStrings": {
    "BlobConnectionString": "<CONNECTION_STRING_AQUI>",
    "BlobContainerName": "meucontainer"
  }
}
```

IMPORTANTE: nunca comite connection strings ou chaves de acesso em repositórios públicos. Use user secrets, variáveis de ambiente ou mecanismos seguros de CI/CD.


## ▶️ Como executar localmente e acessar a documentação com Swagger

```powershell
# Clone o repositorio
git clone https://github.com/erasmobezerra/azureblobstorageapi.git

# Restaure as dependencias
cd ./azureblobstorageapi
dotnet restore

# Configure `appsettings.json` (ou variáveis de ambiente) com `BlobConnectionString` e `BlobContainerName`

# Execute o projeto
dotnet watch run
```

## Usar o Azurite para simular Azure Blob Storage API

Para evitar custos com recursos do Azure, você pode simular uma conta de armazenamento local com o **Azurite**. Sigo os passos a seguir:

#### 1. Crie o container com o Azure Storage Explorer

Baixe e instale o Azure Storage Explorer. Em Explorer, acesse Conta de Armazenamento > Emulador - Portas Padrão Local > Conteineres de Blob e crie um novo container de blob chamado "arquivos".

#### 2. Configurar `appsettings.Development.json`

Na raiz do projeto, edite ou crie um arquivo 'appsettings.Development.json' e inclua o json abaixo que contém a string de conexão e o nome do container:

```bash
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "ConnectionStrings": {
    "BlobConnectionString": "UseDevelopmentStorage=true",
    "BlobContainerName": "arquivos"
  }
}
```

#### 3. Instalar Azurite

Para evitar custos com recursos do Azure, você pode simular uma conta de armazenamento local com o **Azurite**:

```bash
npm install -g azurite
```

#### 4. Executar Azurite

```bash
azurite
```

### 3. Abra outro terminal no mesmo diretório raiz e execute o projeto

```bash
dotnet watch run
```

---

## 🔌 Endpoints disponíveis no Swagger

Acesse [https://localhost:7295/swagger/index.html](https://localhost:7295/swagger/index.html) Ou navegue para `/swagger` na URL base da aplicação

- POST `/api/Arquivos/Upload` — Upload de arquivo (form field `arquivo` do tipo multipart/form-data). Retorna a URI do blob.
- GET `/api/Arquivos/Download/{nome}` — Download do arquivo pelo nome.
- DELETE `/api/Arquivos/Apagar/{nome}` — Deleta o arquivo pelo nome.
- GET `/api/Arquivos/Listar` — Lista arquivos no container. Retorna array de objetos `BlobDto` com propriedades: `Nome`, `Tipo`, `Uri`.

## 🤝 Como contribuir

1. Crie uma branch com nome descritivo: `feature/minha-mudanca`.  
2. Faça commits pequenos e claros.  
3. Abra Pull Request descrevendo o que foi alterado e por quê.  

----

🙏 Agradeço profundamente à **Digital Innovation One** por proporcionar este aprendizado gratuito e de qualidade. Um reconhecimento especial ao professor **[Leonardo Buta](https://www.linkedin.com/in/leonardo-buta/)** pela excelente didática e orientação durante todo o processo.

<div align="center">
  <p>⭐ Se este projeto foi útil para você, considere dar uma estrela!</p>
</div>

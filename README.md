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

Você também pode usar o Azure Storage Explorer para inspecionar blobs ou Azurite para rodar localmente.

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

## 🔌 Endpoints disponíveis no Swagger

Acesse [https://localhost:7295/swagger/index.html](https://localhost:7295/swagger/index.html) Ou navegue para `/swagger` na URL base da aplicação

- POST `/api/Arquivos/Upload` — Upload de arquivo (form field `arquivo` do tipo multipart/form-data). Retorna a URI do blob.
- GET `/api/Arquivos/Download/{nome}` — Download do arquivo pelo nome.
- DELETE `/api/Arquivos/Apagar/{nome}` — Deleta o arquivo pelo nome.
- GET `/api/Arquivos/Listar` — Lista arquivos no container. Retorna array de objetos `BlobDto` com propriedades: `Nome`, `Tipo`, `Uri`.

Observação: ao enviar o arquivo no `Upload`, o nome do blob será o `arquivo.FileName` recebido. Ajuste conforme necessário para evitar colisões de nomes.

## 🤝 Como contribuir

1. Crie uma branch com nome descritivo: `feature/minha-mudanca`.  
2. Faça commits pequenos e claros.  
3. Abra Pull Request descrevendo o que foi alterado e por quê.  

----

🙏 Agradeço profundamente à **Digital Innovation One** por proporcionar este aprendizado gratuito e de qualidade. Um reconhecimento especial ao professor **[Leonardo Buta](https://www.linkedin.com/in/leonardo-buta/)** pela excelente didática e orientação durante todo o processo.

<div align="center">
  <p>⭐ Se este projeto foi útil para você, considere dar uma estrela!</p>
</div>

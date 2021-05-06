<h1> Migração .Net com kubernetes para AWS Lambda Serverless </h1>

<h2>Pré configuração</h2>

- [Instalar o dotnet CLI](https://docs.microsoft.com/pt-br/dotnet/core/tools/) (Já vem configurado quando instala o visual studio) 

- [Instalar o AWS CLI](https://docs.aws.amazon.com/pt_br/cli/latest/userguide/install-cliv2.html) 

- [Configurar o AWS CLI](https://docs.aws.amazon.com/pt_br/cli/latest/userguide/cli-configure-quickstart.html) 

- Instalar ferramento do AWS Lambda no dotnet CLI: 
   `  dotnet tool install -g Amazon.Lambda.Tools`
   
<h2>Configuração</h2> 

- Utilizando terminal, cmd ou powershell, acessar raíz do projeto (pasta com arquivo .csproj). Exemplo: ` cd src/services`

- Adicionar pacote lambda ao projeto: `dotnet add package Amazon.Lambda.AspNetCoreServer`

- Criar utilizando o visual studio, 3 arquivos na raíz do projeto:
    1. `LambdaEntryPoint.cs`
    2. `aws-lambda-tools-defaults.json`
    3. `serverless.template` 
    
 > Observação: A criação dos arquivos com visual studio garante que os arquivos sejam mapeados automaticamente, por isso é importante cria-los manualmente.
 
 - Adicionar dentro dos arquivos criados, o conteúdo dos arquivos desse repositório.
 
 > Caso necessário, ajudar a sessão **Handler** do arquivo **serverless.template** com o nome do projeto. 
 
 - Criar um bucket no S3 onde ficará armazenado o o código **(trocar nome do bucket para cada serviço)**:
 `aws s3 mb s3://service-api-serverless-store --region sa-east-1 
 
<h2>Deploy</h2> 

- Para fazer o deploy utilizar o comando:
`dotnet lambda deploy-serverless ServiceServerless -sb service-api-serverless-store --region sa-east-1`

> Alterar **ServiceServerless** para o nome que você quer dar ao seu projeto, e **service-api-serverless-store** para o nome que foi dado ao bucket no s3.

<h2>Configurações Adicionais</h2> 
Essas configurações podem não ser necessárias em todos os projetos

<h3>Swagger</h3> 

- Acessar o arquivo **Startup.cs** e alterar o SwaggerEndpoint de `/swagger/v1/swagger.json` para `v1/swagger.json`

<h3>AppSettings</h3> 

- Caso o projeto tenha um AppSettings.json com variaveis de ambiente, precisa trocar essas variáveis para valores reais, ou configurar as variáveis dentro da AWS 

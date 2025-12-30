# Manual de Criação de Usuário OCI - Geração do Config para Discovery da CCM

Este repositório contém as instruções necessárias para criar o usuário, grupo, políticas e gerar o arquivo de configuração utilizado pelo time de Engenharia CCM para executar o processo de discovery na Oracle Cloud Infrastructure (OCI).

## Pré-requisitos

Antes de iniciar, certifique-se de possuir:

-   Acesso administrativo ao console da **OCI**
-   Permissão para criar **usuários**, **grupos** e **policies**

## 1. Criação do Grupo

1. Acesse o console da OCI:

        Identity & Security > Domains > Default (ou domínio desejado) > User management > Groups > Create group

2. Preencha as informações:

    -   **Name:** `Consulta`
    -   **Description:** `Grupo para consultas externas`

## 2. Criação do Usuário

Após criar o grupo, crie o usuário responsável pela conexão utilizada no discovery.

1. Acesse:

        Identity & Security > Domains > Default > User management > Users > Create

2.  Informações do usuário:

    -   **First name:** `Consulta`
    -   **Last name:** `CCM`
    -   **Username:** `consulta`
    -   **Email:** *(e-mail desejado)*

3.  Adicione o usuário ao grupo **Consulta**.

## 3. Geração da API Key

Com o usuário criado:

1. Na tela do usuário, acesse:

        API keys > Add API key

2. Escolha:

    -   **Generate API key pair**

3. Clique em **Download private key** para salvar o arquivo `.PEM`.

4. Após o download, clique em **Add** para gerar o arquivo de configuração contendo:

    -   Tenancy OCID\
    -   User OCID\
    -   Fingerprint da chave pública\
    -   Caminho do arquivo de chave privada

5. Clique em **Copy** e salve o conteúdo em um arquivo `.TXT`.

### IMPORTANTE
Envie para o time de Engenharia CCM:

-   O arquivo **.PEM**
-   O arquivo **.TXT** contendo o conteúdo de configuração

## 4. Criação da Policy

Para liberar o acesso do usuário criado, configure a Policy apropriada.

1.  Acesse:

        Identity & Security > Policies > Create Policy

2.  Preencha:

    -   **Name:** `policy-consulta`

    -   **Description:**
        `Policy para liberação de acesso ao grupo Consulta`

    -   **Compartment:** *(compartimento desejado)*

    -   **Policy Statement:**

            Allow group Consulta to read all-resources in tenancy

## Conclusão

Após seguir todas as etapas acima, o ambiente estará pronto para permitir que o time da CCM execute o processo de discovery utilizando as credenciais e configurações geradas.

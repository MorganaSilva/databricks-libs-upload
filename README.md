# Ways to Upload Libs to Databricks

1. Utilizando o Maven

Se você precisa de uma biblioteca Java/Scala hospedada em um repositório Maven, siga os passos abaixo:

    Vá para o workspace no Databricks.
    Clique em Compute e selecione o cluster onde deseja adicionar a biblioteca.
    Clique na aba Libraries e em Install New.
    Escolha a opção Maven e forneça o artifact ID no formato:

groupId:artifactId:version

Exemplo para o Spark XML:

    com.databricks:spark-xml_2.12:0.15.0

2. Carregando Bibliotecas Python (PyPI)

Se você precisa instalar bibliotecas Python do PyPI:

    No Databricks, acesse o menu Compute e selecione o cluster.

    Vá para a aba Libraries e clique em Install New.

    Escolha PyPI e insira o nome do pacote, por exemplo:

    pandas==1.5.2

    Você também pode especificar múltiplas bibliotecas em um arquivo .txt e instalá-las em massa via script.

3. Carregando Bibliotecas Personalizadas

Se você possui uma biblioteca customizada, pode carregá-la de duas maneiras:
a) Upload do arquivo JAR/WHL

    Construa sua biblioteca (JAR para Java/Scala ou WHL para Python).
    Faça o upload do arquivo diretamente na aba Libraries do cluster.
    Clique em Install New > Upload e selecione o arquivo.

b) Utilizando o DBFS (Databricks File System)

    Faça o upload da biblioteca para o DBFS usando o comando:

dbutils.fs.cp("file:/path/to/library.whl", "dbfs:/FileStore/libraries/")

Instale a biblioteca no cluster usando:

    %pip install /dbfs/FileStore/libraries/library.whl

4. Instalando Dependências em Notebooks

Caso você queira instalar bibliotecas diretamente em um notebook:

    Use %pip para bibliotecas Python:

    %pip install nome-da-biblioteca

    Para dependências Java/Scala, utilize um init script ou configure o cluster.

5. Usando Init Scripts

Para gerenciar dependências complexas ou instalar bibliotecas antes que o cluster seja iniciado:

    Crie um init script com os comandos necessários (exemplo para instalar pacotes via apt ou pip).
    Faça o upload do script no DBFS:

    dbutils.fs.put("/databricks/init/myscript.sh", "conteúdo_do_script", True)

    Configure o cluster para usar o script em Advanced Options > Init Scripts.

6. Usando Repositórios de Controle de Versão

Se a biblioteca está em um repositório Git, como o GitHub, você pode cloná-lo diretamente no Databricks:

    Configure o Git em Repos.
    Clone o repositório com o comando:

%sh git clone https://github.com/user/repo.git

Instale a biblioteca com %pip install ou use diretamente no código.

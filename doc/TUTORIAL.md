E5R.Sample.AspNet Tutorial
==========================

Neste tutorial veremos como iniciar um novo projeto nos padrões **E5R Development Team**. Usaremos o conceito de *Baby steps*, executando um passo de cada vez e evoluindo nosso entendimento. Este repositório conterá o resultado final do tutorial, e ao fim da execução de cada passo nós teremos uma nova *tag* refletindo esse estado, de forma que você poderá voltar o estado do repositório para o momento exato da execução de cada passo e prosseguir com seus estudos no seu rítmo.

***Vamos aos estudos!***

## Step1 - Preparando o ambiente

> Este passo está disponível na tag **`step1`**.

Todo o ambiente *E5R Development Team* é gerenciado pela coleção de scripts **E5R Environment**. Siga as instruções em [e5r.github.io/env](https://e5r.github.io/env) para preparar o ambiente.

Certifique-se que o ambiente está disponível, digitando o seguinte comando e verificando sua saída:

```shell
e5r help
```

A saída será algo semelhante a isto:

```
E5R Environment - Version 0.1.0-alpha1

Copyright (c) 2014 E5R Development Team

E5R Environment, is a collection of scripts to automate tasks
that relate to the development of E5R Development Team.
But that can easily be used by any developer (or development
team) wishing to apply concepts and patterns of development
used by E5R Development Team for their projects.

Usage:
   e5r <command> [options]

Commands:
   help             Show this information

   skeleton         Provides methods to create the basic structure
                    for your projects and components

   env              Manages the installation / uninstallation and
                    selection of several versions of your
                    development environment
```

## Step2 - Criando o esqueleto da aplicação

> Este passo está disponível na tag **`step2`**.

Você não precisa se preocupar em criar a maioria dos arquivos e diretórios estruturantes do projeto, isso porque *E5R Environment* nos disponibiliza uma ferramenta útil para esse fim, chamada **skeleton**.

**Skeleton** irá estruturar seu diretório de trabalho, baixar os arquivos modelo da web (_e guardá-los em cache para uso posteriormente de forma mais rápida_), além de preencher script que configuram variáveis de ambiente, build, etc.

Crie o diretório do projeto:

> Usaremos este próprio projeto (E5R.Sample.AspNet) como exemplo, mas você poderá usar o seu próprio projeto.

```shell
mkdir 'E5R.Sample.AspNet'
cd 'E5R.Sample.AspNet'
```

Já dentro do diretório (_que deve estar vazio_), execute o comando a seguir:

```shell
e5r skeleton -init -tech aspnet -license MIT
```

* `e5r skeleton` é o comando principal, seguindo temos os seguintes argumentos:
    - `-init` Indica a tarefa de inicializar nosso diretório atual;
    - `-tech aspnet` Indica que estamos usando a *tecnologia* **aspnet**;
    - `-license MIT` Indica que o projeto será licenciado sob a *The MIT License*.

Se tudo correu como o esperado, você deverá ver a mensagem *E5R Skeleton <aspnet> initialized successfully!*. Isso indica que nosso projeto já tem um esqueleto parecido com a estrutura abaixo:

```
E5R.Sample.AspNet/
+---.e5r/
|       env
|       tech
+---doc/
+---src/
+---test
    build.cmd
    global.json
    LICENSE.md
    makefile.shade
    nuget.config
    packages.config
    README.md
```

### Analisando o esqueleto do novo projeto

Como o nome sugere, é somente o *esqueleto* de um novo projeto, mas já é minimamente funcional, e de agora em diante só nos exige que criemos os componentes de nosso software, e customizemos as tarefas específicas. O objetivo da ferramenta não é criar um projeto modelo (como os templates padrões do [Visual Studio](http://visualstudio.com)), mas somente o conteúdo básico e comum, seguindo os padrões que todos os projetos *E5R* exigem.

Vejamos então cada item do esqueleto:

* O diretório `.e5r` contém informações úteis para agilizar o uso das ferramentas *E5R Environment*:
    - O arquivo `tech` contém o nome da tecnologia do projeto (no caso **aspnet**), dessa forma na execução dos próximos comandos dentro do diretório do projeto, não será mais necessário informar o parâmetro `-tech aspnet` pois ele será presumido automaticamente;
    - O arquivo `env` contém uma lista de definições de variáveis de ambiente, esse é o local ideal para definição de variáveis de ambiente *públicas*, ao invés de replicá-los por exemplo, nos scripts de build; a vantagem é que as variáveis serão disponibilizadas para os scripts de build das várias plataformas disponíveis para o projeto.
* O diretório `doc` está vazio, mas é reservado para arquivos de documentação do projeto;
* O diretório `src` está vazio, mas é reservado para o código fonte dos vários componentes do projeto;
* O diretório `test` está vazio, mas é reservado para o código fonte dos testes unitários dos componentes do projeto;
* O arquivo `build.cmd` é o script (_pré-pronto_) para construir o software no ambiente *Windows*. Se você executá-lo agora perceberá que é funcional, ele vai baixar as ferramentas necessárias que ainda não estão disponíveis em seu ambiente, também irá procurar, compilar, testar e empacotar o software; ele já faz praticamente tudo que precisamos mas pode ser personalizado sem problemas:
    - Se você executar o script nesse momento verá que ele irá executar, mas acusará uma falha, isso é óbvio, porque ainda não incluimos nenhum componente a nosso projeto;
    - Você também terá o script `build.sh` para a plataformas *Unix* - mas no momento em que este tutorial estava sendo escrito, essa funcionalidade ainda não estava disponível.
* O arquivo `global.json` faz o mapeamento de onde estão os códigos fontes de nossos componentes do software; se você analisá-lo verá que aponta para o diretório `src`;
* O arquivo `LICENSE.md` contém o texto de nossa licença de software, no caso `The MIT License`;
* O arquivo `makefile.shade`, é um arquivo **make** e contém as tarefas de construção do sofware propriamente ditas:
    - Saiba mais em [github.com/sakeproject/sake](https://github.com/sakeproject/sake); esse é o mecanismo padrão de construção da equipe [AspNet](https://github.com/aspnet) e também de **E5R Development Team** para projetos desse tipo;
* O arquivo `nuget.config` contém informações úteis para a ferramenta [NuGet](http://nuget.org) (tais como repositórios de pacotes), essa ferramenta é utilizada pelo processo de build (veja o conteúdo do arquivo `build.cmd` por exemplo);
* O arquivo `packages.config` é parecido com `nuget.config`, porém contém referência de pacotes básicos necessários para a construção do software:
    - Nele temos por exemplo a referência ao pacote *Sake* que é a ferramenta usada para construir o projeto usando os passos descritos no arquivo `makefile.shade`.
    - Quando executamos o script de build, ele aciona a ferramenta *NuGet*, que baixa os pacotes listados nesse arquivo (incluindo *Sake*) e então chama por fim a ferramenta *Sake.exe* para terminar o trabalho.
* E por fim, o arquivo `README.md` que é a descrição inicial do projeto.
    - Note que este arquivo não é considerado uma "documentação do projeto", mas deve fornecer informações descritivas sobre o projeto, equipe, ambiente, bootstrap, etc; Você pode criar neste, um link para os arquivos de documentação em si, que se encontram no diretório `doc`.

Quer mais informações sobre **skeleton**?

```shell
e5r skeleton -help
```

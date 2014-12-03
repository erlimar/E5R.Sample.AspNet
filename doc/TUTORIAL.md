E5R.Sample.AspNet Tutorial
==========================

Neste tutorial veremos como iniciar um novo projeto nos padrões **E5R Development Team**. Usaremos o conceito de *Baby steps*, executando um passo de cada vez e evoluindo nosso entendimento. Este repositório conterá o resultado final do tutorial, e ao fim da execução de cada passo nós teremos uma nova *tag* refletindo esse estado, de forma que você poderá voltar o estado do repositório para o momento exato da execução de cada passo e prosseguir com seus estudos no seu rítmo.

***Vamos aos estudos!***

## Step1 - Preparando o ambiente

> Este passo está disponível na tag **[`step1`](https://github.com/erlimar/E5R.Sample.AspNet/tree/step1)**.

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

> Este passo está disponível na tag **[`step2`](https://github.com/erlimar/E5R.Sample.AspNet/tree/step2)**.

Você não precisa se preocupar em criar a maioria dos arquivos e diretórios estruturantes do projeto, isso porque *E5R Environment* nos disponibiliza uma ferramenta útil para esse fim, chamada **skeleton**.

**Skeleton** irá estruturar seu diretório de trabalho, baixar os arquivos modelo da web (_e guardá-los em cache para uso posterior de forma mais rápida_), além de criar scripts de build, configuração de ambiente, etc.

#### 1º. Crie o diretório do projeto

> Usaremos este próprio projeto (E5R.Sample.AspNet) como exemplo, mas você poderá usar o seu próprio projeto.

```shell
mkdir './E5R.Sample.AspNet'
cd './E5R.Sample.AspNet'
```

#### 2º. Gere o esqueleto com a ferramenta Skeleton

Já dentro do diretório (_que deve estar vazio_), execute o comando a seguir:

```shell
e5r skeleton -init -tech aspnet -license MIT
```

* `e5r skeleton` é o comando que executa a ferramenta, e seus parâmetros:
    - `-init` Indica a tarefa de inicializar nosso diretório atual;
    - `-tech aspnet` Indica que estamos usando a *tecnologia* **aspnet**;
    - `-license MIT` Indica que o projeto será licenciado sob a *The MIT License*.

Se tudo correu como o esperado, você deverá ver a mensagem *E5R Skeleton <aspnet> initialized successfully!*. Isso indica que nosso projeto já tem um esqueleto parecido com a estrutura abaixo:

```
E5R.Sample.AspNet/
  |--.e5r/
  |   |-- env
  |   \-- tech
  |--doc/
  |--src/
  |--test/
  |--build.cmd
  |--global.json
  |--LICENSE.md
  |--makefile.shade
  |--nuget.config
  |--packages.config
  \--README.md
```

#### Analisando o esqueleto do novo projeto

Como o nome sugere, é somente o *esqueleto* de um novo projeto, mas já é minimamente funcional, e de agora em diante só nos exige que criemos os componentes de nosso software, e customizemos as tarefas específicas.

> Afinal, ainda somos os programadores! kkk...

O objetivo da ferramenta não é criar um projeto modelo, como os templates padrões do [Visual Studio](http://visualstudio.com), mas somente o conteúdo básico e comum, seguindo os padrões que todos os projetos *E5R* exigem.

Vejamos então cada item do esqueleto.

##### O diretório `.e5r`

Esse diretório contém informações úteis para agilizar o uso das ferramentas *E5R Environment*.

* **tech** `arquivo`: Contém o nome da tecnologia do projeto (no caso **aspnet**), dessa forma na execução dos próximos comandos, não será mais necessário informar o parâmetro `-tech aspnet`, ele será presumido automaticamente;

* **env** `arquivo`: Contém uma lista de definições de variáveis de ambiente, esse é o local ideal para definição de variáveis de ambiente *públicas*, ao invés de replicá-los, por exemplo, nos scripts de build. A vantagem é que as variáveis serão disponibilizadas para os scripts de build das várias plataformas automaticamente;

##### O diretório `doc`

Esse diretório está vazio, mas é reservado para arquivos de documentação do projeto.

##### O diretório `src`

Esse diretório está vazio, mas é reservado para o código fonte dos vários componentes do projeto.

##### O diretório `test`

Esse diretório está vazio, mas é reservado para o código fonte dos testes unitários dos componentes do projeto.

##### Os demais arquivos

* **build.cmd**: É o script (_pré-pronto_) de construção do software no ambiente *Windows*. Se você executá-lo agora perceberá que é funcional, ele vai baixar as ferramentas necessárias que ainda não estão disponíveis em seu ambiente, também irá: procurar, compilar, testar e empacotar o software.
    - Ele já faz praticamente tudo que precisamos mas pode ser personalizado sem problemas;
    - Se você executar o script nesse momento verá que, apesar de executar, acusará uma falha; isso é esperado, porque ainda não incluimos nenhum componente em nosso projeto;
    - Você também terá o script `build.sh` para a plataformas *Unix*, mas no momento em que este tutorial estava sendo escrito, essa funcionalidade ainda não estava disponível.
* **global.json**: Faz o mapeamento de onde estão os fontes de nossos componentes de software; se você analisá-lo verá que aponta para o diretório `src`;
* **LICENSE.md**: Contém o texto de nossa licença de software, no caso `The MIT License`;
* **makefile.shade**, é o **Makefile** com as tarefas de construção do sofware:
    - Saiba mais em [github.com/sakeproject/sake](https://github.com/sakeproject/sake); esse é o mecanismo padrão de construção da equipe [AspNet](https://github.com/aspnet) e também de **E5R Development Team** para projetos AspNet;
    - Se você só está acostumado com [Visual Studio](http://visualstudio.com) e o conceito de **Makefile** é novo pra você, o artigo [MAKEFILES](https://cognitivewaves.wordpress.com/makefiles) talvez seja útil pra você.
* **nuget.config**: [Configurações](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations) da ferramenta [NuGet](http://nuget.org), essa ferramenta é utilizada pelo processo de build (veja o conteúdo do arquivo `build.cmd` por exemplo);
* **packages.config**: Lista de pacotes NuGet primários, necessários para as ferramentas de construção:
    - Nele temos por exemplo a referência ao pacote *Sake* que é a nossa ferramenta **Make**, que por sua vez construirá o software de acordo com os passos descritos no arquivo `makefile.shade`;
    - Quando executamos o script de build, ele aciona a ferramenta *NuGet*, que baixa os pacotes listados nesse arquivo (incluindo *Sake*) e então chama por fim a ferramenta *Sake.exe* para terminar o trabalho.
* **README.md**: É a descrição inicial do projeto:
    - Note que este arquivo não é considerado uma "documentação do projeto", mas deve fornecer informações de descrição do projeto: equipe, ambientes, processos de bootstrap, etc;
    - Você pode criar neste, por exemplo, um link para os arquivos de documentação em si, que se encontram no diretório `doc`.

Quer mais informações sobre **skeleton**?

```shell
e5r skeleton -help
```

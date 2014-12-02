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


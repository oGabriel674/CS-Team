# PHP2Shell — estudo de vulnerabilidades no PHP

## O que é o PHP2Shell?

Em 21 de outubro de 2026, o projeto PHP divulgou duas vulnerabilidades críticas, identificadas como CVE-2026-109618 e CVE-2026-109619. Conhecidas em conjunto como PHP2Shell, essas falhas podem permitir que um atacante execute códigos remotamente em um servidor vulnerável usando apenas requisições HTTP, sem precisar fazer login.

## Como funciona?

As duas falhas ocorrem no gerenciamento de memória do interpretador PHP
quando um erro interrompe o processamento de uma requisição.

> __CVE-2026-109618__: Quando uma alocação de memória falha durante o processamento da requisição, algumas estruturas internas do PHP ficam parcialmente inicializadas. Durante a limpeza, o interpretador pode tratar um campo ainda não inicializado como um endereço válido e tentar liberar uma região indevida da memória.

>__CVE-2026-109619__: Um erro fatal pode interromper a limpeza depois que uma região da memória foi liberada, mas antes que a referência a ela seja removida. Se o PHP usar essa referência posteriormente, poderá acessar uma região que já foi reutilizada para armazenar outros dados. Esse tipo de falha é conhecido como *use-after-free*


Em configurações vulneráveis, esses erros podem alterar informações que o PHP usa para decidir qual função executar em seguida. Se um atacante conseguir influenciar essas informações, pode desviar o fluxo de execução e executar código com as permissões do processo PHP.

## Correção 

As primeiras versões corrigidas foram PHP 8.2.35, 8.3.36, 8.4.27 e 8.5.12.
A correção consiste em atualizar o PHP para uma versão suportada que inclua os patches de segurança que corrigem as falhas no interpretador.

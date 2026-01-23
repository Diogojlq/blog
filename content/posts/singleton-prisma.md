---
title: "O Padrão Singleton na Prática: Otimizando o Prisma Client"
date: 2026-01-23T17:00:00-03:00
draft: false
description: "Descubra como o padrão de projeto Singleton pode salvar a saúde do seu banco de dados ao usar Prisma ORM em aplicações Next.js."
tags: ["Node.js", "Next.js", "TypeScript", "Prisma", "Design Patterns"]
categories: ["Desenvolvimento", "Backend"]
---

No desenvolvimento de uma aplicação minha, um SaaS de agendamentos no qual estou utilizando Node, Express, NextJS e TypeScript, decidi usar como ferramenta de ORM o Prisma, provavelmente a lib mais popular para esse tipo de trabalho em ambiente JavaScript/TypeScript.

Após definir alguns modelos como `User` e `Slot` (uma abstração para os blocos de tempo, facilitando a lógica de negócio dos agendamentos), decidi escrever algumas funções para lidar com registro e login, e percebi algo sobre o que já tinha lido há cerca de dois anos atrás.

No começo do arquivo `login.service.ts`, já fui automaticamente fazendo a importação e instanciando o cliente. Escrevi uma função básica de login e abri outro terminal para navegar até a pasta `routes` e criar a rota que irá receber o request que ativa essa função, sem fechar o arquivo, pois iria continuar trabalhando nele.

Eu tinha separado algumas funções em arquivos diferentes, todas acessando o banco de dados através do `PrismaClient`. Só depois de um tempo percebi que, a cada import, eu acabava criando uma nova instância do Prisma, o que resultava em múltiplas conexões sendo abertas sem necessidade.

E aí me lembrei de algo que havia lido há cerca de dois anos atrás: o padrão Singleton. Singleton é um padrão de projeto que tem um objetivo simples e claro: garantir que uma classe tenha apenas uma instância durante toda a execução da aplicação e fornecer um ponto global de acesso a essa instância.

Em vez de importar o Prisma diretamente de `@prisma/client` e criar uma instância em vários arquivos, criei um arquivo na pasta `prisma` chamado `prisma.ts` com o código centralizado.
O arquivo prisma.ts:
```
import { PrismaClient } from '@prisma/client';

const prisma = new PrismaClient();

export default prisma;
```
Essas 3 linhas de código já garantem um comportamento Singleton. Por causa do sistema de módulos do Node.js, ele é carregado apenas uma vez; o objeto (no caso, o cliente do Prisma) fica em cache e, toda vez que eu precisar utilizar o Prisma Client, importo esse módulo em qualquer lugar do meu backend. Não importa quantos imports, sempre será o mesmo Prisma Client.

A partir disso, nunca mais instancio o Prisma diretamente; sempre que preciso acessar o banco, vou acessar através dessa única instância.

Por exemplo, se preciso utilizar uma query para verificar o login de um usuário dentro do meu `authService.ts` na pasta services, faço a importação diretamente desse arquivo:
```
import prisma from 'caminho/do/arquivo/prisma/prisma' 

export const loginUser = async (email: string) => { 
    const user = await prisma.user.findUnique({
        where: { email: email } }) 
    return user
}
```
**Detalhe importante**: em ambiente de **desenvolvimento**, o Next.js limpa o cache do Node a cada mudança de arquivo (_Fast Refresh_). Isso faz com que o Singleton "morra" e renasça a cada salvamento, acumulando conexões zumbis. Para solucionar esse problema, podemos utilizar o objeto *global* do Node:
```
import { PrismaClient } from '@prisma/client'; 

const globalForPrisma = global as unknown as { 
	prisma: PrismaClient 
}; 

export const prisma = 
	globalForPrisma.prisma || 
	new PrismaClient({ log: ['query'], 
}); 
	
if (process.env.NODE_ENV !== 'production') { 
	globalForPrisma.prisma = prisma;
} 

export default prisma;
```

#### **Conclusão**: 
Implementar o padrão **Singleton** no uso do Prisma não é apenas uma questão de "organização de código", mas sim de **saúde da infraestrutura**. Em um modelo SaaS, onde a eficiência e o controle de custos são vitais, evitar o desperdício de conexões com o banco de dados é um dos primeiros passos para uma aplicação escalável. Ao centralizar a instância do Prisma, ganhamos: 

1. **Performance:** Menos overhead criando conexões a cada requisição. 
2. **Estabilidade:** Evitamos o erro clássico de "Too many connections". 
3. **Manutenibilidade:** Se precisarmos configurar logs ou middlewares do Prisma no futuro, faremos isso em um único arquivo. Se você está começando um projeto com Next.js e Prisma, recomendo fortemente aplicar essa estrutura desde o primeiro dia. Seu banco de dados (e seu bolso, no caso de instâncias pagas) agradecerão!
---
#### Conteúdos utilizados como fonte:

O incível site Refactoring.guru, link da página sobre o Singleton:
https://refactoring.guru/pt-br/design-patterns/singleton

Docs do Prisma, sobre instanciamento: 
https://www.prisma.io/docs/orm/prisma-client/setup-and-configuration/instantiate-prisma-client
 
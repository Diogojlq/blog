---
title: "Arch, Hyprland, produtividade,..."
date: 2026-01-20T20:00:00-03:00
draft: false
tags: ["linux", "produtividade", "hyprland"]
categories: ["tecnologia"]
---

A melhor decisão que já tomei para minha carreira até então, sem sombra de dúvidas, foi abandonar o Windows como ambiente de desenvolvimento e utilizar LINUX. Como todos (ou quase todos) que fizeram essa transição, passei um período fazendo _distro hopping_ (trocando de distribuição) e testando algumas distros diferentes. Em um período de cerca de um mês, fiz pelo menos 10 formatações para testar ambientes diferentes. Comecei usando Ubuntu no WSL, depois Arch no WSL, depois Ubuntu bare metal, um dia de Mint, uma semana de Manjaro com GNOME, depois Manjaro com KDE Plasma, depois Arch com KDE até chegar a dar atenção a window managers, mais especificamente Hyprland, que foi onde eu fiquei até então e não pretendo mudar.

Logo de cara, dezenas se não centenas de horas foram investidas em aprender os gerenciadores de pacote, os comandos e tudo mais que se torna necessário saber nesse processo: mount e unmount de disco, snapshots, diferenças do yay para o pacman para o apt, enfim, coisas relacionadas ao Linux em si. O Arch já é conhecido por não ser a distro mais amigável para iniciantes, mas eu gosto de mergulhar de cabeça nas coisas e aprender na dor, então foi uma experiência incrível, apesar de cansativa.

Só então pude realmente olhar para o conceito de window manager, e acredito que esse é o maior game changer de todos. Pretendo escrever algo mais específico sobre Linux em outro post; por agora vou focar no window manager, pois é onde vejo o maior ganho de produtividade independente da distro que esteja usando. No Windows, nós temos um desktop environment, ambiente desktop, que é a interface gráfica do sistema operacional, onde nós abrimos arquivos, programas e etc. Um window manager é também uma interface gráfica, porém uma versão super minimalista de um desktop environment.

Nos WM, as janelas podem ser flutuantes ou tiled; eu acredito que o ouro está no modo tiling. Não temos ícones, ou o conceito de área de trabalho no Hyprland, e abrimos os apps através de keybinds. Por exemplo, eu abro meu navegador apertando SUPER + B, abro Spotify apertando SUPER + M, o Gemini, que roda como um webapp, eu abro apertando a combinação SUPER + E, e assim por diante, sendo todas as keybinds completamente configuráveis.

Muito importante mencionar o conceito de workspaces também, que eu, sendo obrigado a usar Windows no trabalho, percebi que também existe no Windows, mas não de forma tão ágil como nos WM. Basicamente, a área de trabalho que a maioria das pessoas está acostumada, dos desktop environments, seria como um workspace, e com uma combinação de teclas, no meu caso uso SUPER + 1, 2, 3 e etc., consigo mudar qual workspace está aberto. Se eu abrir o navegador e o Spotify no workspace 1, e mudar para o 2, o workspace 2 estará vazio, sem nada aberto, como se fosse outro desktop ou outra área de trabalho, mas na mesma sessão do Hyprland (ou algum outro WM). As implicações disso na produtividade vou explorar melhor em outro post.

Falando mais sobre o tiling, imagine que eu abra um terminal em um workspace vazio e ele vai abrir ocupando o espaço todo da tela, quase em fullscreen, igual a um app maximizado em uma área de trabalho comum. Em uma área de trabalho comum, se eu abrir outro aplicativo, como por exemplo o Discord, ele vai abrir por cima do terminal, meio que "cobrindo" a janela do terminal; já no WM, com tiling, o Discord abriria ocupando 50% do espaço da tela em ordenação vertical, fazendo com que o workspace fique dividido entre o terminal e o Discord.

Se abrirmos o Neovim (o melhor editor de código já feito) com a janela do Discord selecionada (para permitir uma navegação via teclado, as janelas têm um estado, ativa ou inativa; a janela ativa sempre é apenas uma, a que está "selecionada"), o Neovim vai dividir o espaço de 50% do workspace com o Discord, e ambos então irão ocupar 25% do workspace, enquanto minha janela de terminal continua ocupando 50%. Se a segunda janela aberta vai dividir o workspace horizontalmente ou verticalmente é algo que podemos configurar, assim como adicionar comportamentos específicos para esse tipo de ação. Não vou me estender sobre isso nesse post.

A transição da navegação baseada em mouse para o uso intensivo do teclado é, acima de tudo, uma questão de ergonomia e longevidade profissional. Para quem passa milhares de horas em frente ao computador, o movimento repetitivo de tirar a mão do teclado para buscar o mouse gera um estresse físico acumulado que pode levar a lesões por esforço repetitivo. Ao centralizar a operação no teclado, eliminamos esse deslocamento desnecessário e mantemos as mãos em uma posição mais natural e estável.

Além do aspecto físico, o ganho real de produtividade acontece quando as keybinds e os comandos deixam de ser uma escolha consciente e se tornam reações automáticas à nossa lógica de pensamento. Quando você não precisa mais "procurar" onde clicar, o fluxo entre a ideia e a execução se torna instantâneo, por exemplo:

No DE GNOME, por exemplo, ao apertar ALT + TAB, as janelas abertas aparecem espalhadas após uma animação *cinematográfica* e aparentemente sem uma ordem específica, e você (sim, **você**) precisa procurar com os olhos, encontrar a janela e mover o mouse até ela, e então clicar, para só então ter o aplicativo desejado aberto na sua tela.

No Hyprland: Já acostumei a abrir o meu editor de código no workspace 1, com um terminal ocupando 25% da tela do lado esquerdo. Então, se quero ir até ele, independente de qual janela ou workspace ou até mesmo algo em fullscreen que eu tenha aberto no momento, simplesmente pressiono (hoje já sem pensar) SUPER + 1; em menos de 1 segundo estou lá.

A NAVEGAÇÃO É DEFINITIVAMENTE ONDE ESTÁ A MAIOR POSSIBILIDADE DE GANHO DE PRODUTIVIDADE/EFICIÊNCIA DURANTE O DESENVOLVIMENTO DE SOFTWARE. Além de que se torna muito prazeroso usar o computador; consequentemente, o desenvolvimento da minha principal habilidade, do meu _craft_, se torna mais prazeroso. E isso vale muito mais que algumas dezenas de horas e dores de cabeça lendo documentação para fazer tudo funcionar.

**Nota técnica:** Webapps são aplicações que rodam no navegador, porém dentro de uma janela que é identificada como um aplicativo, além de isso ser super legal, o mais importante é que isso permite que esses webapps sejam executados com um comando no teclado, uma keybind. Ou seja: se quero perguntar algo ao Gemini, aperto SUPER + E e voilà.

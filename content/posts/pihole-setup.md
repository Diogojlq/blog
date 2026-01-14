+++
title = "Pihole Setup"
date = "2026-01-14T16:14:05-03:00"
#dateFormat = "2006-01-02" # This value can be configured for per-post date formatting
author = ""
authorTwitter = "" #do not include @
cover = ""
tags = ["", ""]
keywords = ["", ""]
description = ""
showFullContent = false
readingTime = false
hideComments = false
+++

O primeiro projeto que executei logo que adquiri meu mini pc foi a implementação do Pihole como servidor DNS da minha rede local.
O Pihole atua como um "sinkhole". Ele intercepta requisiçòes de domínio antes mesmo que elas saiam da rede local. Se um dispositivo tenta carregar um domínio de rastreamento ou publicidade, o servidor retorna um endereço inválido, bloqueando o conteúdo a nível de rede.

Pontos fundamentais do Pihole, e principais motivos que eu decidi implementa-lo:
1. Bloqueio por rede: Diferente de extensões de navegador, o bloqeuio acontece para todos os dispositivos conectados na rede, seja uma Smart TV ou um dispositivos IoT, que nativamente não permitem ad-blockers.
2. Docker e Infraestrutura: O serviço (Pihole) roda em um container Docker, o que permite monitoramento em tempo real do tráfego e métricas de bloqueio através de um dashboard administrativo (anexei uma foto do painel da interface administrativa do Pihole na postagem).

A principal vantagem técnica aqui não é apenas a ausência de anúncios, mas a economia de largura de banda e a melhoria na privacidade de todos os dispositivos. Quando o navegador deixa de carregar scripts de telemetria e rastreadores pesados, a navegação se torna visivelmente mais rápida.

Projetos como este reforçam a importância de entender protocolos de rede (como UDP/53) e como pequenas otimizações de infraestrutura podem melhorar drasticamente a segurança e a experiência do usuário final.

# RF2 Server Manager

[English](README.md) · [Italiano](README.it.md) · [Español](README.es.md) · [Français](README.fr.md) · [Deutsch](README.de.md) · **Português**

**Download:** [última versão](https://github.com/KarmaTV80/rf2-server-manager/releases/latest)

---

Ferramenta para Windows que configura e inicia um servidor dedicado de RF2.
Não é um produto oficial e não tem ligação com a Studio 397 nem com a Motorsport Games.

Na primeira execução o app reconhece o idioma do Windows: italiano, inglês, espanhol, francês, alemão ou português. Os outros idiomas passam a inglês. O botão com a bandeira no canto superior direito o muda, e o app lembra a sua escolha.

## Requisitos

- Windows 10 ou 11 de 64 bits. O .NET já está incluído no exe.
- Espaço em disco para o servidor e os conteúdos.
- Microsoft Edge WebView2 Runtime, só para o navegador da aba Workshop. Sem ele, você pode colar o ID do Workshop à mão.

O servidor dedicado e o SteamCMD não estão incluídos: o app pode baixá-los da Valve e da Steam com a configuração guiada.

## Primeira execução

1. Abra `RF2ServerManager.exe`. Não é preciso instalar.
2. Se o Windows mostrar "O Windows protegeu o computador", escolha **Mais informações** e depois **Executar assim mesmo**. Aparece porque o exe não tem assinatura digital.
3. Na configuração guiada escolha as pastas do SteamCMD e do servidor, ou deixe o app baixá-los.
4. Inicie o servidor uma vez: ele cria os arquivos de configuração. Se o Windows pedir permissão para o firewall, escolha **Permitir**.

## Atualizações

Ao iniciar, o app verifica no GitHub se há uma versão nova. Se houver, no fim do menu à esquerda aparece o quadro **Atualizar agora**. O app a baixa, verifica a impressão SHA-256 e reabre sozinho; o servidor, se estiver ligado, continua ligado. Abaixo do número da versão, **Verificar atualizações** repete a verificação à mão. Se não for possível escrever na pasta do app (por exemplo dentro de Arquivos de Programas), baixe a versão nova na [página de versões](https://github.com/KarmaTV80/rf2-server-manager/releases).

## Conteúdos que você já tem no jogo

Não é preciso baixá-los de novo nem copiá-los à mão. O app encontra sozinho a pasta do jogo, que você também pode escolher no passo 1. Preparar. No passo 3. Conteúdo clique em **Adicionar do jogo**, selecione carros e pistas e clique em **Copiar para o servidor**. O jogo é apenas lido.

Na **Biblioteca** cada conteúdo mostra seu estado: *Pronto*, *A instalar* ou *Falta o pacote*, quando os amigos não podem baixá-lo. O botão da linha faz a coisa certa: instala, copia o pacote do jogo ou abre o Workshop na busca daquele conteúdo. Os carros e as pistas do evento são escolhidos no passo 4. Evento, com **Criar um novo evento**.

Os conteúdos instalados no jogo sem pacote `.rfcmp` (por exemplo comprados num site) aparecem no fim das listas: deles é copiada para o servidor a instalação, e só poderão entrar os pilotos que já os têm, na mesma versão.

Os DLCs oficiais comprados funcionam no servidor: o app copia sozinho o arquivo de desbloqueio que o jogo prepara (`ServerUnlock.bin`). As atualizações dos conteúdos também são aplicadas sozinhas.

## Jogar com outras pessoas

No roteador, redirecione para o IP do PC:

| Porta | Protocolo | Uso |
|---|---|---|
| 54297 | TCP e UDP | Simulação |
| 64297 | TCP | Download dos arquivos pelos clientes |
| 64298 e 64299 | UDP | Steam: sem elas o servidor não aparece na lista do jogo |

**Nunca abra as portas 5397 e 5398**: elas controlam o servidor e o jogo. Defina sempre uma senha de entrada e uma senha de admin diferentes entre si. O botão **Verificar rede e portas** no passo 10. Servidor ajuda você a verificar.

## Antitrapaça

No passo 9. Chat e ping o app pode sinalizar pilotos com voltas ou velocidades impossíveis e saltos de um ponto a outro da pista, comparando cada um com os outros da mesma classe. Não desconecta ninguém: avisa e escreve tudo no registro de suspeitos (`sospetti.log`), e depois quem administra o servidor decide. O servidor não vê dentro do PC dos pilotos, por isso encontra os efeitos das trapaças, não os programas.

## Onde ficam os dados

- Configurações e registro: `%AppData%\RF2ServerManager`
- Senhas: só nos arquivos de configuração do servidor, que as guarda em texto simples. Não vão para os perfis.

Se algo der errado, envie o registro da pasta `logs`. O botão **Abrir pasta de registros** está no passo 1. Preparar.

## Limites conhecidos

- A criação de mods e a instalação de pacotes comandam o MAS2 e o ModMgr em segundo plano, com as janelas ocultas: o progresso aparece no registro do app. Com "Iniciar a sessão imediatamente" a janela do servidor também abre minimizada: reabra-a pela barra de tarefas do Windows. Uma atualização dessas ferramentas pode exigir adaptar o app.
- Conteúdos pagos e pacotes copiados do Workshop podem não instalar: o app mostra o erro e limpa os arquivos.
- Treino 2 não tem horário nem duração próprios na configuração do servidor.

## Condições de uso

Gratuito, inclusive para campeonatos e ligas. Não é permitido modificá-lo, descompilá-lo, revendê-lo ou distribuí-lo a partir de outros sites: compartilhe só o link oficial. Texto completo em `LICENSE.txt` e na janela **Sobre** do app.

Componentes de terceiros: FlaUI e Newtonsoft.Json (licença MIT), Microsoft WebView2 SDK (licença Microsoft), .NET (licença MIT), fontes Saira Extra Condensed e Barlow (SIL Open Font License, textos em `Licenze\`).

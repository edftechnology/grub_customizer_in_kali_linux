# Como instalar/configurar/usar o `GRUB Customizer` no `Linux Ubuntu`

## Resumo

Neste documento estão contidos os principais comandos e configurações para instalar/configurar/usar o `GRUB Customizer` no `Linux Ubuntu`.

## _Abstract_

_This document contains the main commands and settings to install/configure/usar the GRUB Customizer on Linux Ubuntu._

## Revisão(ões)/Versão(ões)

|Revisão número|Data da revisão|Descrição da revisão|Autor da revisão|
|:-:|:-:|:-|:-|
|0|31/10/2023|<ul><li>Revisão inicial/criação do documento.</li></ul>|Eden Denis F. da S. L. Santos|
|1|14/11/2023|<ul><li>Incluída a Seção Descrição.</li></ul>|Eden Denis F. da S. L. Santos|

## Controle de configuração/instalação nos Sistemas Operacionais (SO) vs. Computador

|Numero|Computador         |Sistema Operacional (SO)|Status da configuração/instalação|
|:----:|:-----------------:|:----------------------:|:-------------------------------:|
|1     |Dell Precision 7520|Kali   Linux            |Pendente                         |
|2     |Dell Precision 7520|Linux Ubuntu            |N/A                              |
|3     |Dell Precision 7520|Linux Xubuntu           |OK                               |
|4     |Dell Precision 7520|Windows                 |Pendente                         |
|5     |Asus               |Kali   Linux            |N/A                              |
|6     |Asus               |Linux Ubuntu            |Pendente                         |
|7     |Asus               |Linux Xubuntu           |Pendente                         |
|8     |Asus               |Windows                 |Pendente                         |


## Descrição

### `GRUB Customizer`

O `Grub Customizer` é uma ferramenta gráfica que permite aos usuários do Ubuntu e outras distribuições Linux personalizar o menu de inicialização do GRUB2 (GRand Unified Bootloader versão 2). Com esta aplicação, você pode facilmente adicionar, remover, reordenar e editar as entradas do menu de inicialização sem ter que manipular manualmente arquivos de configuração complexos. A ferramenta também oferece opções para alterar a aparência do menu GRUB, como cores e resolução, e permite fazer ajustes avançados, como modificar parâmetros do kernel. É uma maneira mais amigável e acessível de gerenciar as opções de inicialização do sistema.


## 1. Configurar/Instalar/Usar o `GRUB Customizer` do `Linux Ubuntu` [1][2]

### 1.1 Atualizar o Sistema Operacional (SO)

1. Abra o terminal. Você pode fazer isso pressionando: `Ctrl + Alt + T`

2. Certifique-se de que seu sistema esteja limpo e atualizado.

    2.1 Limpar o `cache` do gerenciador de pacotes APT. Especificamente, ele remove todos os arquivos de pacotes (`.deb`) baixados pelo APT e armazenados em `/var/cache/apt/archives/`. Digite o seguinte comando: `sudo apt clean` 
    
    2.2 Remover pacotes `.deb` antigos ou duplicados do cache local. É útil para liberar espaço, pois remove apenas os pacotes que não podem mais ser baixados (ou seja, versões antigas de pacotes que foram atualizados). Digite o seguinte comando: `sudo apt autoclean`

    2.3 Remover pacotes que foram automaticamente instalados para satisfazer as dependências de outros pacotes e que não são mais necessários. Digite o seguinte comando: `sudo apt autoremove -y`

    2.4 Buscar as atualizações disponíveis para os pacotes que estão instalados em seu sistema. Digite o seguinte comando e pressione `Enter`: `sudo apt update -y`

    2.5 Para ver a lista de pacotes a serem atualizados, digite o seguinte comando e pressione `Enter`:  `sudo apt list --upgradable`

    2.6 Realmente atualizar os pacotes instalados para as suas versões mais recentes, com base na última vez que você executou `sudo apt update -y`. Digite o seguinte comando e pressione `Enter`: `sudo apt full-upgrade -y`

    2.7 Remover pacotes que foram automaticamente instalados para satisfazer as dependências de outros pacotes e que não são mais necessários. Digite o seguinte comando: `sudo apt autoremove -y`

    2.8 Remover pacotes `.deb` antigos ou duplicados do cache local. É útil para liberar espaço, pois remove apenas os pacotes que não podem mais ser baixados (ou seja, versões antigas de pacotes que foram atualizados). Digite o seguinte comando: `sudo apt autoclean`

No Kali Linux, a instalação do Grub Customizer pode ser um pouco diferente da de outras distribuições baseadas no Debian, devido à sua natureza especializada e ao conjunto padrão de repositórios. Aqui estão as etapas para instalar o Grub Customizer no Kali Linux:

3. **Instale o Grub Customizer:** `sudo apt install grub-customizer -y`

Após a instalação, você pode abrir o `Grub Customizer` através do menu de aplicativos ou executando `grub-customizer` no Terminal.


### 1.1 Código completo para configurar/instalar/usar

Para configurar/instalar/usar o `GRUB Customizer` no `Linux Ubuntu` sem precisar digitar linha por linha, você pode seguir estas etapas:

1. Abra o terminal. Você pode fazer isso pressionando: `Ctrl + Alt + T`

2. Digite o seguinte comando e pressione `Enter`:

    ```
    sudo apt clean
    sudo apt autoclean
    sudo apt autoremove
    sudo apt update -y
    sudo apt autoremove
    sudo apt autoclean
    sudo apt list --upgradable
    sudo apt full-upgrade -y
    sudo apt install grub-customizer -y
    ```


## Referências

[1] OPENAI. ***Customização do grub no ubuntu.*** Disponível em: <https://chat.openai.com/c/9d00a24c-142f-46fc-965f-97504fc33492> (texto adaptado). ChatGPT. Acessado em: 31/10/2023 15:28.

[2] JAMES, J.. ***How to install grub customizer on ubuntu 22.04 or 20.04.*** Disponível em: <https://www.linuxcapable.com/how-to-install-grub-customizer-on-ubuntu-linux/>. ChatGPT. Acessado em: 31/10/2023 15:29.


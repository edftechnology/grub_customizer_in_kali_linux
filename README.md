# Como instalar/configurar/usar o `GRUB Customizer` no `Kali Ubuntu`

## Resumo

Neste documento estão contidos os principais comandos e configurações para instalar/configurar/usar o `GRUB Customizer` no `Kali Ubuntu`.

## _Abstract_

_This document contains the main commands and settings to install/configure/usar the GRUB Customizer on `Kali Ubuntu`._

## Descrição

### `GRUB Customizer`

O `Grub Customizer` é uma ferramenta gráfica que permite aos usuários do `Linux Ubuntu` e outras distribuições `Linux` personalizar o menu de inicialização do `GRUB2` (GRand Unified Bootloader versão 2). Com esta aplicação, você pode facilmente adicionar, remover, reordenar e editar as entradas do menu de inicialização sem ter que manipular manualmente arquivos de configuração complexos. A ferramenta também oferece opções para alterar a aparência do menu `GRUB`, como cores e resolução, e permite fazer ajustes avançados, como modificar parâmetros do kernel. É uma maneira mais amigável e acessível de gerenciar as opções de inicialização do sistema.


## 1. Configurar/Instalar/Usar o `GRUB Customizer` do `Kali Ubuntu` [1][2]

**ATENÇÂO**: Tenha em mente que o `GRUB` deve ser instalado no primário da sequência de `boot`, logo, se ele for instalado em outro disco, este, por sua vez, deve ser alterado para ser o primeiro disco na inicialização do computador.

### 1.1 Atualizar o Sistema Operacional (SO)

1. Abra o terminal. Você pode fazer isso pressionando:

    ```bash
    Ctrl + Alt + T
    ```

2. Certifique-se de que seu sistema esteja limpo e atualizado.

    2.1 Limpar o `cache` do gerenciador de pacotes `apt`. Especificamente, ele remove todos os arquivos de pacotes (`.deb`) baixados pelo `apt` e armazenados em `/var/cache/apt/archives/`. Digite o seguinte comando:
    ```bash
    sudo apt clean
    ```

    2.2 Remover pacotes `.deb` antigos ou duplicados do `cache` local. É útil para liberar espaço, pois remove apenas os pacotes que não podem mais ser baixados (ou seja, versões antigas de pacotes que foram atualizados). Digite o seguinte comando:
    ```bash
    sudo apt autoclean
    ```

    2.3 Remover pacotes que foram automaticamente instalados para satisfazer as dependências de outros pacotes e que não são mais necessários. Digite o seguinte comando:
    ```bash
    sudo apt autoremove -y
    ```

    2.4 Buscar as atualizações disponíveis para os pacotes que estão instalados em seu sistema. Digite o seguinte comando e pressione `Enter`:
    ```bash
    sudo apt update
    ```

    2.5 **Corrigir pacotes quebrados**: Isso atualizará a lista de pacotes disponíveis e tentará corrigir pacotes quebrados ou com dependências ausentes:
    ```bash
    sudo apt --fix-broken install
    ```

    2.6 Limpar o `cache` do gerenciador de pacotes `apt` novamente:
    ```bash
    sudo apt clean
    ```

    2.7 Para ver a lista de pacotes a serem atualizados, digite o seguinte comando e pressione `Enter`:
    ```bash
    sudo apt list --upgradable
    ```

    2.8 Realmente atualizar os pacotes instalados para as suas versões mais recentes, com base na última vez que você executou `sudo apt update`. Digite o seguinte comando e pressione `Enter`:
    ```bash
    sudo 

3. **Instale o `Grub Customizer`:**

    ```bash
    sudo apt install -y grub-customizer
    ```

4. **Abra o `Grub Customizer` (como root):**

    ```bash
    sudo grub-customizer
    ```

5. **Alternativa mais segura (terminal puro):** Se preferir evitar mudanças pelo aplicativo gráfico em ambientes híbridos (UEFI + Legacy), edite manualmente:

    ```bash
    sudo nano /etc/default/grub
    sudo update-grub
    ```

### 1.2 Avisos importantes (LEIA com atenção)

1. **Em dual-boot com UEFI/Legacy misto (ex.: Ubuntu em UEFI + Kali em Legacy/BIOS):**

    - **Não use** o `grub-customizer` para reinstalar o GRUB ou trocar o modo (UEFI ↔ Legacy).
    - **Não clique** em “Instalar no MBR” ou “Reinstalar GRUB”.
    - Use apenas para: reordenar/renomear entradas, ocultar entradas, ajustar `timeout` e definir entrada padrão.

2. **Backup recomendado antes de salvar alterações:**

    ```bash
    sudo cp -a /etc/default/grub /etc/default/grub.bak
    sudo cp -a /boot/grub /boot/grub.bak
    ```


### 1.3 Código completo para configurar/instalar/usar

Para configurar/instalar/usar o `GRUB Customizer` no `Kali Ubuntu` sem precisar digitar linha por linha, você pode seguir estas etapas:

1. Abra o `Terminal Emulator`. Você pode fazer isso pressionando:

    ```bash
    Ctrl + Alt + T
    ```

2. Digite o seguinte comando e pressione `Enter`:

    ```bash
    sudo apt clean
    sudo apt autoclean
    sudo apt autoremove -y
    sudo apt update
    sudo apt --fix-broken install
    sudo apt list --upgradable
    sudo apt full-upgrade -y
    sudo apt install -y grub-customizer
    sudo cp -a /etc/default/grub /etc/default/grub.bak
    sudo cp -a /boot/grub /boot/grub.bak
    sudo grub-customizer
    ```


## 2. Consultar a versão do `Kali Linux`

1. **Método padrão (recomendado):**

    ```bash
    cat /etc/os-release
    ```

2. **Usando `lsb_release` (se instalado):**

    ```bash
    lsb_release -a
    ```

    Se o comando não existir:

    ```bash
    sudo apt install -y lsb-release
    ```

3. **Comando específico do Kali:**

    ```bash
    kali-version
    ```

4. **Versão do kernel (útil para compatibilidade):**

    ```bash
    uname -r
    ```


## 3. Decisão de boot e arquitetura do `GRUB` (documentação de referência)

Esta seção concentra decisões de arquitetura de boot (evidências, justificativas e procedimentos). Ela **não** descreve o particionamento em si; isso fica em documentação específica de layout de disco.

### 3.1 Decisão de boot: `MBR` + `Legacy BIOS`

Este sistema utiliza `MBR` + `Legacy BIOS` em vez de `GPT` + `UEFI` pelos seguintes motivos:

- Compatibilidade total com _hardware_ Dell antigo.
- Dual-boot mais estável entre `Ubuntu` e `Kali`.
- Evita conflitos entre múltiplos `GRUBs` em `EFI`.
- Recuperação simples via `Live USB`.

### 3.2 Evidências técnicas (conforme capturas)

Registre aqui as evidências observadas nas fotos/logs:

- `/sys/firmware/efi` inexistente (indica `Legacy BIOS`).
- Saída do `grub-install` usando `Installing for i386-pc platform`.
- `GRUB` instalado no `MBR` do disco `/dev/nvme0n1`.

### 3.3 Controle do GRUB em dual-boot

- O `GRUB` ativo deve ser o do `Ubuntu`.
- Quando o `GRUB` do `Kali` assume, há falhas de boot (loop/splash travado).
- Estratégia adotada:
  - `GRUB` centralizado no `Kali`.
  - `Kali` como entrada secundária no menu.

### 3.4 Layout de boot funcional (resumo)

- `/dev/nvme0n1p5` → `/boot` (`Ubuntu`).
- `/dev/nvme0n1p6` → `/` (`Ubuntu`).
- `/dev/nvme0n1p7` → `/` (`Kali`).
- `GRUB` instalado no `MBR` (`/dev/nvme0n1`).

### 3.5 Problemas encontrados e causa raiz

- Boot do `Kali` travava no splash.
- Entradas manuais do `GRUB` falharam.

Causas prováveis:

- Instalação do `Kali` sem `/boot` dedicado.
- `GRUB` do `Kali` tentando assumir controle do boot.
- Firmware `Legacy` incompatível com abordagem `UEFI` neste hardware.

### 3.6 Recuperação do GRUB (`Legacy`)

1. Boot via `Live USB` do `Ubuntu`.
2. Montar sistema:

    ```bash
    sudo mount /dev/nvme0n1p6 /mnt
    sudo mount /dev/nvme0n1p5 /mnt/boot
    ```

3. Entrar no `chroot` e reinstalar:

    ```bash
    sudo chroot /mnt
    grub-install /dev/nvme0n1
    update-grub
    exit
    ```


## 4. GRUB no Kali: configuracao, layout e operacao (Legacy BIOS / MBR)

Este documento descreve como configurar o `GRUB` do `Kali Linux` para atuar
como bootloader principal do sistema, bem como reproduzir o layout classico
(tema azul padrao), conforme exibido durante o boot.

### 4.1 Contexto do ambiente

- Sistema principal de boot: `Kali Linux`.
- Metodo de boot: `Legacy BIOS` + `MBR`.
- Disco: `/dev/nvme0n1`.
- `GRUB` instalado como: `i386-pc`.
- Sistemas detectados:
  - `Kali GNU/Linux`.
  - `Ubuntu 22.04 LTS`.
  - `Windows 10`.

### 4.2 Modo de boot detectado

- Firmware: `Legacy BIOS` (nao `UEFI`).
- Evidencias:
  - `/sys/firmware/efi` inexistente.
  - `GRUB` instalado como `i386-pc`.
  - Boot realizado via `MBR` do disco `/dev/nvme0n1`.

> Observacao: em sistemas `Legacy`, nao existe particao `EFI`. Todo o controle
> de boot ocorre via `MBR` e arquivos em `/boot/grub`.

### 4.3 Tornando o GRUB do Kali o bootloader principal

Isto garante que:

- O `GRUB` do `Kali` sobrescreva o `MBR`.
- O menu exibido ao ligar a maquina seja o do `Kali`.
- Outros sistemas sejam apenas entradas no menu.

Caso seja necessario reinstalar manualmente:

```bash
sudo grub-install /dev/nvme0n1
sudo update-grub
```

### 4.4 Layout classico do GRUB (tema azul)

O layout exibido (fundo azul, fonte branca, sem imagem) corresponde
ao tema padrao do `GRUB`, sem custom themes.

Para garantir esse layout:

Arquivo principal:

- `/etc/default/grub`

Configuracao recomendada:

- `GRUB_TIMEOUT=10`
- `GRUB_TIMEOUT_STYLE=menu`
- `GRUB_DEFAULT=0`
- `GRUB_GFXMODE=text`
- `GRUB_TERMINAL=console`

Importante: nao definir `GRUB_THEME` garante que o `GRUB` utilize
o layout classico padrao.

Apos qualquer alteracao:

```bash
sudo update-grub
```

### 4.5 Geracao automatica das entradas

O `Kali` detecta automaticamente outros sistemas via `os-prober`
(quando habilitado):

- `Ubuntu`.
- `Windows`.
- Outras instalacoes `Linux`.

As entradas sao geradas em:

- `/boot/grub/grub.cfg`

Nao edite esse arquivo manualmente.

### 4.6 Entradas customizadas (opcional)

Entradas adicionais podem ser definidas em:

- `/etc/grub.d/40_custom`

Exemplo:

```bash
menuentry "Sistema personalizado" {
    set root=(hd0,msdos7)
    linux /boot/vmlinuz root=/dev/nvme0n1p7 ro
    initrd /boot/initrd.img
}
```

Sempre regenerar o `GRUB` apos alteracoes:

```bash
sudo update-grub
```

### 4.7 Observacoes importantes

- Em sistemas `Legacy`, misturar `UEFI` e `BIOS` gera falhas de boot.
- Apenas um `GRUB` deve controlar o `MBR`.
- O `GRUB` do `Kali` mostrou-se mais estavel neste ambiente.
- Reboots podem resolver travamentos iniciais causados por
  inicializacao de drivers (`GPU`, `ACPI`, `initramfs`).

### 4.8 Resultado final esperado

- `GRUB` do `Kali` exibido ao ligar a maquina.
- Layout azul classico.
- Entradas para `Kali`, `Ubuntu` e `Windows`.
- Boot funcional sem dependencia do `GRUB` do `Ubuntu`.

### 4.9 Referencias

- `man grub-install`
- `man update-grub`
- <https://www.gnu.org/software/grub/>
- <https://www.kali.org/docs/troubleshooting/grub-recovery/>


## Referências

[1] OPENAI. ***Instalar o `grub customizer` no `kali ubuntu` pelo `terminal emulator`.*** Disponível em: <https://chatgpt.com/g/g-p-6980caf949648191ad6acfcdbe590f9e-instalar/c/6982bd52-ac78-8325-8330-86637d06c77f> (texto adaptado). ChatGPT. Acessado em: 05/02/2026.

[2] OPENAI. ***Como consultar a versão do `Kali Linux`.*** Disponível em: <https://chatgpt.com/g/g-p-6980caf949648191ad6acfcdbe590f9e-instalar/c/6982bd52-ac78-8325-8330-86637d06c77f> (texto adaptado). ChatGPT. Acessado em: 05/02/2026.


<div align="center">


# 🔒 BlockSecure

**Sistema de bloqueio e kiosk mode para terminais médicos e industriais**

[![Versão](https://img.shields.io/badge/versão-1.0.0-gold?style=for-the-badge)](https://github.com/VictorJesus26/PRODUCAO_BLOCKSECURE/releases)
[![Plataforma](https://img.shields.io/badge/plataforma-Windows-0078d4?style=for-the-badge&logo=windows)](https://www.microsoft.com/windows)
[![Linguagem](https://img.shields.io/badge/linguagem-C%23%20%2F%20.NET-512BD4?style=for-the-badge&logo=dotnet)](https://dotnet.microsoft.com/)
[![Licença](https://img.shields.io/badge/licença-Privada-red?style=for-the-badge)](LICENSE)

---

*Desenvolvido por Victor Jesus para garantir a integridade e segurança de terminais de visualização médica.*

</div>

---

## 📋 Sobre o Projeto

O **BlockSecure** é uma solução corporativa de **kiosk mode** e **bloqueio de sistema**. Ele garante que terminais Windows utilizados em ambientes hospitalares e industriais operem de forma segura, restrita e controlada, impedindo o acesso não autorizado a funções do sistema operacional.

### 🎯 Casos de Uso

- 🏥 **Terminais de Visualização Médica** — Estações de trabalho DICOM e sistemas de imagem
- 🏭 **Terminais Industriais** — Painéis de controle e visualização em chão de fábrica
- 🖥️ **Quiosques Corporativos** — Estações de trabalho dedicadas a uma única aplicação

---

## ✨ Funcionalidades

| Funcionalidade | Descrição |
|---|---|
| 🔐 **Kiosk Mode** | Bloqueia o terminal para operar apenas a aplicação designada |
| ⌨️ **Bloqueio de Atalhos** | Desabilita combinações como `Win+D`, `Alt+Tab`, `Ctrl+Alt+Del` |
| 🚫 **Bloqueio de USB** | Impede o uso de dispositivos de armazenamento externos |
| 📋 **Bloqueio do Gerenciador de Tarefas** | Previne o fechamento ou alteração de processos críticos |
| 🖥️ **Bloqueio de Ícones da Área de Trabalho** | Mantém o ambiente de trabalho limpo e controlado |
| 👁️ **Monitoramento de Processos** | Monitora processos críticos e restaura o ambiente automaticamente |
| 🔄 **Inicialização Automática** | Configurável para iniciar automaticamente com o Windows via Task Scheduler |
| 📊 **Log de Auditoria** | Registra todas as tentativas de acesso, bloqueios e alterações em `activity_log.xml` |
| 🔑 **Painel Administrativo** | Acesso protegido por senha para configuração e manutenção |

---

## 📁 Estrutura do Pacote de Implantação

```
PRODUCAO_BLOCKSECURE/
│
├── 🖼️  logo.png                    # Logomarca exibida na interface
├── 📄  config.template.xml         # Modelo de configuração (renomear para config.xml)
│
├── 🚀  INICIAR_SOFTWARE.bat        # Inicia o software com privilégios de Admin
├── 🔧  CONFIGURAR_INICIALIZACAO.bat # Configura a inicialização automática no boot
│
└── 📖  LEIA-ME.txt                 # Instruções de instalação (formato texto)
```

> **📦 O executável `BlockSecure.exe` é distribuído via [Releases](../../releases) do GitHub.**
> Faça o download da versão mais recente na aba **Releases** e coloque o `.exe` na mesma pasta dos arquivos acima.

---

## 🚀 Instalação e Implantação

### Pré-requisitos

- **Windows 10** ou superior (64-bit)
- **Privilégios de Administrador** para instalação e configuração
- **.NET Runtime** compatível com a versão compilada

### Passos de Instalação

**1. Baixar o executável**
```
Acesse a aba "Releases" do repositório e baixe o BlockSecure.exe da versão mais recente.
```

**2. Montar o pacote no terminal**
```
Crie uma pasta segura no terminal (ex: C:\BlockSecure\) e coloque todos os arquivos nela:
  - BlockSecure.exe  (baixado em Releases)
  - logo.png
  - INICIAR_SOFTWARE.bat
  - CONFIGURAR_INICIALIZACAO.bat
  - config.template.xml  → renomear para config.xml
```

**3. Configurar o arquivo `config.xml`**

Edite o arquivo `config.xml` (ou renomeie `config.template.xml` para `config.xml`) com os dados do terminal:

```xml
<?xml version="1.0" encoding="utf-8"?>
<AppSettings>
  <SerialNumber>SN-000000</SerialNumber>   <!-- Número de série do equipamento -->
  <Customer>Nome do Hospital / Cliente</Customer>
  <KioskMode>true</KioskMode>              <!-- true = bloqueios ativos -->
  <RunOnStartup>true</RunOnStartup>
  <AdminPassword>suporte123</AdminPassword> <!-- Senha do painel administrativo -->

  <!-- Processos a monitorar (separados por vírgula) -->
  <WatchedProcesses>DROC</WatchedProcesses>
  <AutoRestoreOnProcessExit>true</AutoRestoreOnProcessExit>

  <Shortcuts>
    <string>Win+D</string>
    <string>Alt+Tab</string>
    <string>Ctrl+Alt+Del</string>
  </Shortcuts>

  <Blocks>
    <string>USB Storage</string>
    <string>Task Manager</string>
    <string>Desktop Icons</string>
  </Blocks>
</AppSettings>
```

**3. Configurar inicialização automática** *(Recomendado)*
```
Execute como Administrador: CONFIGURAR_INICIALIZACAO.bat
```
Isso criará uma **Tarefa Agendada** no Windows para iniciar o BlockSecure automaticamente a cada logon, com privilégios elevados.

**4. Testar a inicialização manual**
```
Execute: INICIAR_SOFTWARE.bat
```

---

## 🔑 Acesso Administrativo

Para acessar o painel de administração e realizar configurações ou manutenção:

| Método | Instrução |
|---|---|
| **Senha Padrão** | Definida no arquivo `config.xml` (Padrão: `suporte123`) |
| **Atalho de Recuperação** | `CTRL` + `SHIFT` + `ALT` + `S` |

> ⚠️ **Importante:** Recomenda-se alterar a senha padrão após a primeira configuração em produção.

---

## 📊 Log de Auditoria

O arquivo `activity_log.xml` registra automaticamente:

- ✅ Inicializações e encerramentos do software
- 🚫 Tentativas de uso de atalhos bloqueados
- 🔌 Tentativas de conexão de dispositivos USB
- 🔑 Acessos ao painel administrativo
- ⚙️ Alterações de configuração

---

## ⚙️ Referência de Configuração (`config.xml`)

| Parâmetro | Tipo | Descrição |
|---|---|---|
| `SerialNumber` | String | Identificador único do equipamento/terminal |
| `Customer` | String | Nome do cliente ou unidade hospitalar |
| `KioskMode` | Boolean | `true` ativa todos os bloqueios; `false` desabilita |
| `RunOnStartup` | Boolean | Controla a inicialização automática com Windows |
| `AdminPassword` | String | Definição da senha para acessar o painel administrativo |
| `WatchedProcesses` | String | Processos monitorados (ex: `DROC`) |
| `AutoRestoreOnProcessExit` | Boolean | Restaura o ambiente quando o processo monitorado encerra |
| `Shortcuts` | Lista | Combinações de teclas a serem bloqueadas |
| `Blocks` | Lista | Recursos do sistema a serem bloqueados |

### Valores Disponíveis para `Blocks`

| Valor | Efeito |
|---|---|
| `USB Storage` | Bloqueia dispositivos de armazenamento USB |
| `Task Manager` | Impede abertura do Gerenciador de Tarefas |
| `Desktop Icons` | Oculta/bloqueia ícones da área de trabalho |

---

## 🛠️ Suporte Técnico

Para suporte, dúvidas ou solicitações de personalização:

<div align="center">



</div>

---

## 📝 Changelog

### v1.0.0 — Lançamento Inicial
- ✅ Kiosk Mode funcional com bloqueio de atalhos do sistema
- ✅ Bloqueio de USB Storage, Task Manager e Desktop Icons
- ✅ Monitoramento de processo com restauração automática
- ✅ Log de auditoria em XML (`activity_log.xml`)
- ✅ Painel administrativo com senha de acesso
- ✅ Configuração via `config.xml`
- ✅ Scripts de implantação (`.bat`) para instalação simplificada
- ✅ Inicialização automática via Windows Task Scheduler

---

<div align="center">

**Desenvolvido por Victor Jesus

*2026 Victor Jesus. Todos os direitos reservados.*

</div>

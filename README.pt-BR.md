# 🪐 NTC IDE PRO: O Ambiente de Desenvolvimento Hiper-Isolado

[🇺🇸 Read in English](README.md)

![NTC IDE PRO Preview](preview.png)

Uma distribuição do VS Code avançada, isolada e baseada em perfis customizados, projetada para operar com zero dependências globais de sistema. Otimizado para desenvolvimento em alto ritmo, engenharia de prompts customizada e sincronização profunda com o terminal.

Desenvolvido por **Leandro Paixão** (SaaS & Cloud Architect).

---

## 🌌 O Conceito: Por que Isolamento de Perfil?

Instalações padrão do VS Code compartilham extensões, caches de workspace e configurações globalmente em todo o seu computador. Quando você trabalha com múltiplos clientes ou experimenta com diversos fluxos de LLM, um ambiente global se torna inchado, lento e propenso a conflitos de extensões.

O **NTC IDE PRO** resolve isso alavancando um perfil de execução em sandbox utilizando diretórios de dados de usuário customizados (`--user-data-dir`). Ele opera completamente separado da sua instalação diária do VS Code, trazendo:
*   **Extensões Isoladas:** Execute apenas extensões de codificação de elite sem inchar seu setup principal.
*   **Cockpit Embutido:** Inicia nativamente com o **NTC Shell** (PowerShell 7 + Oh My Posh) rodando no dock do terminal.
*   **Configurações Limpas:** Estética estrita, tipografia de desenvolvedor customizada e layouts de janela limpos otimizados para trabalho focado (deep work).

---

## ⚡ Arquitetura de Execução (O Launcher)

Em vez de depender de clones pesados de aplicativos, o **NTC IDE PRO** usa uma função de bootstrap de shell de alta performance. Quando você roda `ntc-ide` (ou usa o atalho `n1` no NTC Shell), o terminal aciona um perfil dedicado apontando para um mapa de diretórios isolado:

```powershell
function global:ntc-ide {
    param([string]$folderPath = ".")
    $profileDir = "$HOME\Documents\ntc-ide-pro\IDE\profile-data"
    Start-Process "code" -ArgumentList "$folderPath --user-data-dir `"$profileDir`"" -NoNewWindow
}
```

---

## 🛠️ Instalação & Setup

### 1. Requisitos

- VS Code instalado no seu sistema.
- A fonte Nerd Font **MesloLGS NF** instalada para suporte aos ícones do terminal.

### 2. Deploy

Para clonar e registrar o perfil isolado no seu sistema, rode:

```bash
# Clone o repositório na sua pasta de documentos
cd "$HOME\Documents"
git clone https://github.com/paixaoinfo/ntc-ide-pro.git

# Execute o script de configuração local para registrar 'ntc-ide' globalmente
cd ntc-ide-pro
./setup_ntc_ide_pro.ps1
```

### 3. Uso

Uma vez registrado, você pode invocar o seu workspace isolado de qualquer diretório:

```bash
ntc-ide .
```

# 💻 Minha Configuração de Terminal (Zsh + iTerm2 + Starship)

Este README apresenta **um guia completo e cronológico** para configurar meu terminal no macOS. O objetivo é criar um ambiente:

* rápido ⚡
* moderno 🎨
* produtivo 🧠
* repleto de ícones Nerd Font ✨
* perfeito para desenvolvimento em Flutter/Dart

Tudo explicadinho como um tutorial do zero ao avançado.

---

# 📦 1. Requisitos

Antes de começar, você precisa ter:

* macOS
* Homebrew instalado
* Zsh (já é o shell padrão do macOS)
* Acesso ao arquivo `~/.zshrc`

---

# 🪟 2. Instalar o iTerm2

Meu terminal principal.

### 🔽 2.1. Baixar

[https://iterm2.com/](https://iterm2.com/)

### 💾 2.2. Instalar

1. Abra o `.dmg`
2. Arraste para Applications
3. Abra via Spotlight

---

# 🖋️ 3. Instalar a JetBrains Mono Nerd Font

Necessária para ícones perfeitos no terminal.

### 🔽 3.1. Instalar via Homebrew

```sh
brew install --cask font-jetbrains-mono-nerd-font
```

### 🔧 3.2. Configurar fonte no iTerm2

1. Preferences → Profiles → Text
2. Fonte → **JetBrainsMono Nerd Font**
3. (Opcional) Use a different font for non‑ASCII

---

# ⚙️ 4. Instalar Ferramentas Essenciais

Instale isso ANTES de configurar o `.zshrc` (porque ele usa essas ferramentas!).

---

## 🔹 4.1. EZA – substituto moderno do `ls`

```sh
brew install eza
```

Aliases usados:

```sh
alias ls="eza --icons"
alias ll="eza -l --icons"
alias la="eza -la --icons"
alias lt="eza --tree --icons"
alias l.="eza -a --icons | grep '^\.'"
```

---

## 🔹 4.2. Zoxide – cd inteligente

```sh
brew install zoxide
```

Exemplos:

* `z projetos`
* `zoxide query -l`

Alias útil:

```sh
alias zz="zoxide query -l | fzf | xargs z"
```

---

## 🔹 4.3. BAT – cat com syntax highlight

```sh
brew install bat
```

Integrando com Git:

```sh
git config --global core.pager "bat --paging=always"
```

---

## 🔹 4.4. FZF – busca fuzzy

```sh
brew install fzf
$(brew --prefix)/opt/fzf/install
```

Atalhos:

* **Ctrl+R** → histórico
* **Ctrl+T** → busca arquivos

---

## 🔹 4.5. ripgrep – busca ultrarrápida

```sh
brew install ripgrep
```

---

# 🚀 5. Instalar Starship Prompt

Prompt minimalista e extremamente customizável.

### 🔽 5.1. Instalar

```sh
brew install starship
mkdir -p ~/.config
touch ~/.config/starship.toml
```

---

# 🖥️ 6. Configurar o Shell (ZSH)

Agora que todas as ferramentas estão instaladas, configuramos o ZSH corretamente.

### 🔧 6.1. Meu `.zshrc` completo

```sh
export HISTFILE=~/.zsh_history
export HISTSIZE=100000
export SAVEHIST=100000

setopt CORRECT

autoload -Uz compinit
compinit

eval "$(starship init zsh)"
eval "$(zoxide init zsh)"

alias ls="eza --icons"
alias ll="eza -l --icons"
alias la="eza -la --icons"
alias lt="eza --tree --icons"
alias l.="eza -a --icons | grep '^\.'"
```

Explica:

* histórico maior
* autocorreção leve
* autocompletar ativo
* zoxide inicializado
* starship inicializado
* ls moderno com ícones

---

# 🌟 7. Configurar o Starship (`starship.toml`)

A alma do visual do terminal.

```toml
[custom.flutter]
detect_files = ["pubspec.yaml"]
command = "flutter --version --machine | jq -r '.frameworkVersion'"
symbol = ""
format = "[$symbol v$output]($style) "
style = "bold blue"

[os]
disabled = false
style = "bold white"

[os.symbols]
Macos = " "
```

### Como funciona o módulo Flutter

* Detecta `pubspec.yaml`
* Extrai versão exata do Flutter
* Mostra ícone `` + versão

### Como funciona o módulo macOS

* Mostra ícone do macOS ``
* Sempre visível

---

# 📦 8. Módulo Package

Exibe a versão do projeto Flutter/Dart:

```txt
📦 v1.0.0+1
```

Para customizar:

```toml
[package]
symbol = "📦 "
```

---

# 🧪 9. Testando as Nerd Fonts

```sh
echo " Flutter"
echo " Dart"
echo " macOS"
```

Se aparecer quadrado → fonte não aplicada.

---

# 🧊 10. Prévia do Resultado Final

```txt
app-controle-de-agua on  main  📦 v1.0.0+1   v3.10.0  
❯
```

---

# 📘 11. Como Copiar Minha Configuração

1. Instale iTerm2
2. Instale JetBrains Mono Nerd Font
3. Configure no iTerm2
4. Instale ferramentas (EZA, Zoxide, FZF…)
5. Instale Starship
6. Copie meu `.zshrc`
7. Copie meu `starship.toml`
8. Reinicie o terminal

---

# 💡 12. Módulos Extras

## Dart

```toml
[custom.dart]
detect_files = ["pubspec.yaml"]
command = "dart --version 2>&1 | head -n 1 | sed 's/Dart SDK version //g'"
symbol = ""
format = "[$symbol v$output]($style) "
style = "bold cyan"
```

## Git

```toml
[git_branch]
symbol = " "
style = "bold purple"
format = "[$symbol$branch]($style) "

[git_status]
style = "bold yellow"
format = "([$all_status]($style) )"
```

---

# ✨ 13. Dicas Finais

* Use tema escuro para realçar os ícones
* Mantenha seu `starship.toml` no Git para backup
* Zoxide + FZF + EZA = velocidade máxima no terminal

---
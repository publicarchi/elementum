---
since: 2025-08-13
tags: terminal, bash
---

# Terminal

Theme : robbyrussell +++

- clean +
- cloud
- garyblessington +
- gozilla
- zhann +

Nécessitant installation

- Pure https://github.com/sindresorhus/pure
- spaceship https://spaceship-prompt.sh

Installer des plugins avec Oh-MyZSH

- https://github.com/zsh-users/zsh-autocoplete
- https://github.com/zsh-users/zsh-syntax-highlighting
- https://github.com/spaceship-prompt/spaceship-prompt.git

Dans `.zprofile` ou `.zsh`

```bash
ZSH_THEME="spaceship"

plugins=(
  git
  zsh-autosuggestions
  zsh-syntax-highlighting
)
```

```bash
# clone the repo
git clone https://github.com/spaceship-prompt/spaceship-prompt.git "$ZSH_CUSTOM/themes/spaceship-prompt" --depth=1

# Link the theme
ln -s "$ZSH_CUSTOM/themes/spaceship-prompt/spaceship.zsh-theme" "$ZSH_CUSTOM/themes/spaceship.zsh-theme"
```
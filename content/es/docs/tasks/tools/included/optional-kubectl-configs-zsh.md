---
title: "Autocompletar zsh"
description: "Alguna configuración opcional para la finalización automática de zsh."
headless: true
---

El script de finalización de kubectl para Zsh se puede generar con el comando `kubectl completion zsh`. Obtener el script de finalización en su shell habilita el autocompletado de kubectl.

Para hacerlo en todas sus sesiones de shell, agregue lo siguiente a su`~/.zshrc` expediente:

```zsh
source <(kubectl completion zsh)
```
Si tiene un alias para kubectl, puede extender la finalización del shell para trabajar con ese alias:

```zsh
echo 'alias k=kubectl' >>~/.zshrc
echo 'complete -F __start_kubectl k' >>~/.zshrc
```

Después de recargar su shell, el autocompletado de kubectl debería estar funcionando.

Si recibe un error como `complete:13: command not found: compdef`, 
luego agregue lo siguiente al comienzo de su `~/.zshrc` expediente:

```zsh
autoload -Uz compinit
compinit
```
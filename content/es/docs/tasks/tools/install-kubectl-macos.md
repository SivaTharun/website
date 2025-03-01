---
reviewers:
title: Instalar y configurar kubectl en macOS
content_type: task
weight: 10
card:
  name: tasks
  weight: 20
  title: Instalar kubectl en macOS
---

## {{% heading "prerequisites" %}}

Debes usar una versión de kubectl que esté dentro de una diferencia de versión menor de tu clúster. Por ejemplo, un v{{< skew latestVersion >}} La cliente puede comunicarse con v{{< skew prevMinorVersion >}}, v{{< skew latestVersion >}}, and v{{< skew nextMinorVersion >}} aviones de control.
El uso de la última versión de kubectl ayuda a evitar problemas imprevistos.

## Instalar kubectl en macOS

Existen los siguientes métodos para instalar kubectl en macOS:

- [Instalar kubectl binary con curl en macOS](#install-kubectl-binary-with-curl-on-macos)
- [Instalar con Homebrew en macOS](#install-with-homebrew-on-macos)
- [Instalar con Macports en macOS](#install-with-macports-on-macos)

### Instalar kubectl binary con curl en macOS

1. Descargue la última versión:

   {{< tabs name="download_binary_macos" >}}
   {{< tab name="Intel" codelang="bash" >}}
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl"
   {{< /tab >}}
   {{< tab name="Apple Silicon" codelang="bash" >}}
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/arm64/kubectl"
   {{< /tab >}}
   {{< /tabs >}}

   {{< note >}}
   Para descargar una versión específica, reemplace el `$(curl -L -s https://dl.k8s.io/release/stable.txt)` parte del comando con la versión específica.

   Por ejemplo, para descargar la versión {{< param "fullversion" >}} en Intel macOS, escriba:

   ```bash
   curl -LO "https://dl.k8s.io/release/{{< param "fullversion" >}}/bin/darwin/amd64/kubectl"
   ```

   Y para macOS en Apple Silicon, escriba:

   ```bash
   curl -LO "https://dl.k8s.io/release/{{< param "fullversion" >}}/bin/darwin/arm64/kubectl"
   ```

   {{< /note >}}

1. Validar el binario (opcional)

   Descargue el archivo de suma de comprobación de kubectl:

   {{< tabs name="download_checksum_macos" >}}
   {{< tab name="Intel" codelang="bash" >}}
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl.sha256"
   {{< /tab >}}
   {{< tab name="Apple Silicon" codelang="bash" >}}
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/arm64/kubectl.sha256"
   {{< /tab >}}
   {{< /tabs >}}
  
   Valide el binario kubectl con el archivo de suma de comprobación:

   ```bash
   echo "$(<kubectl.sha256)  kubectl" | shasum -a 256 --check
   ```

   Si es válido, la salida es:

   ```console
   kubectl: OK
   ```

   Si la verificación falla, `shasum` sale con un estado distinto de cero e imprime una salida similar a:

   ```bash
   kubectl: FAILED
   shasum: WARNING: 1 computed checksum did NOT match
   ```

   {{< note >}}
   Descargue la misma versión del binario y la suma de comprobación.
   {{< /note >}}

1. Hacer ejecutable el binario de kubectl.

   ```bash
   chmod +x ./kubectl
   ```

1. Mueva el binario kubectl a una ubicación de archivo en su sistema `PATH`.

   ```bash
   sudo mv ./kubectl /usr/local/bin/kubectl
   sudo chown root: /usr/local/bin/kubectl
   ```

   {{< note >}}
   Cerciorarse `/usr/local/bin` está en su variable de entorno PATH.
   {{< /note >}}

1. Pruebe para asegurarse de que la versión que instaló esté actualizada:

   ```bash
   kubectl version --client
   ```

### Instalar con Homebrew en macOS

Si está en macOS y usa [Homebrew](https://brew.sh/) administrador de paquetes, puede instalar kubectl con Homebrew.

1. Ejecute el comando de instalación:

   ```bash
   brew install kubectl 
   ```

   or

   ```bash
   brew install kubernetes-cli
   ```

1. Pruebe para asegurarse de que la versión que instaló esté actualizada:

   ```bash
   kubectl version --client
   ```

### Instalar con Macports en macOS

Si está en macOS y usa [Macports](https://macports.org/) administrador de paquetes, puede instalar kubectl con Macports.

1. Ejecute el comando de instalación:

   ```bash
   sudo port selfupdate
   sudo port install kubectl
   ```

1. Pruebe para asegurarse de que la versión que instaló esté actualizada:

   ```bash
   kubectl version --client
   ```

## Verificar la configuración de kubectl

{{< include "included/verify-kubectl.md" >}}

## Complementos y configuraciones opcionales de kubectl

### Habilitar el autocompletado de shell

kubectl proporciona soporte de autocompletado para Bash y Zsh, lo que puede ahorrarle mucho escribir.

A continuación, se muestran los procedimientos para configurar el autocompletado para Bash y Zsh.

{{< tabs name="kubectl_autocompletion" >}}
{{< tab name="Bash" include="included/optional-kubectl-configs-bash-mac.md" />}}
{{< tab name="Zsh" include="included/optional-kubectl-configs-zsh.md" />}}
{{< /tabs >}}

### Instalar el complemento `kubectl convert`

{{< include "included/kubectl-convert-overview.md" >}}

1. Descargue la última versión con el comando:

   {{< tabs name="download_convert_binary_macos" >}}
   {{< tab name="Intel" codelang="bash" >}}
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl-convert"
   {{< /tab >}}
   {{< tab name="Apple Silicon" codelang="bash" >}}
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/arm64/kubectl-convert"
   {{< /tab >}}
   {{< /tabs >}}

1. Validar el binario (opcional)

   Descargue el archivo de suma de comprobación de kubectl:

   {{< tabs name="download_convert_checksum_macos" >}}
   {{< tab name="Intel" codelang="bash" >}}
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl-convert.sha256"
   {{< /tab >}}
   {{< tab name="Apple Silicon" codelang="bash" >}}
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/arm64/kubectl-convert.sha256"
   {{< /tab >}}
   {{< /tabs >}}

   Valide el binario kubectl-convert con el archivo de suma de comprobación:

   ```bash
   echo "$(<kubectl-convert.sha256)  kubectl-convert" | shasum -a 256 --check
   ```

   Si es válido, la salida es:

   ```console
   kubectl-convert: OK
   ```

   Si la verificación falla, `shasum` sale con un estado distinto de cero e imprime una salida similar a:

   ```bash
   kubectl-convert: FAILED
   shasum: WARNING: 1 computed checksum did NOT match
   ```

   {{< note >}}
   Descargue la misma versión del binario y la suma de comprobación.
   {{< /note >}}

1. Hacer ejecutable kubectl-convert binary

   ```bash
   chmod +x ./kubectl-convert
   ```

1. Mueva el binario kubectl-convert a una ubicación de archivo en su sistema`PATH`.

   ```bash
   sudo mv ./kubectl-convert /usr/local/bin/kubectl-convert
   sudo chown root: /usr/local/bin/kubectl-convert
   ```

   {{< note >}}
   Cerciorarse `/usr/local/bin` está en tu PATH Variable ambiental.
   {{< /note >}}

1. Verifique que el complemento se haya instalado correctamente

   ```shell
   kubectl convert --help
   ```

   Si no ve un error, significa que el complemento se instaló correctamente.

## {{% heading "whatsnext" %}}

{{< include "included/kubectl-whats-next.md" >}}

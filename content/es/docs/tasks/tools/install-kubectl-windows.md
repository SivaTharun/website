---
reviewers:
title: Instalar y configurar kubectl en Windows
content_type: task
weight: 10
card:
  name: tasks
  weight: 20
  title: Instalar kubectl en Windows
---

## {{% heading "prerequisites" %}}

Debes usar una versión de kubectl que esté dentro de una diferencia de versión menor de tu clúster. Por ejemplo, un v{{< skew latestVersion >}} La cliente puede comunicarse con v{{< skew prevMinorVersion >}}, v{{< skew latestVersion >}}, y v{{< skew nextMinorVersion >}} aviones de control.

El uso de la última versión de kubectl ayuda a evitar problemas imprevistos.

## Instalar kubectl en Windows

Existen los siguientes métodos para instalar kubectl en Windows:

- [Instalar kubectl binary con curl en Windows](#install-kubectl-binary-with-curl-on-windows)
- [Instalar en Windows usando Chocolatey o Scoop](#install-on-windows-using-chocolatey-or-scoop)


### Instalar kubectl binary con curl en Windows

1. Descarga la [última versión {{< param "fullversion" >}}](https://dl.k8s.io/release/{{< param "fullversion" >}}/bin/windows/amd64/kubectl.exe).

   O si tiene `curl` instalado, use este comando:

   ```powershell
   curl -LO https://dl.k8s.io/release/{{< param "fullversion" >}}/bin/windows/amd64/kubectl.exe
   ```

   {{< note >}}
   Para conocer la última versión estable (por ejemplo, para secuencias de comandos), eche un vistazo a [https://dl.k8s.io/release/stable.txt](https://dl.k8s.io/release/stable.txt).
   {{< /note >}}

1. Validar el binario (opcional)

   Descargue el archivo de suma de comprobación de kubectl:

   ```powershell
   curl -LO https://dl.k8s.io/{{< param "fullversion" >}}/bin/windows/amd64/kubectl.exe.sha256
   ```

   Valide el binario kubectl con el archivo de suma de comprobación:

   - Usando el símbolo del sistema para comparar manualmente la salida de `CertUtil` con el archivo de suma de comprobación descargado:

     ```cmd
     CertUtil -hashfile kubectl.exe SHA256
     type kubectl.exe.sha256
     ```

   - Usando PowerShell para automatizar la verificación usando el `-eq` Operadora para obtener una `True` o `False` resultado:

     ```powershell
     $($(CertUtil -hashfile .\kubectl.exe SHA256)[1] -replace " ", "") -eq $(type .\kubectl.exe.sha256)
     ```

1. Agregue el binario a su `PATH`.

1. Prueba para asegurar la versión de`kubectl` Es la misma que descargada:

   ```cmd
   kubectl version --client
   ```

{{< note >}}
[Docker Desktop para Windows](https://docs.docker.com/docker-for-windows/#kubernetes) agrega su propia versión de `kubectl` a` PATH`.
Si ha instalado Docker Desktop antes, es posible que deba colocar su `PATH` entrada antes de la agregada por el instalador de Docker Desktop o elimine el `kubectl`.
{{< /note >}}

### Instalar en Windows usando Chocolatey o Scoop

1. Para instalar kubectl en Windows, puede usar [Chocolatey](https://chocolatey.org) 
administrador de paquetes o [Scoop](https://scoop.sh) instalador de línea de comandos.

   {{< tabs name="kubectl_win_install" >}}
   {{% tab name="choco" %}}
   ```powershell
   choco install kubernetes-cli
   ```
   {{% /tab %}}
   {{% tab name="scoop" %}}
   ```powershell
   scoop install kubectl
   ```
   {{% /tab %}}
   {{< /tabs >}}


1. Pruebe para asegurarse de que la versión que instaló esté actualizada:

   ```powershell
   kubectl version --client
   ```

1. Navegue a su directorio de inicio:

   ```powershell
   # Si estas usando cmd.exe, correr: cd %USERPROFILE%
   cd ~
   ```

1. Cree el directorio `.kube`:

   ```powershell
   mkdir .kube
   ```

1. Cambie al directorio `.kube` que acaba de crear:

   ```powershell
   cd .kube
   ```

1. Configure kubectl para usar un clúster de Kubernetes remoto:

   ```powershell
   New-Item config -type file
   ```

{{< note >}}
Edite el archivo de configuración con un editor de texto de su elección, como el Bloc de notas.
{{< /note >}}

## Verificar la configuración de kubectl

{{< include "included/verify-kubectl.md" >}}

## Complementos y configuraciones opcionales de kubectl

### Habilitar el autocompletado de shell

kubectl proporciona soporte de autocompletado para Bash y Zsh, lo que puede ahorrarle mucho escribir.

A continuación se muestran los procedimientos para configurar el autocompletado para Zsh, si lo está ejecutando en Windows.

{{< include "included/optional-kubectl-configs-zsh.md" >}}

### Install `kubectl convert` plugin

{{< include "included/kubectl-convert-overview.md" >}}

1. Descargue la última versión con el comando:

   ```powershell
   curl -LO https://dl.k8s.io/release/{{< param "fullversion" >}}/bin/windows/amd64/kubectl-convert.exe
   ```

1. Validar el binario (opcional)

   Descargue el archivo de suma de comprobación kubectl-convert:

   ```powershell
   curl -LO https://dl.k8s.io/{{< param "fullversion" >}}/bin/windows/amd64/kubectl-convert.exe.sha256
   ```

   Valide el binario kubectl-convert con el archivo de suma de comprobación:

   - Usando el símbolo del sistema para comparar manualmente la salida de `CertUtil` con el archivo de suma de comprobación descargado:

     ```cmd
     CertUtil -hashfile kubectl-convert.exe SHA256
     type kubectl-convert.exe.sha256
     ```

   - Usando PowerShell para automatizar la verificación usando el `-eq` 
     Operadora para obtener una `True` or `False` resultado:

     ```powershell
     $($(CertUtil -hashfile .\kubectl-convert.exe SHA256)[1] -replace " ", "") -eq $(type .\kubectl-convert.exe.sha256)
     ```

1. Agregue el binario a su`PATH`.

1. Verifique que el complemento se haya instalado correctamente

   ```shell
   kubectl convert --help
   ```

   Si no ve un error, significa que el complemento se instaló correctamente.

## {{% heading "whatsnext" %}}

{{< include "included/kubectl-whats-next.md" >}}

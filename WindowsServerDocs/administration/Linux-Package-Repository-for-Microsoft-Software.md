---
title: Linux-Softwarerepository für Microsoft-Produkte
description: In diesem Dokument wird beschrieben, wie Sie Linux-Softwarepakete für Microsoft-Produkte verwenden und installieren.
ms.topic: article
ms.assetid: b5387444-595f-4f38-abb7-163a70ea1895
author: victorcheng7
ms.author: vichen
ms.date: 08/14/2020
ms.openlocfilehash: 28ce502a78c58eda74d5b412fe4e4d0d3279d442
ms.sourcegitcommit: dac52260fdcc3721daf7e32cd45760a0ced96de7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2020
ms.locfileid: "91663681"
---
# <a name="linux-software-repository-for-microsoft-products"></a>Linux-Softwarerepository für Microsoft-Produkte

## <a name="overview"></a>Übersicht

Microsoft erstellt und unterstützt eine Vielzahl von Softwareprodukten für Linux-Systeme und macht Sie über standardmäßige apt-und yum-paketrepositorys verfügbar. In diesem Dokument wird beschrieben, wie Sie das Repository auf Ihrem Linux-System konfigurieren, damit Sie die Linux-Software von Microsoft mithilfe der Standardpaket Verwaltungs Tools Ihrer Distribution installieren/aktualisieren können.

Das Linux-Softwarerepository von Microsoft besteht aus mehreren untergeordneten Depots:

 - Prod – das produktionssubrepository ist für Pakete vorgesehen, die für die Verwendung in der Produktion bestimmt sind. Diese Pakete werden kommerziell von Microsoft gemäß den Bedingungen des anwendbaren Supportvertrags oder des Programms, das Sie mit Microsoft haben, unterstützt.

 - MSSQL-Server: diese Depots enthalten Pakete für Microsoft SQL Server für Linux-siehe auch: [SQL Server für Linux](https://www.microsoft.com/sql-server/sql-server-vnext-including-Linux).

> [!NOTE]
> Pakete in den Linux-Softwarerepositorys unterliegen den Lizenzbedingungen, die sich in den Paketen befinden. Lesen Sie vor Verwendung des Pakets die Lizenzbedingungen. Durch die Installation und Nutzung des Pakets erklären Sie sich mit diesen Bedingungen einverstanden. Wenn Sie mit den Lizenzbedingungen nicht einverstanden sind, verwenden Sie das Paket nicht.

## <a name="configuring-the-repositories"></a>Konfigurieren der Depots

Depots können automatisch durch Installieren des Linux-Pakets konfiguriert werden, das für Ihre Linux-Distribution und-Version gilt. Das Paket installiert die Repository-Konfiguration zusammen mit dem öffentlichen GPG-Schlüssel, der von Tools wie z. b. apt/yum/zypperverwendet wird, um die signierten Pakete und/oder Repository-Metadaten zu validieren.

### <a name="enterprise-linux-rhel-and-variants"></a>Enterprise Linux (RHEL und Varianten)

 - Enterprise Linux 6 (EL6)<p>`sudo rpm -Uvh https://packages.microsoft.com/config/rhel/6/packages-microsoft-prod.rpm`

 - Enterprise Linux 7 (EL7)<p>`sudo rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm`

 - Enterprise Linux 8 (EL8)<p>`sudo rpm -Uvh https://packages.microsoft.com/config/rhel/8/packages-microsoft-prod.rpm`

### <a name="suse"></a>SUSE

 - SUSE Linux Enterprise Server 12<p>`sudo rpm -Uvh https://packages.microsoft.com/config/sles/12/packages-microsoft-prod.rpm`

 - SUSE Linux Enterprise Server 15<p>`sudo rpm -Uvh https://packages.microsoft.com/config/sles/15/packages-microsoft-prod.rpm`

### <a name="ubuntu"></a>Ubuntu

 - Ubuntu 16,04 (xenial)<p>`curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -`<p>`sudo apt-add-repository https://packages.microsoft.com/ubuntu/16.04/prod`<p>`sudo apt-get update`

 - Ubuntu 18,04 (Bionic)<p>`curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -`<p>`sudo apt-add-repository https://packages.microsoft.com/ubuntu/18.04/prod`<p>`sudo apt-get update`

 - Ubuntu 20,04 (Fokus)<p>`curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -`<p>`sudo apt-add-repository https://packages.microsoft.com/ubuntu/20.04/prod`<p>`sudo apt-get update`

## <a name="manual-configuration"></a>Manuelle Konfiguration

Die Repository-Konfigurationsdateien sind über [Packages.Microsoft.com/config](https://packages.microsoft.com/config/)verfügbar. Der Name und der Speicherort dieser Dateien können mit der folgenden URI-Benennungs Konvention gefunden werden:

`https://packages.microsoft.com/config/<Distribution>/<Version>/prod.(repo|list)`

### <a name="package-and-repository-signing-key"></a>Signierungs Schlüssel für Paket und Repository

- Der öffentliche GPG-Schlüssel von Microsoft kann hier heruntergeladen werden: [https://packages.microsoft.com/keys/microsoft.asc](https://packages.microsoft.com/keys/microsoft.asc)
- ID des öffentlichen Schlüssels: Microsoft (releasesignierung) <gpgsecurity@microsoft.com>
- Fingerabdruck des öffentlichen Schlüssels: `BC52 8686 B50D 79E3 39D3 721C EB3E 94AD BE12 29CF`

### <a name="examples"></a>Beispiele

 - RHEL/CentOS 7

```
# Install repository configuration
curl -sSL https://packages.microsoft.com/config/rhel/7/prod.repo | sudo tee /etc/yum.repos.d/microsoft-prod.repo

# Install Microsoft's GPG public key
curl -sSL https://packages.microsoft.com/keys/microsoft.asc > ./microsoft.asc
sudo rpm --import ./microsoft.asc
```

 - Ubuntu 20.04

```
# Install repository configuration
curl -sSL https://packages.microsoft.com/config/ubuntu/20.04/prod.list | sudo tee /etc/apt/sources.list.d/microsoft-prod.list

# Install Microsoft GPG public key
curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -

# Update package index files
sudo apt-get update
```

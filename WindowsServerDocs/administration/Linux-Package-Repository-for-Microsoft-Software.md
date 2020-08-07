---
title: Linux-Softwarerepository für Microsoft-Produkte
description: In diesem Dokument wird beschrieben, wie Sie Linux-Softwarepakete für Microsoft-Produkte verwenden und installieren.
manager: szark
ms.topic: article
ms.assetid: b5387444-595f-4f38-abb7-163a70ea1895
author: szarkos
ms.author: szark
ms.date: 10/16/2017
ms.openlocfilehash: f8d31aaeaba4bba6cf6caaa2a69190cfdbd8e488
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879521"
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

- Enterprise Linux 6 (EL6)<p>sudo rpm-Uvhhttps://packages.microsoft.com/config/rhel/6/packages-microsoft-prod.rpm

- Enterprise Linux 7 (EL7)<p>sudo rpm-Uvhhttps://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm


### <a name="ubuntu"></a>Ubuntu

 - Ubuntu 14,04 (trusty)<p>cURL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key Add-sudo apt-Add-Repositoryhttps://packages.microsoft.com/ubuntu/14.04/prod<p>sudo apt-get update

 - Ubuntu 16,04 (xenial)<p>cURL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key Add-sudo apt-Add-Repositoryhttps://packages.microsoft.com/ubuntu/16.04/prod<p>sudo apt-get update

 - Ubuntu 18,04 (Bionic)<p>cURL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key Add-sudo apt-Add-Repositoryhttps://packages.microsoft.com/ubuntu/18.04/prod<p>sudo apt-get update

 - Ubuntu 18,10 (kosmisch)<p>cURL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key Add-sudo apt-Add-Repositoryhttps://packages.microsoft.com/ubuntu/18.10/prod<p>sudo apt-get update

 - Ubuntu 19,04 (Disco)<p>cURL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key Add-sudo apt-Add-Repositoryhttps://packages.microsoft.com/ubuntu/19.04/prod<p>sudo apt-get update

### <a name="suse-linux-enterprise-12"></a>SUSE Linux Enterprise 12

sudo rpm-Uvhhttps://packages.microsoft.com/config/sles/12/packages-microsoft-prod.rpm

## <a name="manual-configuration"></a>Manuelle Konfiguration

Die Repository-Konfigurationsdateien sind über [Packages.Microsoft.com/config](https://packages.microsoft.com/config/)verfügbar. Der Name und der Speicherort dieser Dateien können mit der folgenden URI-Benennungs Konvention gefunden werden:

https://packages.microsoft.com/config/<Distribution>/<Version>Prod. (Repository | Liste)

**Signierungs Schlüssel für Paket und Repository**

- Der öffentliche GPG-Schlüssel von Microsoft kann hier heruntergeladen werden:[https://packages.microsoft.com/keys/microsoft.asc](https://packages.microsoft.com/keys/microsoft.asc)
- ID des öffentlichen Schlüssels: Microsoft (releasesignierung)<gpgsecurity@microsoft.com>
- Fingerabdruck des öffentlichen Schlüssels:`BC52 8686 B50D 79E3 39D3 721C EB3E 94AD BE12 29CF`

### <a name="examples"></a>Beispiele

 - RHEL/CentOS 7

```
# Install repository configuration
curl https://packages.microsoft.com/config/rhel/7/prod.repo > ./microsoft-prod.repo
sudo cp ./microsoft-prod.repo /etc/yum.repos.d/

# Install Microsoft's GPG public key
curl https://packages.microsoft.com/keys/microsoft.asc > ./microsoft.asc
sudo rpm --import ./microsoft.asc
```

- Ubuntu 16.04

```
# Install repository configuration
curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/

# Install Microsoft GPG public key
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
```

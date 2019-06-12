---
title: Linux-Software-Repository für Microsoft-Produkte
description: Dieses Dokument beschreibt, wie und Linux-Software-Pakete für Microsoft-Produkte installieren.
ms.custom: na
ms.prod: windows-server-threshold
ms.service: na
manager: szark
ms.technology: compute
ms.topic: article
ms.assetid: b5387444-595f-4f38-abb7-163a70ea1895
author: szarkos
ms.author: szark
ms.date: 10/16/2017
ms.openlocfilehash: 3b4feb6b8b3dad5c34de92f634eb30d0e952fe76
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435776"
---
# <a name="linux-software-repository-for-microsoft-products"></a>Linux-Software-Repository für Microsoft-Produkte

## <a name="overview"></a>Übersicht
Microsoft erstellt und unterstützt eine Vielzahl von Softwareprodukten für Linux-Systemen und stellt sie über standard APT und YUM-Package-Repositorys zur Verfügung. In diesem Dokument wird beschrieben, wie so konfigurieren Sie das Repository auf Ihrem Linux-System, sodass Sie Sie dann installieren/Linux-Software von Microsoft über die Verwaltungstools für Ihre Distribution des standard-Pakets aktualisieren können.

Microsoft Linux-Softwarerepository besteht aus mehreren untergeordneten Repositorys:

 - Produktion: die Produktion unterrepository für Pakete, die für die Verwendung in einer produktionsumgebung vorgesehen festgelegt ist. Diese Pakete werden im Handel von Microsoft unterstützt, unter den Bedingungen des entsprechenden Support-Vertrag oder Programm, das Sie bei Microsoft verfügen.

 - MSSQL-Server - enthalten diese Repositorys-Paket für Microsoft SQL Server unter Linux – Siehe auch: [SQLServer unter Linux](https://www.microsoft.com/en-us/sql-server/sql-server-vnext-including-Linux).

> [!Note]
> Pakete in der Linux-Softwarerepositorys unterliegen den Lizenzbedingungen in den Paketen ab. Lesen Sie die Lizenzbedingungen zustimmen, bevor Sie das Paket verwenden. Die Installation und Verwendung des Pakets bildet Ihre Zustimmung für diese Begriffe. Wenn Sie den Lizenzbedingungen nicht einverstanden sind, verwenden Sie das Paket nicht.


## <a name="configuring-the-repositories"></a>Konfigurieren die Repositorys
Repositorys können automatisch so konfiguriert werden, durch Installieren des Linux-Pakets, die für Ihre Linux-Distribution und Version angewendet wird. Das Paket installiert die Repository-Konfiguration zusammen mit dem öffentlichen GPG-Schlüssel, die von Tools wie z. B. apt/Yum/Zypper verwendet werden, um die signierten Paketen und/oder die Repository-Metadaten zu überprüfen.

### <a name="enterprise-linux-rhel-and-variants"></a>Enterprise Linux (RHEL und Varianten davon)

 - Enterprise Linux 6 (EL6)

        sudo rpm -Uvh https://packages.microsoft.com/config/rhel/6/packages-microsoft-prod.rpm

 - Enterprise Linux 7 (EL7)

        sudo rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm


### <a name="ubuntu"></a>Ubuntu

 - Ubuntu 14.04 (Trusty)

        wget https://packages.microsoft.com/config/ubuntu/14.04/packages-microsoft-prod.deb
        sudo dpkg -i packages-microsoft-prod.deb
        sudo apt-get update

 - Ubuntu 16.04 (Xenial)

        wget https://packages.microsoft.com/config/ubuntu/16.04/packages-microsoft-prod.deb
        sudo dpkg -i packages-microsoft-prod.deb
        sudo apt-get update

 - Ubuntu 16.10 (Yakkety)

        wget https://packages.microsoft.com/config/ubuntu/16.10/packages-microsoft-prod.deb
        sudo dpkg -i packages-microsoft-prod.deb
        sudo apt-get update


### <a name="suse-linux-enterprise-12"></a>SUSE Linux Enterprise 12

        sudo rpm -Uvh https://packages.microsoft.com/config/sles/12/packages-microsoft-prod.rpm


## <a name="manual-configuration"></a>Manuelle Konfiguration
Die Repository-Konfigurationsdateien stehen über [packages.microsoft.com/config](https://packages.microsoft.com/config/). Der Name und Speicherort dieser Dateien gesucht werden, indem die folgenden URI-Namenskonvention sind möglich:

        https://packages.microsoft.com/config/<Distribution>/<Version>/prod.(repo|list)

**Paket und die Signatur von Repository-Schlüssel**

 - Öffentliche Microsoft GPG-Schlüssel kann hier heruntergeladen werden: [https://packages.microsoft.com/keys/microsoft.asc](https://packages.microsoft.com/keys/microsoft.asc)
 - Öffentliche Schlüssel-ID: Microsoft (Signieren von Version) <gpgsecurity@microsoft.com>
 - Fingerabdrucks: `BC52 8686 B50D 79E3 39D3 721C EB3E 94AD BE12 29CF`

### <a name="examples"></a>Beispiele:

 - RHEL/CentOS 7

        # Install repository configuration
        curl https://packages.microsoft.com/config/rhel/7/prod.repo > ./microsoft-prod.repo
        sudo cp ./microsoft-prod.repo /etc/yum.repos.d/

        # Install Microsoft's GPG public key
        curl https://packages.microsoft.com/keys/microsoft.asc > ./microsoft.asc
        sudo rpm --import ./microsoft.asc

 - Ubuntu 16.04

        # Install repository configuration
        curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list
        sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/

        # Install Microsoft GPG public key
        curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
        sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/




---
title: Migrieren der Remotedesktopdienste-Bereitstellung auf Windows Server 2016
description: Dieser Artikel beschreibt, wie Sie Ihre Remote Desktop Services-Bereitstellung auf neuen Windows Server 2016-Server zu migrieren.
ms.custom: na
ms.prod: windows-server-threshold
msreviewer: ''
nams.suite: ''
nams.technology: remote-desktop-services
ms.author: chrimo
ms.date: 11/01/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9b1fa833-4325-48a8-bf34-46265f40c001
author: christianmontoya
manager: scottman
ms.openlocfilehash: 0e4736f753fc0ad2ece6135de84d481eecb8b7a1
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812584"
---
# <a name="migrate-your-remote-desktop-services-deployment-to-windows-server-2016"></a>Migrieren der Remotedesktopdienste-Bereitstellung auf Windows Server 2016

Wenn Sie derzeit Remote Desktop Services in Windows Server 2012 R2 ausführen, können Sie auf Windows Server 2016 verschieben, um neue Funktionen wie Unterstützung für Azure SQL- und "direkte Speicherplätze" nutzen.

Migration für eine Remotedesktopdienste-Bereitstellung wird von Quellservern unter Windows Server 2016 zu Zielservern unter Windows Server 2016 unterstützt. Das heißt, gibt es keine direkte direkte Migration von RDS unter Windows Server 2012 R2 auf Windows Server 2016. Stattdessen für die meisten der RDS-Komponenten, Sie zunächst ein upgrade auf Windows Server 2016, und klicken Sie dann auf die Migration und Lizenzen. Die einzigen Komponenten mit einer direkten Migration sind RD-Web und RD-Gateway den Lizenzserver.

Weitere Informationen zu den Upgradeprozess und die Anforderungen, finden Sie unter [Ihre Remote Desktop Services-Bereitstellungen auf Windows Server 2016 Upgrade](upgrade-to-rds-2016.md).

Verwenden Sie die folgenden Schritte aus, um Ihre Remote Desktop Services-Bereitstellung zu migrieren:

- [Migrieren von RD-Verbindungsbrokerserver](#migrate-rdconnection-broker-servers)

- [Migrieren von sitzungssammlungen](#migrate-session-collections)

- [Migrieren von Sammlungen virtueller Desktops](#migrate-virtual-desktop-collections)

- [Migrieren von Servern mit Web Access für Remotedesktop](#migrate-rdweb-access-servers)

- [Migrieren von RD-Gatewayservern](#migrate-rdgateway-servers)

- [Migrieren des Remotedesktop-Lizenzierungsservern](#migrate-rdgateway-servers)

- [Migrieren von Zertifikaten](#migrate-certificates)

## <a name="migrate-rdconnection-broker-servers"></a>Migrieren von RD-Verbindungsbrokerserver

Dies ist der erste und wichtigste Schritt für die Migration: Migrieren Ihren Remotedesktop-Verbindungsbroker zu Zielservern unter Windows Server 2016.

> [!IMPORTANT]
> Der Quellserver des Remotedesktop-Verbindungsbroker (RD-Verbindungsbroker) müssen für hohe Verfügbarkeit zur Unterstützung der Migration konfiguriert werden. Weitere Informationen finden Sie unter [Bereitstellen eines Remotedesktop-Verbindungsbroker-Clusters](Deploy-a-Remote-Desktop-Connection-Broker-cluster.md).

1. Sind mehrere RD-Verbindungsbrokerserver mit hoher Verfügbarkeit eingerichtet, entfernen Sie alle RD-Verbindungsbrokerserver mit Ausnahme des derzeit aktiven Servers.

2. [Aktualisieren Sie](upgrade-to-rds-2016.md) die übrigen RD-Verbindungsbroker-Server in der Bereitstellung auf Windows Server 2016.

3. Remotedesktop-Verbindungsbroker von Windows Server 2016-Server in der Bereitstellung mit hoher Verfügbarkeit hinzufügen.

> [!NOTE] 
> Eine Mischkonfiguration für hohe Verfügbarkeit-Konfiguration mit Windows Server 2016 und Windows Server 2012 R2 wird für RD-Verbindungsbrokerserver nicht unterstützt. Ein RD Connection Broker, die unter Windows Server 2016 kann für sitzungssammlungen mit RD-Sitzungshostservern unter Windows Server 2012 R2, und Sammlungen virtuelle Desktops mit RD-virtualisierungshostservern unter Windows Server 2012 R2 dienen.

## <a name="migrate-session-collections"></a>Migrieren von Sitzungssammlungen

Um einer sitzungssammlung in Windows Server 2012 R2 zu einer sitzungssammlung in Windows Server 2016 zu migrieren, gehen Sie wie folgt vor.

> [!IMPORTANT]
> Migrieren von sitzungssammlungen erst nach Abschluss des vorhergehenden Schritts, [Migrieren von RD-Verbindungsbrokerserver](#migrate-rdconnection-broker-servers).

1. [Aktualisieren Sie die sitzungssammlung](Upgrade-to-RDSH-2016.md) von Windows Server 2012 R2 auf Windows Server 2016.

2. Fügen Sie den neuen RD-Sitzungshost-Server, die mit Windows Server 2016 zur sitzungssammlung hinzu.

3. Melden Sie sich bei allen Sitzungen auf den RD-Sitzungshostservern ab, und entfernen Sie die Server, für die eine Migration erforderlich ist, aus der Sitzungssammlung.

   > [!NOTE]
   > Falls die UVHD-Vorlage (UVHD-template.vhdx) in der sitzungssammlung aktiviert ist, und der Dateiserver zu einem neuen Server migriert wurde, aktualisieren Sie die Benutzerprofil-Datenträger: Speicherort der Auflistungseigenschaft mit dem neuen Pfad. Die Benutzerprofil-Datenträger müssen am neuen Speicherort unter dem gleichen relativen Pfad wie auf dem Quellserver zur Verfügung stehen.
   >
   > Eine sitzungssammlung aus RD-Sitzungshostservern mit einer Mischung aus Servern unter Windows Server 2012 R2 und Windows Server 2016 wird nicht unterstützt.

## <a name="migrate-virtual-desktop-collections"></a>Migrieren von Sammlungen virtueller Desktops

Um einer Sammlung virtueller Desktops von einem Quellserver unter Windows Server 2012 R2 zu einem Zielserver unter Windows Server 2016 zu migrieren, gehen Sie wie folgt vor.

> [!IMPORTANT]
> Migrieren von Sammlungen virtueller Desktops erst nach Abschluss des vorhergehenden Schritts, [Migrieren von RD-Verbindungsbrokerserver](#migrate-rdconnection-broker-servers).

1. [Aktualisieren den Sammlung virtuellen Desktops](Upgrade-to-RDVH-2016.md) vom Server ausgeführt wird in Windows Server 2012 R2 auf Windows Server 2016.

2. Fügen Sie die neuen RD-Virtualisierungshost von Windows Server 2016-Server, auf der Sammlung virtueller Desktops.

3. Migrieren Sie alle virtuellen Computer in der aktuellen Sammlung virtueller Desktops, die auf RD-Virtualisierungshostservern ausgeführt werden, zu den neuen Servern.

4. Entfernen Sie alle RD-Virtualisierungshostserver, für die die Migration erforderlich war, aus der Sammlung virtueller Desktops auf dem Quellserver.

> [!NOTE]
> Falls die UVHD-Vorlage (UVHD-template.vhdx) in der sitzungssammlung aktiviert ist, und der Dateiserver zu einem neuen Server migriert wurde, aktualisieren Sie die Benutzerprofil-Datenträger: Speicherort der Auflistungseigenschaft mit dem neuen Pfad. Die Benutzerprofil-Datenträger müssen am neuen Speicherort unter dem gleichen relativen Pfad wie auf dem Quellserver zur Verfügung stehen.
>
> Ein Sammlung virtueller Desktops der Remotedesktop-Virtualisierungshostserver mit einer Mischung aus Servern unter Windows Server 2012 R2 und Windows Server 2016 wird nicht unterstützt.

## <a name="migrate-rdweb-access-servers"></a>Migrieren von Servern mit Web Access für Remotedesktop

Um das Migrieren der Server mit Web Access für Remotedesktop, gehen Sie wie folgt vor:

- Einbinden Sie der Zielserver unter Windows Server 2016 mit der Remotedesktopdienste-Bereitstellung, und installieren Sie die RD-Web-Rolle

- Verwendung [IIS Web Deploy-Tool](https://www.iis.net/) zum Migrieren von Einstellungen für die RD-Web-Website von der aktuellen Web Access für Remotedesktop-Server auf dem Zielserver unter Windows Server 2016.

- [Migrieren von Zertifikaten](#migrate-certificates) auf dem Zielserver Windows Server 2016 ausgeführt.

- Entfernen Sie den Quellserver aus der Remote Desktop Services-Bereitstellung.

## <a name="migrate-rdgateway-servers"></a>Migrieren von Remotedesktop-Gatewayservern

Um die Migration des Remotedesktop-Gatewayservern, gehen Sie wie folgt vor:

- Einbinden Sie der Zielserver unter Windows Server 2016 mit der Remotedesktopdienste-Bereitstellung, und installieren Sie die RD-Gateway-Rolle

- Verwendung [IIS Web Deploy-Tool](https://www.iis.net/) die endpunkteinstellungen des RD-Gateway aus der aktuellen RD-Gatewayserver auf dem Zielserver unter Windows Server 2016 zu migrieren.

- [Migrieren von Zertifikaten](#migrate-certificates) auf dem Zielserver Windows Server 2016 ausgeführt.

- Entfernen Sie den Quellserver aus der Remote Desktop Services-Bereitstellung.

## <a name="migrate-rdlicensing-servers"></a>Migrieren von Remotedesktop-Lizenzierungsservern

Führen Sie diese Schritte zum Migrieren eines RD-Lizenzierungsservers von einem Quellserver unter Windows Server 2012 oder Windows Server 2012 R2 zu einem Zielserver unter Windows Server 2016.

1. [Migrieren der Remotedesktopdienste-Clientzugriffslizenzen (TS CALs)](migrate-rds-cals.md) vom Quellserver zum Zielserver.

2. Bearbeiten der **Bereitstellungseigenschaften** in **Server-Manager** auf dem Remotedesktop-Server (die in der Regel auf dem ersten RD Connection Broker Server ausgeführt wird), enthalten nur die neuen RD-Lizenzierung Server unter Windows Server 2016.

3. Deaktivieren Sie das RD-lizenzierungsquellserver: In **Remotedesktoplizenzierungs-Manager**mit der rechten Maustaste auf den entsprechenden Server, zeigen Sie auf **erweitert** auszuwählenden **Server deaktivieren**, und klicken Sie dann die Schritte im Assistenten .

4. Entfernen Sie die RD-lizenzierungsquellserver aus der Bereitstellung in **Server-Manager** auf dem Remotedesktop-Server.

## <a name="migrate-certificates"></a>Migrieren von Zertifikaten

Erfolgreiche Certificate Migration ist den tatsächlichen Prozess Migrieren von Zertifikaten und zum Aktualisieren der Zertifikatsinformationen in den Bereitstellungseigenschaften der Remote Desktop Services erforderlich.

Typische Certificate Migration umfasst die folgenden Schritte aus:

- Exportieren Sie das Zertifikat in eine PFX-Datei mit dem privaten Schlüssel.

- Importieren Sie das Zertifikat aus einer PFX-Datei.

Aktualisieren Sie nach der Migration die entsprechenden Zertifikate die folgenden erforderlichen Zertifikate für die Remotedesktopdienste-Bereitstellung im Server-Manager oder PowerShell ein:

- RD Connection Broker - SSO

- Remotedesktop-Verbindungsbroker - RDP-Datei veröffentlichen

- RD-Gateway - HTTPS-Verbindung

- Web Access für Remotedesktop - HTTPS-Verbindung und Abonnement von RemoteApp/Desktop-Verbindung

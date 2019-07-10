---
title: Migrieren von Remotedesktopdienste-Bereitstellungen zu Windows Server 2016
description: In diesem Artikel wird beschrieben, wie eine Remotedesktopdienste-Bereitstellung zu neuen Windows Server 2016-Servern migriert wird.
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
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "66812584"
---
# <a name="migrate-your-remote-desktop-services-deployment-to-windows-server-2016"></a>Migrieren von Remotedesktopdienste-Bereitstellungen zu Windows Server 2016

Wenn du die Remotedesktopdienste (Remote Desktop Services, RDS) zurzeit in Windows Server 2012 R2 ausführst, kannst du zu Windows Server 2016 wechseln, um von neuen Features wie der Unterstützung für Azure SQL und direkten Speicherplätzen zu profitieren.

Die Migration einer Bereitstellung der Remotedesktopdienste wird von Quellservern unter Windows Server 2016 zu Zielservern unter Windows Server 2016 unterstützt. Anders gesagt: Es gibt keine direkte Migration der Remotedesktopdienste von Windows Server 2012 R2 zu Windows Server 2016. Stattdessen führst du für die meisten RDS-Komponenten zunächst ein Upgrade auf Windows Server 2016 aus und migrierst dann die Daten und Lizenzen. Die einzigen Komponenten, die direkt migriert werden können, sind RD-Web, RD-Gateway und der Lizenzierungsserver.

Weitere Informationen zum Upgradeprozess und den Anforderungen findest du unter [Aktualisieren der Remotedesktopdienste-Bereitstellungen auf Windows Server 2016](upgrade-to-rds-2016.md).

Mit den folgenden Schritten kannst du deine Remotedesktopdienste-Bereitstellung migrieren:

- [Migrieren von Remotedesktop-Verbindungsbrokerservern](#migrate-rdconnection-broker-servers)

- [Migrieren von Sitzungssammlungen](#migrate-session-collections)

- [Migrieren von Sammlungen virtueller Desktops](#migrate-virtual-desktop-collections)

- [Migrieren von RD-Webzugriffsservern](#migrate-rdweb-access-servers)

- [Migrieren von Remotedesktop-Gatewayservern](#migrate-rdgateway-servers)

- [Migrieren von Remotedesktop-Lizenzierungsservern](#migrate-rdgateway-servers)

- [Migrieren von Zertifikaten](#migrate-certificates)

## <a name="migrate-rdconnection-broker-servers"></a>Migrieren von Remotedesktop-Verbindungsbrokerservern

Dies ist der erste und wichtigste Schritte bei der Migration deines Remotedesktop-Verbindungsbrokers auf Zielservern unter Windows Server 2016.

> [!IMPORTANT]
> Die Quellserver des Remotedesktop-Verbindungsbrokers (RD-Verbindungsbroker) müssen für hohe Verfügbarkeit konfiguriert sein, damit die Migration unterstützt wird. Weitere Informationen findest du unter [Bereitstellen eines Remotedesktop-Verbindungsbrokerclusters](Deploy-a-Remote-Desktop-Connection-Broker-cluster.md).

1. Sind mehrere RD-Verbindungsbrokerserver mit hoher Verfügbarkeit eingerichtet, entfernen Sie alle RD-Verbindungsbrokerserver mit Ausnahme des derzeit aktiven Servers.

2. Führe für die übrigen Remotedesktop-Verbindungsbrokerserver in der Bereitstellung ein [Upgrade](upgrade-to-rds-2016.md) auf Windows Server 2016 durch.

3. Füge Windows Server 2016-RD-Verbindungsbrokerserver in der Hochverfügbarkeitsbereitstellung hinzu.

> [!NOTE] 
> Eine Mischkonfiguration für hohe Verfügbarkeit mit Windows Server 2016 und Windows Server 2012 R2 wird für RD-Verbindungsbrokerserver nicht unterstützt. Ein RD-Verbindungsbroker unter Windows Server 2016 kann für Sitzungssammlungen mit RD-Sitzungshostservern unter Windows Server 2012 R2 und für Sammlungen virtueller Desktops mit RD-Virtualisierungshostservern unter Windows Server 2012 R2 verwendet werden.

## <a name="migrate-session-collections"></a>Migrieren von Sitzungssammlungen

Führe zum Migrieren einer Sitzungssammlung in Windows Server 2012 R2 zu einer Sitzungssammlung in Windows Server 2016 die folgenden Schritte aus.

> [!IMPORTANT]
> Migriere die Sitzungssammlungen erst nach erfolgreicher Ausführung des vorigen Schritts [Migrieren von Remotedesktop-Verbindungsbrokerservern](#migrate-rdconnection-broker-servers).

1. [Führe ein Upgrade der Sitzungssammlung](Upgrade-to-RDSH-2016.md) von Windows Server 2012 R2 auf Windows Server 2016 aus.

2. Füge den neuen RD-Sitzungshostserver unter Windows Server 2016 zur Sitzungssammlung hinzu.

3. Melden Sie sich bei allen Sitzungen auf den RD-Sitzungshostservern ab, und entfernen Sie die Server, für die eine Migration erforderlich ist, aus der Sitzungssammlung.

   > [!NOTE]
   > Falls die UVHD-Vorlage (UVHD-template.vhdx) in der Sitzungssammlung aktiviert ist und der Dateiserver zu einem neuen Server migriert wurde, aktualisiere die Sammlungseigenschaft „Benutzerprofil-Datenträger: Speicherort“ mit dem neuen Pfad. Die Benutzerprofil-Datenträger müssen am neuen Speicherort unter dem gleichen relativen Pfad wie auf dem Quellserver zur Verfügung stehen.
   >
   > Eine Sitzungssammlung aus RD-Sitzungshostservern mit einer Mischung aus Servern unter Windows Server 2012 R2 und Windows Server 2016 wird nicht unterstützt.

## <a name="migrate-virtual-desktop-collections"></a>Migrieren von Sammlungen virtueller Desktops

Führe zum Migrieren einer Sammlung virtueller Desktops von einem Quellserver unter Windows Server 2012 R2 zu einem Zielserver unter Windows Server 2016 die folgenden Schritte aus.

> [!IMPORTANT]
> Migriere die Sammlungen virtueller Desktops erst nach erfolgreicher Ausführung des vorigen Schritts [Migrieren von Remotedesktop-Verbindungsbrokerservern](#migrate-rdconnection-broker-servers).

1. [Führe ein Upgrade der Sammlung virtueller Desktops](Upgrade-to-RDVH-2016.md) von Windows Server 2012 R2 auf Windows Server 2016 aus.

2. Füge die neuen Windows Server 2016-RD-Virtualisierungshostserver zur Sammlung virtueller Desktops hinzu.

3. Migrieren Sie alle virtuellen Computer in der aktuellen Sammlung virtueller Desktops, die auf RD-Virtualisierungshostservern ausgeführt werden, zu den neuen Servern.

4. Entfernen Sie alle RD-Virtualisierungshostserver, für die die Migration erforderlich war, aus der Sammlung virtueller Desktops auf dem Quellserver.

> [!NOTE]
> Falls die UVHD-Vorlage (UVHD-template.vhdx) in der Sitzungssammlung aktiviert ist und der Dateiserver zu einem neuen Server migriert wurde, aktualisiere die Sammlungseigenschaft „Benutzerprofil-Datenträger: Speicherort“ mit dem neuen Pfad. Die Benutzerprofil-Datenträger müssen am neuen Speicherort unter dem gleichen relativen Pfad wie auf dem Quellserver zur Verfügung stehen.
>
> Eine Sammlung virtueller Desktops aus RD-Virtualisierungshostservern mit einer Mischung aus Servern unter Windows Server 2012 R2 und Windows Server 2016 wird nicht unterstützt.

## <a name="migrate-rdweb-access-servers"></a>Migrieren von Servern mit Web Access für Remotedesktop

Führe die folgenden Schritte aus, um RD-Webzugriffsserver zu migrieren:

- Füge die Zielserver unter Windows Server 2016 zur Remotedesktopdienste-Bereitstellung hinzu, und installiere die RD-Webrolle.

- Verwende das [IIS-Webbereitstellungstool](https://www.iis.net/), um die Websiteeinstellungen für RD-Web von den derzeitigen RD-Webzugriffsservern zu den Zielservern unter Windows Server 2016 zu migrieren.

- [Migriere Zertifikate](#migrate-certificates) zu den Zielservern unter Windows Server 2016.

- Entferne die Quellserver aus der Remotedesktopdienste-Bereitstellung.

## <a name="migrate-rdgateway-servers"></a>Migrieren von Remotedesktop-Gatewayservern

Führe die folgenden Schritte aus, um RD-Gatewayserver zu migrieren:

- Füge die Zielserver unter Windows Server 2016 zur Remotedesktopdienste-Bereitstellung hinzu, und installiere die RD-Gatewayrolle.

- Verwende das [IIS-Webbereitstellungstool](https://www.iis.net/), um die Endpunkteinstellungen für das RD-Gateway von den derzeitigen RD-Gatewayservern zu den Zielservern unter Windows Server 2016 zu migrieren.

- [Migriere Zertifikate](#migrate-certificates) zu den Zielservern unter Windows Server 2016.

- Entferne die Quellserver aus der Remotedesktopdienste-Bereitstellung.

## <a name="migrate-rdlicensing-servers"></a>Migrieren von Remotedesktop-Lizenzierungsservern

Führe zum Migrieren eines RD-Lizenzierungsservers von einem Quellserver unter Windows Server 2012 oder Windows Server 2012 R2 zu einem Zielserver unter Windows Server 2016 die folgenden Schritte aus.

1. [Migriere die Clientzugriffslizenzen für Remotedesktopdienste (RDS-CALs)](migrate-rds-cals.md) vom Quellserver zum Zielserver.

2. Bearbeite die **Bereitstellungseigenschaften** im **Server-Manager** auf dem Remotedesktop-Verwaltungsserver (der in der Regel auf dem ersten RD-Verbindungsbrokerserver ausgeführt wird), sodass nur die neuen RD-Lizenzierungsserver unter Windows Server 2016 enthalten sind.

3. Deaktiviere den RD-Lizenzierungsquellserver: Klicke im **Remotedesktoplizenzierungs-Manager** mit der rechten Maustaste auf den entsprechenden Server, zeige auf **Erweitert**, um **Server deaktivieren** auszuwählen, und führe dann die Schritte des Assistenten aus.

4. Entferne die RD-Lizenzierungsquellserver im **Server-Manager** auf dem Remotedesktop-Verwaltungsserver aus der Bereitstellung.

## <a name="migrate-certificates"></a>Migrieren von Zertifikaten

Für eine erfolgreiche Zertifikatmigration ist sowohl der tatsächliche Prozess der Migration von Zertifikaten als auch das Aktualisieren der Zertifikatinformationen in den Eigenschaften der Remotedesktopdienste-Bereitstellung erforderlich.

Die Zertifikatmigration umfasst in der Regel die folgenden Schritte:

- Exportiere das Zertifikat mit dem privaten Schlüssel in eine PFX-Datei.

- Importiere das Zertifikat aus einer PFX-Datei.

Aktualisiere nach der Migration des entsprechenden Zertifikats die folgenden erforderlichen Zertifikate für die Remotedesktopdienste-Bereitstellung im Server-Manager oder in PowerShell:

- RD-Verbindungsbroker – einmaliges Anmelden

- RD-Verbindungsbroker – Veröffentlichen der RDP-Datei

- RD-Gateway – HTTPS-Verbindung

- RD-Webzugriff – HTTPS-Verbindung und Abonnement für RemoteApp/Desktopverbindung

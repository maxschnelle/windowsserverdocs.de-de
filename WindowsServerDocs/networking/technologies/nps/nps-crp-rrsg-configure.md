---
title: Konfigurieren von RADIUS-Remoteservergruppen
description: Dieses Thema enthält Informationen zum Konfigurieren von RADIUS-Remoteservergruppen im Netzwerkrichtlinienserver unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ca125e57-249c-4d97-85d1-2929cbf871f1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 02088a35196c0bfadeb65e8971a47fdcc741258d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818761"
---
# <a name="configure-remote-radius-server-groups"></a>Konfigurieren von RADIUS-Remoteservergruppen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um RADIUS-Remoteservergruppen konfigurieren, wenn Sie NPS, fungiert als Proxy-Server und Weiterleiten von verbindungsanforderungen an andere NPSs für die Verarbeitung konfigurieren möchten.

## <a name="add-a-remote-radius-server-group"></a>Fügen Sie eine Remote-RADIUS-Servergruppe hinzu.

Sie können dieses Verfahren verwenden, in das Windows-Verwaltungsinstrumentation (Network Policy Server, NPS)-Snap-in einer neuen RADIUS-Remoteservergruppe hinzu.

Wenn Sie NPS als RADIUS-Proxy konfigurieren, erstellen Sie eine neue Verbindungsanforderungsrichtlinie, die NPS verwendet, um zu bestimmen, welche verbindungsanforderungen an andere RADIUS-Server weitergeleitet. Darüber hinaus wird die Verbindungsanforderungsrichtlinie konfiguriert, durch Angeben einer RADIUS-Remoteservergruppe, die eine oder mehrere RADIUS-Server enthält die NPS anweist, wohin die Weiterleitung von verbindungsanforderungen gesendet, die die Verbindungsanforderungsrichtlinie entsprechen.

>[!NOTE]
>Sie können auch eine neue RADIUS-Remoteservergruppe während des Prozesses zum Erstellen einer neuen Verbindungsanforderungsrichtlinie konfigurieren.

Grundvoraussetzung für die Ausführung dieses Vorgangs ist die Mitgliedschaft in **Domänen-Admins** oder einer gleichwertigen Gruppe.

### <a name="to-add-a-remote-radius-server-group"></a>Eine remote-RADIUS-Servergruppe hinzufügen 

1. Klicken Sie im Server-Manager **Tools**, und klicken Sie dann auf **Network Policy Server** die NPS-Konsole zu öffnen.
2. Doppelklicken Sie in der Konsolenstruktur auf **RADIUS-Clients und Servern**, mit der rechten Maustaste **RADIUS-Remoteservergruppen**, und klicken Sie dann auf **neu**.
3. Die **Neuer RADIUS-Remoteservergruppe** Dialogfeld wird geöffnet. In **Gruppenname**, geben Sie einen Namen für die remote-RADIUS-Servergruppe.
4. **In der RADIUS-Servern**, klicken Sie auf **hinzufügen**. Die **RADIUS-Server hinzufügen** Dialogfeld wird geöffnet. Geben Sie die IP-Adresse des RADIUS-Servers, die Sie der Gruppe hinzufügen möchten, oder geben Sie den vollständig qualifizierten Domänennamen \(FQDN\) der RADIUS-Server, und klicken Sie dann auf **überprüfen**.
5. Klicken Sie im Dialogfeld **RADIUS-Server hinzufügen** auf die Registerkarte **Authentifizierung/Kontoführung**. In **gemeinsamer geheimer Schlüssel** und **gemeinsamen geheimen Schlüssel bestätigen**, geben Sie den gemeinsamen geheimen Schlüssel. Sie müssen den gleichen gemeinsamen geheimen Schlüssel verwenden, wenn Sie den lokalen Computer als RADIUS-Client auf dem RADIUS-Remoteserver konfigurieren.
6. Wenn Sie Extensible Authentication Protocol (EAP) für die Authentifizierung nicht verwenden, klicken Sie auf **Anforderung darf die Authenticator-Nachrichtenattribut**. EAP Nachrichtenauthentifizierung Attributs wird standardmäßig verwendet.
7. Stellen Sie sicher, dass die Authentifizierung und-Kontoführung Portnummern für die Bereitstellung richtig sind.
8. Bei Verwendung von einer anderen gemeinsamen geheimen Schlüssel für die Kontoführung, im **Buchhaltung**Deaktivieren der **verwenden den gleichen gemeinsamen geheimen Schlüssel für die Authentifizierung und Kontoführung** Kontrollkästchen, und geben Sie das gemeinsame Geheimnis der Buchhaltung in  **Gemeinsamer geheimer Schlüssel** und **gemeinsamen geheimen Schlüssel bestätigen**.
9. Wenn Sie nicht möchten, zum Weiterleiten von Network Access Server starten und beenden-Meldungen an den RADIUS-Remoteserver, deaktivieren die **weiterleiten Network Access Server starten und Beenden von Benachrichtigungen an diesen Server** Kontrollkästchen.

Weitere Informationen zum Verwalten von NPS finden Sie unter [Verwalten des Netzwerkrichtlinienservers](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).


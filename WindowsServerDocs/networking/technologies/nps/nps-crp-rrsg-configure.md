---
title: Konfigurieren von RADIUS-Remoteservergruppen
description: Dieses Thema enthält Informationen zum Konfigurieren von RADIUS-Remoteservergruppen im Netzwerkrichtlinienserver in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ca125e57-249c-4d97-85d1-2929cbf871f1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f293fd18176115365e5e243a90a034676b3262f9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-remote-radius-server-groups"></a>Konfigurieren von RADIUS-Remoteservergruppen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie die RADIUS-Remoteservergruppen konfigurieren, wenn Sie NPS als einen Proxyserver und Vorwärts verbindungsanforderungen an andere NPS-Server für die Verarbeitung fungieren konfigurieren möchten.

## <a name="add-a-remote-radius-server-group"></a>Fügen Sie eine Remote-RADIUS-Remoteservergruppe hinzu

Dieses Verfahrens können eine neue RADIUS-Remoteservergruppe in der Netzwerkrichtlinienserver (Network Policy Server, NPS)-Snap-in hinzu.

Wenn Sie NPS als RADIUS-Proxy konfigurieren, erstellen Sie eine neue Verbindungsanforderungsrichtlinie, die NPS verwendet, um zu bestimmen, welche verbindungsanforderungen an andere RADIUS-Server weiterleiten. Darüber hinaus wird die Verbindungsanforderungsrichtlinie konfiguriert, durch die Angabe einer RADIUS-Remoteservergruppe, die einen oder mehrere RADIUS-Server, enthält, die NPS darüber informiert werden, wo Sie die verbindungsanforderungen zu senden, die die Verbindungsanforderungsrichtlinie entsprechen.

>[!NOTE]
>Sie können auch eine neue RADIUS-Remoteservergruppe während der Erstellung einer neuen Verbindungsanforderungsrichtlinie konfigurieren.

Mitgliedschaft in **Domänen-Admins**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.

### <a name="to-add-a-remote-radius-server-group"></a>So fügen Sie einen RADIUS-Remoteservergruppe hinzu 

1. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver** die NPS-Konsole zu öffnen.
2. Doppelklicken Sie in der Konsolenstruktur auf **RADIUS-Clients und Servern**, mit der rechten Maustaste **RADIUS-Remoteservergruppen**, und klicken Sie dann auf **neu**.
3. Die **Neuer RADIUS-Remoteservergruppe** Dialogfeld wird geöffnet. In **Gruppenname**, geben Sie einen Namen für die RADIUS-Remoteservergruppe.
4. **In der RADIUS-Server**, klicken Sie auf **hinzufügen**. Die **RADIUS-Server hinzufügen** Dialogfeld wird geöffnet. Geben Sie die IP-Adresse des RADIUS-Servers, die Sie verwenden möchten, fügen der Gruppe oder geben Sie den vollqualifizierten Domänennamen \(FQDN\) des RADIUS-Servers, und klicken Sie dann auf **überprüfen, ob**.
5. In **RADIUS-Server hinzufügen**, klicken Sie auf die **Authentifizierung/Kontoführung** Registerkarte. In **gemeinsamer geheimer Schlüssel** und **gemeinsamen geheimen Schlüssel bestätigen**, geben Sie den gemeinsamen geheimen Schlüssel. Sie müssen den gleichen gemeinsamen geheimen Schlüssel verwenden, wenn Sie den lokalen Computer als RADIUS-Client auf dem remote-RADIUS-Server konfigurieren.
6. Wenn Sie nicht Extensible Authentication Protocol (EAP) für die Authentifizierung verwenden, klicken Sie auf **Anforderung muss das Attribut Message Authenticator enthalten**. EAP wird standardmäßig der Nachrichtenauthentifizierung Attribut verwendet.
7. Stellen Sie sicher, dass die Authentifizierung und-Kontoführung Portnummern für die Bereitstellung richtig sind.
8. Wenn Sie einen anderen gemeinsamen geheimen Schlüssel für die Kontoführung, verwenden Sie in **Kontoführung**Kontrollkästchen die **verwenden den gleichen gemeinsamen geheimen Schlüssel für die Authentifizierung und-Kontoführung** Kontrollkästchen, und geben Sie in der Buchhaltung-geheime **gemeinsamer geheimer Schlüssel** und **gemeinsamen geheimen Schlüssel bestätigen**.
9. Wenn Sie nicht möchten, zum Weiterleiten von Network Access Server starten und beenden Nachrichten mit dem RADIUS-Remoteserver, deaktivieren die **weiterleiten Network Access Server starten und Beenden von Benachrichtigungen an diesen Server** Kontrollkästchen.

Weitere Informationen zum Verwalten von NPS finden Sie unter [Netzwerkrichtlinienserver verwalten](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).


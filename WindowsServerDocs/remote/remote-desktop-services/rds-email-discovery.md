---
title: Einrichten von e-Mail-Discovery, um Ihre RDS-feed zu abonnieren
description: Informationen Sie zum Integrieren von Azure Active Directory-Domänendienste in Ihre RDS-Bereitstellung.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 3/27/2018
ms.localizationpriority: medium
ms.topic: article
author: christianmontoya
ms.openlocfilehash: 5b3f162b8eee70fbc452b7400b737454c3fffb59
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2018
ms.locfileid: "1691669"
---
# <a name="set-up-email-discovery-to-subscribe-to-your-rds-feed"></a>Einrichten von e-Mail-Discovery, um Ihre RDS-feed zu abonnieren

Haben Sie schon einmal bereitet die Endbenutzer mit ihrer veröffentlichten RDS-feed, entweder aufgrund eines fehlenden Zeichens in den Feed verbunden URL oder da sie die e-Mail mit dem URL verloren? Nahezu alle Remotedesktop-Clientanwendungen unterstützt suchen Ihr Abonnement, indem Sie Ihre e-Mail-Adresse, leicht einfacher denn je, erhalten Benutzer an ihre RemoteApps und Desktops angeschlossen eingeben.

>[!IMPORTANT]
>Die Microsoft Remote Desktop-app in den Microsoft Store unterstützt e-Mail-Adresse Abonnement zu diesem Zeitpunkt nicht.

Vor dem Einrichten von e-Mail-Discovery, folgendermaßen Sie vor:

- Stellen Sie sicher, dass Sie über die Berechtigung zum Hinzufügen eines TXT-Eintrags auf die Domäne, die Ihre e-Mail-Adresse zugeordnet (z. B., wenn die Benutzer haben @contoso.com e-Mail-Adressen, benötigen Sie Berechtigungen für die Domäne "contoso.com")
- Erstellen Sie eine feed-URL RD-Website (https://\ < Rdweb-Dns-Name\ >.domain/RDWeb/Feed/webfeed.aspx, wie etwahttps://rdweb.contoso.com/RDWeb/Feed/webfeed.aspx)

Nun, verwenden Sie diese Schritte zum Einrichten von e-Mail-Erkennung:

1. In Ihrem Browser eine Verbindung mit der Website der Registrierungsstelle für Domänennamen, in Ihrer Domäne registriert ist.
2. Navigieren Sie zu der entsprechenden Seite für Ihre registrierte Domäne, in dem Sie anzeigen, hinzufügen und Bearbeiten von DNS-Einträgen.
3. Geben Sie einen neuen DNS-Datensatz mit den folgenden Eigenschaften:
   - **Host:** _msradc
   - **Text:** \ < RD Web Feed URL\ >
   - **TTL:** 300

   Die Namen der DNS-Datensätze Felder variieren je nach der Registrierungsstelle für Domänennamen, aber dieser Prozess, mit dem Namen _msradc. TXT-Eintrag bewirken \ < lautet > (beispielsweise _msradc.contoso.com), die einen Wert des vollständigen RD Web Feeds hat.

Das wars! Nun, starten Sie die Anwendung Remote Desktop auf Ihrem Gerät und sich selbst!
---
title: Einrichten von e-Mail-Ermittlung Ihre RDS-feed abonnieren
description: Erfahren Sie, wie Sie Azure AD Domain Services in Ihre RDS-Bereitstellung integrieren.
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 3/27/2018
ms.localizationpriority: medium
ms.topic: article
author: christianmontoya
ms.openlocfilehash: 5b3f162b8eee70fbc452b7400b737454c3fffb59
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878321"
---
# <a name="set-up-email-discovery-to-subscribe-to-your-rds-feed"></a>Einrichten von e-Mail-Ermittlung Ihre RDS-feed abonnieren

Mussten Sie jemals schwierigkeiten, die Ihre Endbenutzer mit ihren veröffentlichten RDS-feed, entweder aufgrund fehlender Einzelzeichen im Feed verbunden URL oder weil sie die e-Mail-Adresse mit der URL verloren gehen? Fast alle Remotedesktop-Client-Anwendungen unterstützen, finden Ihr Abonnement durch Eingabe Ihrer e-Mail-Adresse, die einfacher als je zuvor, erhalten Ihre Benutzer, die mit ihren RemoteApps und Desktops verbunden sind.

>[!IMPORTANT]
>Die Microsoft-Remotedesktop-app in den Microsoft Store-unterstützt Abonnement von e-Mail-Adresse zu diesem Zeitpunkt nicht.

Bevor Sie die Ermittlung von e-Mail-Adresse eingerichtet haben, führen Sie folgende Schritte aus:

- Stellen Sie sicher, dass Sie die Berechtigung zum Hinzufügen eines TXT-Eintrags in die Domäne Ihrer e-Mail-Adresse zugeordnet haben (z. B., wenn Ihre Benutzer @contoso.com e-Mail-Adressen, benötigen Sie Berechtigungen für die Domäne "contoso.com")
- Erstellen Sie eine RD-Web-feed-URL (https://\<Rdweb-Dns-Name\>.domain/RDWeb/Feed/webfeed.aspx, z. B. https://rdweb.contoso.com/RDWeb/Feed/webfeed.aspx)

Verwenden Sie nun diese Schritte zum Einrichten von e-Mail-Ermittlung:

1. Verbinden Sie in Ihrem Browser mit der Website der Domänennamen-Registrierungsstelle, in dem Ihre Domäne registriert ist.
2. Navigieren Sie zu der entsprechenden Seite für die registrierte Domäne, in dem Sie anzeigen, hinzufügen und Bearbeiten von DNS-Einträge können.
3. Geben Sie einen neuen DNS-Datensatz mit den folgenden Eigenschaften:
   - **Host:** _msradc
   - **Text:** \<RD-Web-Feed-URL\>
   - **TTL:** 300

   Die Namen der DNS-Datensätze Felder variieren von Domänennamen-Registrierungsstelle, aber dieser Vorgang führt zu einer TXT-Eintrag mit dem Namen _msradc. \<Domain_name\> (z. B. _msradc.contoso.com), die mit dem Wert des vollständigen RD-Web-Feeds.

Das war schon alles! Jetzt starten Sie die Remote Desktop-Anwendung auf Ihrem Gerät, und abonnieren Sie selbst!
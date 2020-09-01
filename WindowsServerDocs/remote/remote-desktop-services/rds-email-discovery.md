---
title: Einrichten der E-Mail-Erkennung zum Abonnieren deines RDS-Feeds
description: Erfahren Sie, wie Sie die E-Mail-Erkennung in Ihrer RDS-Bereitstellung einrichten.
ms.author: chrimo
ms.date: 8/28/2020
ms.localizationpriority: medium
ms.topic: article
author: christianmontoya
ms.openlocfilehash: 71b892d95b15f02445ec7898a6c57f931bc4b501
ms.sourcegitcommit: 2b1a12c85acff137e5ac84cd0e62d8353fcdde31
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89087463"
---
# <a name="set-up-email-discovery-to-subscribe-to-your-rds-feed"></a>Einrichten der E-Mail-Erkennung zum Abonnieren deines RDS-Feeds

Hattest du jemals Schwierigkeiten, für deine Endbenutzer eine Verbindung mit dem veröffentlichten RDS-Feed herzustellen, weil entweder in der Feed-URL ein einzelner Buchstabe gefehlt hat oder weil die E-Mail mit der URL verloren gegangen ist? Nahezu alle Remotedesktop-Clientanwendungen unterstützen die Suche nach deinem Abonnement durch Eingabe deiner E-Mail-Adresse. So kannst du deine Endbenutzer leichter als je zuvor mit ihren RemoteApps und Desktops verbinden.

Führe vor dem Einrichten der E-Mail-Erkennung die folgenden Schritte aus:

- Vergewissere dich, dass du über Berechtigungen zum Hinzufügen eines TXT-Eintrags zu der mit deiner E-Mail verknüpften Domäne verfügst. (Beispiel: Wenn deine Benutzer E-Mail-Adressen vom Typ @contoso.com besitzen, benötigst du Berechtigungen für die Domäne „contoso.com“.)
- Erstellen Sie eine RD-Feed-URL („https://\<rdweb-dns-name\>.domain/RDWeb/Feed/webfeed.aspx“, z. B. https://rdweb.contoso.com/RDWeb/Feed/webfeed.aspx).

>[!NOTE]
>Wenn Sie Windows Virtual Desktop anstelle des Remotedesktops verwenden, sollten Sie stattdessen diese URLs verwenden:
>
>- Wenn Sie Windows Virtual Desktop (klassisch) verwenden: <https://rdweb.wvd.microsoft.com/api/feeddiscovery/webfedddiscovery.aspx>
>- Wenn Sie Windows Virtual Desktop verwenden: <https://rdweb.wvd.microsoft.com/api/arm/feeddiscovery>

Führen Sie nun die folgenden Schritte zum Einrichten der E-Mail-Erkennung aus:

1. Öffne im Browser die Website der Domänennamen-Registrierungsstelle, bei der deine Domäne registriert ist.
2. Navigiere zur entsprechenden Seite für deine registrierte Domäne, auf der du DNS-Einträge anzeigen, hinzufügen und bearbeiten kannst.
3. Gib einen neuen DNS-Eintrag mit den folgenden Eigenschaften ein:
   - **Host:** _msradc
   - **Text:** \<RD Web Feed URL\>
   - **TTL:** 300

   Die Namen der Felder für DNS-Einträge variieren je nach Domänennamen-Registrierungsstelle, mit diesen Schritten erhalten Sie jedoch einen TXT-Eintrag namens „_msradc.\<domain_name\> (z. B. „_msradc.contoso.com“) mit einem Wert des vollständigen RD-Feeds.

Das war's. Starte jetzt die Remotedesktopanwendung auf deinem Gerät, und abonniere deinen eigenen Feed!
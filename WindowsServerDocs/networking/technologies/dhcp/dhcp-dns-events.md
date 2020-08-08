---
title: DHCP-Protokollierungs Ereignisse für DNS-Daten Satz Registrierungen
description: Dieses Thema enthält Informationen zu DHCP-Server Protokollierungs Ereignissen in Windows Server 2016.
manager: brianlic
ms.topic: get-started-article
ms.assetid: beb8c188-6fcf-4520-8825-d17f8ee9fb04
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 6dd02ff590c3b616f60ed095d55d00b96c428aab
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942560"
---
# <a name="dhcp-logging-events-for-dns-registrations"></a>DHCP-Protokollierungs Ereignisse für DNS-Registrierungen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Die DHCP-Server Ereignisprotokolle enthalten jetzt ausführliche Informationen zu Fehlern bei der DNS-Registrierung.

>[!NOTE]
>In vielen Fällen ist der Grund für den Fehler bei der Registrierung von DNS-Einträgen durch DHCP-Server, dass eine DNS-Reverse- \- Lookupzone entweder falsch oder überhaupt nicht konfiguriert ist.

Die folgenden neuen DHCP-Ereignisse helfen Ihnen, leicht zu erkennen, wann DNS-Registrierungen aufgrund einer falsch konfigurierten oder fehlenden DNS-Reverse-Lookupzone fehlschlagen \- .

|id|Ereignis|Wert|
|-----|--------------------|--------------------------------------------------------|
|20317|DHCPv4. forwardrecorddnsfailure|Fehler bei der Daten Satz Registrierung für die IPv4-Adresse "%1" und den voll qualifizierten Namen "%2": %3. Dies liegt wahrscheinlich daran, dass die Forward-Lookupzone für diesen Datensatz auf dem DNS-Server nicht vorhanden ist.|
|20318|DHCPv4. forwardrecorddnstimeout|Fehler bei der Daten Satz Registrierung für die IPv4-Adresse "%1" und den voll qualifizierten Namen "%2": %3.|
|20319|DHCPv4. ptrrecorddnsfailure|Fehler beim Registrieren des PTR-Datensatzes für die IPv4-Adresse "%1" und den voll qualifizierten Namen "%2". Dies liegt wahrscheinlich daran, dass die Reverse-Lookupzone für diesen Datensatz auf dem DNS-Server nicht vorhanden ist.|
|20320|DHCPv4. ptrrecorddnstimeout|Fehler beim Registrieren des PTR-Datensatzes für die IPv4-Adresse "%1" und den voll qualifizierten Namen "%2".|
|20321|DHCPv6. forwardrecorddnsfailure|Fehler bei der Daten Satz Registrierung für die IPv6-Adresse "%1" und den voll qualifizierten Namen "%2": %3. Dies liegt wahrscheinlich daran, dass die Forward-Lookupzone für diesen Datensatz auf dem DNS-Server nicht vorhanden ist.|
|20322|DHCPv6. forwardrecorddnstimeout|Fehler bei der Daten Satz Registrierung für die IPv6-Adresse "%1" und den voll qualifizierten Namen "%2": %3.|
|20323|DHCPv6. ptrrecorddnsfailure|Fehler bei der Registrierung des PTR-Datensatzes für die IPv6-Adresse "%1" und den voll qualifizierten Namen "%2". Dies liegt wahrscheinlich daran, dass die Reverse-Lookupzone für diesen Datensatz auf dem DNS-Server nicht vorhanden ist.|
|20324|DHCPv6. ptrrecorddnstimeout|Fehler bei der Registrierung des PTR-Datensatzes für die IPv6-Adresse "%1" und den voll qualifizierten Namen "%2".|
|20325|DHCPv4. forwardrecorddnserror|Fehler beim Registrieren des PTR-Datensatzes für die IPv4-Adresse "%1" und den Fehler "%2": %3 \( %4 \) .|
|20326|DHCPv6. forwardrecorddnserror|Fehler bei der Daten Satz Registrierung für die IPv6-Adresse "%1" und den voll qualifizierten Namen "%2". %3 \( %4\)|
|20327|DHCPv6. ptrrecorddnserror|Fehler beim Registrieren des PTR-Datensatzes für die IPv6-Adresse "%1" und den Fehler "%2": %3 \( %4 \) .|


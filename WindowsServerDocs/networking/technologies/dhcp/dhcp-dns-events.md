---
title: DHCP-Protokollierung von Ereignissen für DNS-Registrierungen für aufzeichnen
description: Dieses Thema enthält Informationen zu DHCP-Server Protokollieren von Ereignissen in Windows Server2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: beb8c188-6fcf-4520-8825-d17f8ee9fb04
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 61a5099cd5e1ef1d4687baa8c20411c96ea8f519
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="dhcp-logging-events-for-dns-registrations"></a>DHCP-Protokollierung von Ereignissen für die DNS-Registrierung

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

DHCP-Server-Ereignisprotokolle enthalten nun ausführliche Informationen zu DNS-Registrierungsfehler.

>[!NOTE]
>In vielen Fällen ist die Ursache für Fehler bei der DNS-Registrierung von DHCP-Servern, dass eine DNS-Reverse\-Lookupzone falsch konfiguriert oder gar nicht konfiguriert wird.

Die folgenden neuen DHCP-Ereignisse unterstützen Sie einfach identifizieren, wenn die DNS-Registrierung fehlerhaft aufgrund einer falsch konfigurierten oder fehlende DNS-Reverse\-Lookupzone.

|ID|Ereignis|Wert|
|-----|--------------------|--------------------------------------------------------|
|20317|DHCPv4.ForwardRecordDNSFailure|Fehler %3 bei der Registrierung eines Forward für IPv4-Adresse %1 und %2-FQDN. Dies ist wahrscheinlich, da die Forward-Lookupzone für diesen Datensatz nicht auf dem DNS-Server vorhanden ist.|
|20318|DHCPv4.ForwardRecordDNSTimeout|Fehler %3 bei der Registrierung eines Forward für IPv4-Adresse %1 und %2-FQDN.|
|20319|DHCPv4.PTRRecordDNSFailure|Fehler %3 bei der Registrierung der PTR-Einträge für IPv4-Adresse %1 und %2-FQDN. Dies ist wahrscheinlich, da der Reverse-Lookupzone für diesen Datensatz nicht auf dem DNS-Server vorhanden ist.|
|20320|DHCPv4.PTRRecordDNSTimeout|Fehler %3 bei der Registrierung der PTR-Einträge für IPv4-Adresse %1 und %2-FQDN.|
|20321|DHCPv6.ForwardRecordDNSFailure|Fehler %3 bei der Registrierung eines Forward für IPv6-Adresse %1 und %2-FQDN. Dies ist wahrscheinlich, da die Forward-Lookupzone für diesen Datensatz nicht auf dem DNS-Server vorhanden ist.|
|20322|DHCPv6.ForwardRecordDNSTimeout|Fehler %3 bei der Registrierung eines Forward für IPv6-Adresse %1 und %2-FQDN.|
|20323|DHCPv6.PTRRecordDNSFailure|Fehler %3 bei der Registrierung der PTR-Einträge für IPv6-Adresse %1 und %2-FQDN. Dies ist wahrscheinlich, da der Reverse-Lookupzone für diesen Datensatz nicht auf dem DNS-Server vorhanden ist.|
|20324|DHCPv6.PTRRecordDNSTimeout|Fehler %3 bei der Registrierung der PTR-Einträge für IPv6-Adresse %1 und %2-FQDN.|
|20325|DHCPv4.ForwardRecordDNSError|Fehler %3 \(%4\) bei der Registrierung der PTR-Einträge für IPv4-Adresse %1 und %2-FQDN.|
|20326|DHCPv6.ForwardRecordDNSError|Fehler bei der Forward aufzeichnen Registrierung für IPv6-Adresse %1 und %2-FQDN mit Fehler %3 \(%4\)|
|20327|DHCPv6.PTRRecordDNSError|Fehler %3 \(%4\) bei der Registrierung der PTR-Einträge für IPv6-Adresse %1 und %2-FQDN.|


---
title: DHCP-Protokollierung von Ereignissen für DNS-Datensatz Registrierungen
description: Dieses Thema enthält Informationen zu DHCP-Server zu protokollieren von Ereignissen in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: beb8c188-6fcf-4520-8825-d17f8ee9fb04
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7f4ce217b19cfd8a63bff1ae504362d4fc24fcd0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816901"
---
# <a name="dhcp-logging-events-for-dns-registrations"></a>DHCP-Protokollierung von Ereignissen für DNS-Registrierungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

DHCP-Server-Ereignisprotokolle bieten jetzt detaillierte Informationen über Fehler bei der DNS-Registrierung.

>[!NOTE]
>In vielen Fällen ist die Ursache für Fehler bei der DNS-Datensatz Registrierung durch DHCP-Server, dass ein DNS-Reverse\-Lookup-Zone ist entweder falsch konfiguriert oder überhaupt nicht konfiguriert.

Die folgenden neuen DHCP-Ereignisse unterstützen Sie auf einfache Weise identifizieren, wenn DNS-Registrierungen sind fehlerhaft aufgrund einer falsch konfigurierten oder fehlende Reverse-DNS\-Lookup-Zone.

|ID|Ereignis|Wert|
|-----|--------------------|--------------------------------------------------------|
|20317|DHCPv4.ForwardRecordDNSFailure|Fehler %3 bei der Registrierung eines Forward für IPv4-Adresse %1 und %2-FQDN. Dies ist wahrscheinlich, da die forward-Lookupzone für diesen Datensatz auf dem DNS-Server nicht vorhanden ist.|
|20318|DHCPv4.ForwardRecordDNSTimeout|Fehler %3 bei der Registrierung eines Forward für IPv4-Adresse %1 und %2-FQDN.|
|20319|DHCPv4.PTRRecordDNSFailure|PTR-Datensatz-Registrierung für die IPv4-Adresse %1 und %2-FQDN, Fehler bei %3. Dies ist wahrscheinlich, da die reverse-Lookupzone für diesen Datensatz auf dem DNS-Server nicht vorhanden ist.|
|20320|DHCPv4.PTRRecordDNSTimeout|PTR-Datensatz-Registrierung für die IPv4-Adresse %1 und %2-FQDN, Fehler bei %3.|
|20321|DHCPv6.ForwardRecordDNSFailure|Fehler %3 bei der Registrierung eines Forward für IPv6-Adresse %1 und %2-FQDN. Dies ist wahrscheinlich, da die forward-Lookupzone für diesen Datensatz auf dem DNS-Server nicht vorhanden ist.|
|20322|DHCPv6.ForwardRecordDNSTimeout|Fehler %3 bei der Registrierung eines Forward für IPv6-Adresse %1 und %2-FQDN.|
|20323|DHCPv6.PTRRecordDNSFailure|PTR-Datensatz-Registrierung für die IPv6-Adresse %1 und %2-FQDN, Fehler bei %3. Dies ist wahrscheinlich, da die reverse-Lookupzone für diesen Datensatz auf dem DNS-Server nicht vorhanden ist.|
|20324|DHCPv6.PTRRecordDNSTimeout|PTR-Datensatz-Registrierung für die IPv6-Adresse %1 und %2-FQDN, Fehler bei %3.|
|20325|DHCPv4.ForwardRecordDNSError|Fehler bei der PTR-Datensatz-Registrierung für IPv4-Adresse %1 und %2-FQDN Fehlercode: %3 \(%4\).|
|20326|DHCPv6.ForwardRecordDNSError|Fehler %3 bei der Registrierung eines Forward für IPv6-Adresse %1 und %2-FQDN \(%4\)|
|20327|DHCPv6.PTRRecordDNSError|Fehler bei der PTR-Datensatz-Registrierung für IPv6-Adresse %1 und %2-FQDN Fehlercode: %3 \(%4\).|


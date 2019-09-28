---
title: DHCP-Protokollierungs Ereignisse für DNS-Daten Satz Registrierungen
description: Dieses Thema enthält Informationen zu DHCP-Server Protokollierungs Ereignissen in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: beb8c188-6fcf-4520-8825-d17f8ee9fb04
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ccd8024af30f1103afa8eac52926a6b42d32940a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355427"
---
# <a name="dhcp-logging-events-for-dns-registrations"></a>DHCP-Protokollierungs Ereignisse für DNS-Registrierungen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Die DHCP-Server Ereignisprotokolle enthalten jetzt ausführliche Informationen zu Fehlern bei der DNS-Registrierung.

>[!NOTE]
>In vielen Fällen liegt der Grund für die Registrierung von DNS-Einträgen durch DHCP-Server darin, dass eine DNS Reverse @ no__t-0lookupzone entweder falsch konfiguriert oder überhaupt nicht konfiguriert ist.

Die folgenden neuen DHCP-Ereignisse helfen Ihnen, leicht zu erkennen, wann DNS-Registrierungen aufgrund einer falsch konfigurierten oder fehlenden DNS Reverse @ no__t-0lookupzone fehlschlagen.

|ID|Ereignis|Wert|
|-----|--------------------|--------------------------------------------------------|
|20317|DHCPv4. forwardrecorddnsfailure|Fehler bei der Daten Satz Registrierung für die IPv4-Adresse "% 1" und den voll qualifizierten Namen "% 2":% 3. Dies liegt wahrscheinlich daran, dass die Forward-Lookupzone für diesen Datensatz auf dem DNS-Server nicht vorhanden ist.|
|20318|DHCPv4. forwardrecorddnstimeout|Fehler bei der Daten Satz Registrierung für die IPv4-Adresse "% 1" und den voll qualifizierten Namen "% 2":% 3.|
|20319|DHCPv4. ptrrecorddnsfailure|Fehler beim Registrieren des PTR-Datensatzes für die IPv4-Adresse "% 1" und den voll qualifizierten Namen "% 2". Dies liegt wahrscheinlich daran, dass die Reverse-Lookupzone für diesen Datensatz auf dem DNS-Server nicht vorhanden ist.|
|20320|DHCPv4. ptrrecorddnstimeout|Fehler beim Registrieren des PTR-Datensatzes für die IPv4-Adresse "% 1" und den voll qualifizierten Namen "% 2".|
|20321|DHCPv6. forwardrecorddnsfailure|Fehler bei der Daten Satz Registrierung für die IPv6-Adresse "% 1" und den voll qualifizierten Namen "% 2":% 3. Dies liegt wahrscheinlich daran, dass die Forward-Lookupzone für diesen Datensatz auf dem DNS-Server nicht vorhanden ist.|
|20322|DHCPv6. forwardrecorddnstimeout|Fehler bei der Daten Satz Registrierung für die IPv6-Adresse "% 1" und den voll qualifizierten Namen "% 2":% 3.|
|20323|DHCPv6. ptrrecorddnsfailure|Fehler bei der Registrierung des PTR-Datensatzes für die IPv6-Adresse "% 1" und den voll qualifizierten Namen "% 2". Dies liegt wahrscheinlich daran, dass die Reverse-Lookupzone für diesen Datensatz auf dem DNS-Server nicht vorhanden ist.|
|20324|DHCPv6. ptrrecorddnstimeout|Fehler bei der Registrierung des PTR-Datensatzes für die IPv6-Adresse "% 1" und den voll qualifizierten Namen "% 2".|
|20325|DHCPv4. forwardrecorddnserror|Fehler bei der PTR-Daten Satz Registrierung für die IPv4-Adresse "% 1" und den voll qualifizierten Namen "% 2":% 3 \(% 4 @ no__t-1.|
|20326|DHCPv6. forwardrecorddnserror|Fehler beim Registrieren des Forward-Datensatzes für die IPv6-Adresse "% 1" und den voll qualifizierten Namen "% 2":% 3 \(% 4 @ no__t-1|
|20327|DHCPv6. ptrrecorddnserror|Fehler bei der PTR-Daten Satz Registrierung für die IPv6-Adresse "% 1" und den voll qualifizierten Namen "% 2":% 3 \(% 4 @ no__t-1.|


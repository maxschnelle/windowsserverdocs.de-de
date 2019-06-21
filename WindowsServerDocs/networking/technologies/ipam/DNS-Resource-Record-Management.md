---
title: Verwaltung von DNS-Ressourceneinträgen
description: Dieses Thema ist Teil des Leitfadens Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66c09d-e401-4f70-9a2a-6047dd629bfa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a2db802fa928a4051fbe409fc0ba60d774bb0428
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284054"
---
# <a name="dns-resource-record-management"></a>Verwaltung von DNS-Ressourceneinträgen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema enthält Informationen zum Verwalten von DNS-Ressourceneinträge mithilfe von IPAM.  
  
> [!NOTE]  
> Zusätzlich zu diesem Thema sind die folgenden DNS-Ressource-datensatzverwaltung Themen in diesem Abschnitt verfügbar.  
>   
> -   [Hinzufügen eines DNS-Ressourceneintrags](../../technologies/ipam/Add-a-DNS-Resource-Record.md)  
> -   [Löschen von DNS-Ressourceneinträgen](../../technologies/ipam/Delete-DNS-Resource-Records.md)  
> -   [Filtern der Ansicht von DNS-Ressourceneinträgen](../../technologies/ipam/Filter-the-View-of-DNS-Resource-Records.md)  
> -   [Anzeigen von DNS-Ressourceneinträge für eine bestimmte IP-Adresse](../../technologies/ipam/View-DNS-Resource-Records-for-a-Specific-IP-Address.md)  
  
## <a name="resource-record-management-overview"></a>Übersicht über die Resource-datensatzverwaltung  
Wenn Sie IPAM unter Windows Server 2016 bereitstellen, können Sie die serverermittlung zum Hinzufügen von DHCP- und DNS-Server zur IPAM-Server-Verwaltungskonsole ausführen. Der IPAM-Server dann dynamisch erfasst DNS-Daten alle sechs Stunden von der DNS-Servern, die sie konfiguriert ist verwalten. IPAM verwaltet eine lokale Datenbank, in dem sie diese DNS-Daten speichert. IPAM bietet Ihnen Benachrichtigungen über den Tag und die Zeit, die die Server-Daten gesammelt wurden, sowie die am nächsten Tag angezeigt, und die Uhrzeit, wann die Datensammlung von DNS-Server ausgeführt wird.  
  
Die gelbe Statusleiste in der folgenden Abbildung zeigt den Speicherort der Benutzeroberfläche des IPAM-Benachrichtigungen.  
  
![IPAM-Benachrichtigungen](../../media/DNS-Resource-Record-Management/ipam_DataCollection_01.jpg)  
  
Die gesammelten Daten für die DNS-enthält DNS-Zone und Ressource Informationen aufzuzeichnen. Sie können IPAM zum Sammeln von Zoneninformationen über Ihre bevorzugten DNS-Server konfigurieren.  IPAM sammelt sowohl die dateibasierte als auch die Active Directory-Zonen.  
  
> [!NOTE]  
> IPAM sammelt Daten ausschließlich aus der Domäne verbundene Microsoft DNS-Server. Die DNS-Servern von Drittanbietern und nicht in Domänen eingebundene Server werden von IPAM nicht unterstützt.  
  
Es folgt eine Liste der DNS-Ressourcendatensatztypen, die von IPAM gesammelt werden.  
  
-   AFS-Datenbank  
  
-   ATM-Adresse  
  
-   CNAME  
  
-   DHCID  
  
-   DNAME  
  
-   Host A oder AAAA  
  
-   Informationen zum Host  
  
-   ISDN  
  
-   MX  
  
-   Namenserver  
  
-   Zeigerressourceneinträge (PTR)  
  
-   Verantwortliche person  
  
-   Weiterleitung über  
  
-   Dienstidentifizierung  
  
-   SOA  
  
-   SRV  
  
-   Text  
  
-   Bekannte Dienste  
  
-   WINS  
  
-   WINS-R  
  
-   X.25  
  
In Windows Server 2016 bietet IPAM eine Integration zwischen IP-adressbestand, DNS-Zonen und DNS-Ressourceneinträge:  
  
-   Sie können IPAM verwenden, um automatisch eine IP-adressbestand von DNS-Ressourceneinträge erstellen.  
  
-   Sie können eine IP-adressbestand manuell vom DNS A- und AAAA-Ressourceneinträge erstellen.  
  
-   Sie können DNS-Ressourceneinträgen für eine bestimmte DNS-Zone anzeigen und Filtern die Datensätze basierend auf Typ, IP-Adresse, Datensatz Ressourcendaten und anderen Filteroptionen.  
  
-   IPAM erstellt automatisch eine Zuordnung zwischen IP-Adressbereiche und DNS-Reverse-Lookup-Zonen.  
  
-   IPAM erstellt IP-Adressen für die PTR-Einträge, die in der reverse-Lookup-Zone vorhanden sind und die in diesen IP-Adressbereich enthalten sind. Sie können diese Zuordnung auch manuell ändern, falls erforderlich.  
  
IPAM ermöglicht Ihnen die folgenden Vorgänge für Ressourceneinträge in der IPAM-Konsole ausführen.  
  
-   Erstellen von DNS-Ressourceneinträgen  
  
-   Bearbeiten Sie die DNS-Ressourceneinträgen  
  
-   Löschen von DNS-Ressourceneinträgen  
  
-   Erstellen Sie die zugehörigen Ressourceneinträge  
  
IPAM meldet Sie automatisch alle DNS-Änderungen an der Konfiguration, dass Sie mithilfe der IPAM-Konsole vornehmen.  
  
## <a name="see-also"></a>Siehe auch  
[Verwalten von IPAM](Manage-IPAM.md)  
  



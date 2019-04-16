---
title: DNS-Datensatz Ressourcenverwaltung
description: Dieses Thema ist Teil des Handbuchs Verwaltung von IP-Adressverwaltung (IPAM) in Windows Server2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66c09d-e401-4f70-9a2a-6047dd629bfa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5ed781ef37243b80ea9da8aad27a29046b8dc8c9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="dns-resource-record-management"></a>DNS-Datensatz Ressourcenverwaltung

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Thema enthält Informationen zum Verwalten von DNS-Ressourceneinträge mithilfe von IPAM.  
  
> [!NOTE]  
> Zusätzlich zu diesem Thema werden die folgenden DNS-Ressource aufzeichnen Management-Themen in diesem Abschnitt.  
>   
> -   [Hinzufügen eines DNS-Ressourceneintrags](../../technologies/ipam/Add-a-DNS-Resource-Record.md)  
> -   [Löschen von DNS-Ressourceneinträgen](../../technologies/ipam/Delete-DNS-Resource-Records.md)  
> -   [Filtern der Ansicht von DNS-Ressourceneinträgen](../../technologies/ipam/Filter-the-View-of-DNS-Resource-Records.md)  
> -   [Anzeigen von DNS-Ressourceneinträgen für eine bestimmte IP-Adresse](../../technologies/ipam/View-DNS-Resource-Records-for-a-Specific-IP-Address.md)  
  
## <a name="resource-record-management-overview"></a>Resource Record Management (Übersicht)  
Bei der Bereitstellung von IPAM in Windows Server2016 können Sie Server-Ermittlung zum Hinzufügen von DHCP- und DNS-Servern für die IPAM-Server Management Console durchführen. Der IPAM-Server dann dynamisch DNS-Daten erfasst alle sechs Stunden die DNS-Server, die Konfiguration zur verwalten. IPAM verwaltet eine lokale Datenbank, in denen diese DNS-Daten gespeichert. IPAM bietet Ihnen eine Benachrichtigung über den Tag und Zeit, die die Server-Daten gesammelt wurden, sowie die am nächsten Tag angezeigt wird, und die Datensammlung von DNS-Servern erfolgen wird.  
  
Gelbe Statusleiste in der folgenden Abbildungzeigt den Speicherort der Benutzeroberfläche der IPAM-Benachrichtigungen.  
  
![IPAM-Benachrichtigungen](../../media/DNS-Resource-Record-Management/ipam_DataCollection_01.jpg)  
  
Die DNS-Daten, die gesammelt werden enthält DNS-Zone Informationen und Ressourcen aufzeichnen. Sie können IPAM zum Sammeln von Informationen aus Ihrem bevorzugten DNS-Server konfigurieren.  IPAM sammelt dateibasierte und Active Directory-Zonen.  
  
> [!NOTE]  
> IPAM sammelt Daten ausschließlich von Microsoft DNS-Servern Domäne. Die DNS-Servern von Drittanbietern und nicht der Domäne verbundene Server werden durch IPAM nicht unterstützt.  
  
Es folgt eine Liste der DNS-Ressourcendatensatztypen, die von IPAM gesammelt werden.  
  
-   AFS-Datenbank  
  
-   ATM-Adresse  
  
-   CNAME  
  
-   DHCID  
  
-   DNAME  
  
-   Host A oder AAAA  
  
-   Host-Informationen  
  
-   ISDN  
  
-   MX  
  
-   Namensserver  
  
-   Zeigerressourceneinträge (PTR)  
  
-   Verantwortliche Person  
  
-   Umleiten  
  
-   Speicherort  
  
-   SOA  
  
-   SRV  
  
-   Text  
  
-   Bekannte Dienste  
  
-   WINS  
  
-   WINS-R  
  
-   X. 25  
  
In Windows Server2016 bietet IPAM Integration von IP-adressbestand, DNS-Zonen und DNS-Ressourceneinträge:  
  
-   IPAM können Sie um eine IP-adressbestand von DNS-Ressourceneinträge automatisch erstellen.  
  
-   Sie können manuell eine IP-adressbestand von DNS A- und AAAA-Ressourceneinträge erstellen.  
  
-   Sie können DNS-Ressourceneinträgen für eine bestimmte DNS-Zone anzeigen und Filtern der Datensätze, die je nach Typ, IP-Adresse, Datensatz Ressourcendaten und andere Filteroptionen.  
  
-   IPAM wird automatisch eine Zuordnung zwischen IP-Adressbereiche und DNS-Reverse-Lookupzonen erstellt.  
  
-   IPAM erstellt IP-Adressen für die PTR-Einträge, die in der Reverse-Lookupzone vorhanden sind und die in die IP-Adressbereich enthalten sind. Sie können diese Zuordnung auch manuell ändern, falls erforderlich.  
  
IPAM können Sie die folgenden Vorgänge für Ressourceneinträge aus der IPAM-Konsole ausführen.  
  
-   Erstellen von DNS-Ressourceneinträgen  
  
-   Bearbeiten von DNS-Ressourceneinträgen  
  
-   Löschen von DNS-Ressourceneinträgen  
  
-   Erstellen Sie die zugehörigen Ressourceneinträge  
  
IPAM meldet Sie automatisch alle DNS-Konfiguration geändert wird, Sie mit der IPAM-Konsole.  
  
## <a name="see-also"></a>Siehe auch  
[Verwalten von IPAM](Manage-IPAM.md)  
  



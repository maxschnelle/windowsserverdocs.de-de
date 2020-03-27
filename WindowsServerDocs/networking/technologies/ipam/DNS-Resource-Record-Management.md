---
title: Verwaltung von DNS-Ressourceneinträgen
description: Dieses Thema ist Teil des Verwaltungs Handbuchs für die IP-Adressverwaltung (IPAM) in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66c09d-e401-4f70-9a2a-6047dd629bfa
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 3aa20913a01a23291879b98d6f53fe60a7138670
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312452"
---
# <a name="dns-resource-record-management"></a>Verwaltung von DNS-Ressourceneinträgen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Dieses Thema enthält Informationen zum Verwalten von DNS-Ressourcen Einträgen mithilfe von IPAM.  
  
> [!NOTE]  
> Zusätzlich zu diesem Thema sind die folgenden Themen zur Verwaltung von DNS-Ressourcen Einträgen in diesem Abschnitt verfügbar.  
>   
> -   [Hinzufügen eines DNS-Ressourcen Datensatzes](../../technologies/ipam/Add-a-DNS-Resource-Record.md)  
> -   [Löschen von DNS-Ressourcen Einträgen](../../technologies/ipam/Delete-DNS-Resource-Records.md)  
> -   [Filtern der Sicht der DNS-Ressourcen Einträge](../../technologies/ipam/Filter-the-View-of-DNS-Resource-Records.md)  
> -   [Anzeigen von DNS-Ressourcen Einträgen für eine bestimmte IP-Adresse](../../technologies/ipam/View-DNS-Resource-Records-for-a-Specific-IP-Address.md)  
  
## <a name="resource-record-management-overview"></a>Übersicht über die Ressourcen Daten Satz Verwaltung  
Wenn Sie IPAM in Windows Server 2016 bereitstellen, können Sie die Server Ermittlung durchführen, um DHCP-und DNS-Server zur IPAM-Server-Verwaltungskonsole hinzuzufügen. Der IPAM-Server sammelt dann alle sechs Stunden dynamische DNS-Daten von den DNS-Servern, die für die Verwaltung konfiguriert sind. IPAM verwaltet eine lokale Datenbank, in der diese DNS-Daten gespeichert werden. Mit IPAM erhalten Sie eine Benachrichtigung über den Tag und die Uhrzeit, zu der die Serverdaten gesammelt wurden, sowie über den nächsten Tag und die Uhrzeit, zu der die Datensammlung von DNS-Servern stattfindet.  
  
Die Gelbe Statusleiste in der folgenden Abbildung zeigt den Speicherort der Benutzeroberfläche von IPAM-Benachrichtigungen.  
  
![IPAM-Benachrichtigungen](../../media/DNS-Resource-Record-Management/ipam_DataCollection_01.jpg)  
  
Zu den gesammelten DNS-Daten zählen Informationen zur DNS-Zonen-und Ressourcen Aufzeichnung. Sie können IPAM so konfigurieren, dass Zonen Informationen von Ihrem bevorzugten DNS-Server gesammelt werden.  IPAM sammelt sowohl Datei-als auch Active Directory Zonen.  
  
> [!NOTE]  
> IPAM sammelt Daten ausschließlich von in die Domäne eingebundenen Microsoft DNS-Servern. DNS-Server von Drittanbietern und Server, die keiner Domäne beigetreten sind, werden von IPAM nicht unterstützt.  
  
Im folgenden finden Sie eine Liste der DNS-Ressourcen Daten Satz Typen, die von IPAM gesammelt werden.  
  
-   AFS-Datenbank  
  
-   ATM-Adresse  
  
-   CNAME  
  
-   DHCID  
  
-   DName  
  
-   Host A oder AAAA  
  
-   Host Informationen  
  
-   Digitalen  
  
-   MX  
  
-   Namenserver  
  
-   Zeiger (PTR)  
  
-   Verantwortliche Person  
  
-   Weiterleiten  
  
-   Dienst Identifizierung  
  
-   SOA  
  
-   SRV  
  
-   Text  
  
-   Bekannte Dienste  
  
-   WINS  
  
-   WINS-R  
  
-   X. 25  
  
In Windows Server 2016 bietet IPAM eine Integration zwischen IP-Adress Inventur, DNS-Zonen und DNS-Ressourcen Einträgen:  
  
-   Sie können IPAM verwenden, um automatisch einen IP-Adress bestand aus DNS-Ressourcen Einträgen zu erstellen.  
  
-   Sie können einen IP-Adress bestand aus DNS A-und AAAA-Ressourcen Einträgen manuell erstellen.  
  
-   Sie können DNS-Ressourcen Einträge für eine bestimmte DNS-Zone anzeigen und die Datensätze basierend auf Typ, IP-Adresse, Ressourcen Daten Satz Daten und anderen Filteroptionen filtern.  
  
-   IPAM erstellt automatisch eine Zuordnung zwischen IP-Adressbereichen und DNS-Reverse-Lookupzonen.  
  
-   Von IPAM werden IP-Adressen für die PTR-Einträge erstellt, die in der Reverse-Lookupzone vorhanden sind und in diesem IP-Adressbereich enthalten sind. Sie können diese Zuordnung bei Bedarf auch manuell ändern.  
  
Mit IPAM können Sie die folgenden Vorgänge für Ressourcen Einträge über die IPAM-Konsole ausführen.  
  
-   Erstellen von DNS-Ressourcen Einträgen  
  
-   Bearbeiten von DNS-Ressourcen Einträgen  
  
-   Löschen von DNS-Ressourceneinträgen  
  
-   Verknüpfte Ressourcen Einträge erstellen  
  
IPAM protokolliert automatisch alle Änderungen an der DNS-Konfiguration, die Sie mithilfe der IPAM-Konsole vornehmen.  
  
## <a name="see-also"></a>Weitere Informationen  
[Verwalten von IPAM](Manage-IPAM.md)  
  



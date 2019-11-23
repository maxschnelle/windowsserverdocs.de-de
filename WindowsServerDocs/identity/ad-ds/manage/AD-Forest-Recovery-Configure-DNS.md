---
title: 'AD-Gesamtstruktur Wiederherstellung: Konfigurieren des DNS-Server'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 2c1f2f68509c9136735fb13e24c86a1da40660eb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369246"
---
# <a name="ad-forest-recovery---configuring-the-dns-server-service"></a>AD-Gesamtstruktur Wiederherstellung: Konfigurieren des DNS-Server Dienstes

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Wenn die DNS-Server Rolle nicht auf dem Domänen Controller installiert ist, den Sie aus der Sicherung wiederherstellen, müssen Sie den DNS-Server installieren und konfigurieren. 

## <a name="install-and-configure-the-dns-server-service"></a>Installieren und Konfigurieren des DNS-Server Dienstanbieter

Führen Sie diesen Schritt für jeden wiederhergestellten DC aus, der nach Abschluss der Wiederherstellung nicht als DNS-Server ausgeführt wird. 

> [!NOTE]
> Wenn der von der Sicherung wiederhergestellte Domänen Controller unter Windows Server 2008 R2 ausgeführt wird, müssen Sie den Domänen Controller mit einem isolierten Netzwerk verbinden, um den DNS-Server zu installieren. Verbinden Sie dann jeden der wiederhergestellten DNS-Server mit einem sich gegenseitig freigegebenen, isolierten Netzwerk. Führen Sie Repadmin/replsum aus, um sicherzustellen, dass die Replikation zwischen den wiederhergestellten DNS-Servern funktioniert Nachdem Sie die Replikation überprüft haben, können Sie die wiederhergestellten DCS mit dem Produktionsnetzwerk verbinden, wenn die DNS-Server Rolle bereits installiert ist. Sie können einen Hotfix anwenden, der den Start eines DNS-Servers ermöglicht, während der Server nicht mit einem Netzwerk verbunden ist. Sie sollten den Hotfix während der automatisierten Buildprozesse in das Betriebssystem-Installations Abbild überschreiben. Weitere Informationen zum Hotfix finden Sie im [Artikel 975654](https://go.microsoft.com/fwlink/?LinkId=184691) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=184691). 

Führen Sie die folgenden Schritte zur Installation und Konfiguration aus.

### <a name="to-install-and-the-dns-server-service-using-server-manager"></a>So installieren Sie und den DNS-Server Dienst mithilfe von Server-Manager  

1. Öffnen Sie Server-Manager, und klicken Sie auf **Rollen und Features hinzufügen**. 
2. Wenn im Assistenten zum Hinzufügen von Rollen die Seite **Vorbemerkungen** angezeigt wird, klicken Sie auf **Weiter**. 
3. Wählen Sie auf der Seite **Installationstyp** die Option **rollenbasierte oder featurebasierte Installation** aus, und klicken Sie auf **weiter**
4. Wählen Sie auf dem Bildschirm **Server Auswahl** den Server aus, und klicken Sie auf **weiter**.
5. Wählen Sie auf dem Bildschirm **Server Rollen** die Option **DNS-Server**aus, und **Klicken Sie**bei entsprechender Aufforderung auf **Features hinzufügen**
6. Klicken Sie auf dem Bildschirm **Features** auf **weiter**.
7. Lesen Sie die Informationen auf der Seite **DNS-Server** , und klicken Sie dann auf **weiter**.
   ![DNS-Server](media/AD-Forest-Recovery-Configure-DNS/dns1.png)  
8. Überprüfen Sie auf der Seite **Bestätigung** , ob die DNS-Server Rolle installiert wird, und klicken Sie dann auf **Installieren**. 

### <a name="to-configure-the-dns-server-service"></a>So konfigurieren Sie den DNS-Server Dienst

1. Öffnen Sie Server-Manager, klicken Sie auf **Extras und dann auf** **DNS**.
   ![DNS-Server](media/AD-Forest-Recovery-Configure-DNS/dns2.png)
2. Erstellen Sie DNS-Zonen für die gleichen DNS-Domänen Namen, die vor dem kritischen Funktionsfehler auf den DNS-Servern gehostet wurden. Weitere Informationen finden Sie unter Hinzufügen einer Forward-Lookupzone ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574)).
3. Konfigurieren Sie die DNS-Daten so, wie Sie vor den kritischen Fehlern vorhanden waren. Zum Beispiel:  

   - Konfigurieren Sie DNS-Zonen, die in AD DS gespeichert werden sollen. Weitere Informationen finden Sie unter Ändern des Zonen Typs ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579)).
   - Konfigurieren Sie die DNS-Zone, die für Domänen Controller-Serverlocatorpunkt-Ressourcen Einträge (DC Serverlocatorpunkt) autorisierend ist, um sicheres dynamisches Update zuzulassen. Weitere Informationen finden Sie unter nur sichere dynamische Updates zulassen ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580)).

4. Stellen Sie sicher, dass die übergeordnete DNS-Zone Delegat-Ressourcen Einträge (Nameserver (NS) und Host (A)-Ressourcen Einträge) für die untergeordnete Zone enthält, die auf diesem DNS-Server gehostet wird. Weitere Informationen finden Sie unter Erstellen einer Zonen Delegierung ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562)).
5. Nachdem Sie DNS konfiguriert haben, können Sie die Registrierung der Netlogon-Einträge beschleunigen.

   > [!NOTE]
   > Sichere dynamische Updates funktionieren nur, wenn ein globaler Katalogserver verfügbar ist. 

   Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie die EINGABETASTE:  

   **NET stoppt Netlogon**  

6. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:  

   **NET Start Netlogon**  

   ![DNS-Server](media/AD-Forest-Recovery-Configure-DNS/dns3.png)  

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)

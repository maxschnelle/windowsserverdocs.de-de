---
title: Wiederherstellung der Active Directory-Gesamtstruktur - Konfigurieren von DNS-Serverdienst
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f24570965fd8b3f3e050779c42758865cbee2728
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---configuring-the-dns-server-service"></a>AD-Gesamtstruktur Recovery - Konfiguration des DNS-Serverdiensts 

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2
 
Wenn die DNS-Serverrolle nicht auf dem Domänencontroller, die Sie aus einer Sicherung wiederherstellen installiert ist, müssen Sie installieren und konfigurieren den DNS-Server.  
  

## <a name="install-and-configure-the-dns-server-service"></a>Installieren Sie und konfigurieren Sie den DNS-Serverdienst  
Führen Sie diesen Schrittfür jeden wiederhergestellten Domänencontroller, die nicht als ein DNS-Server ausgeführt wird, nachdem die Wiederherstellung abgeschlossen ist.  
  
> [!NOTE]
>  Wenn der Domänencontroller, die Sie aus einer Sicherung wiederhergestellt, Windows Server2008 R2 ausgeführt wird, müssen Sie den Domänencontroller mit einem isolierten Netzwerk verbinden, um DNS-Server installieren. Klicken Sie dann verbinden Sie den wiederhergestellten DNS-Servern mit einem sich gegenseitig gemeinsam genutzten, isolierten Netzwerk. Führen Sie Repadmin /replsum, stellen Sie sicher, dass die Replikation zwischen den wiederhergestellten DNS-Servern funktioniert. Nachdem Sie die Replikation überprüfen, können Sie den wiederhergestellten Domänencontroller mit dem Produktionsnetzwerk verbinden, wenn die DNS-Serverrolle bereits installiert ist, können Sie ein Update, das es ermöglicht, einen DNS-Server starten, während der Server nicht mit einem Netzwerk verbunden ist anwenden. Sie sollten den Hotfix in das Betriebssystemabbild-Installation während der automatisierten Buildprozesse slipstream. Weitere Informationen zu diesem Hotfix finden Sie unter [Artikel 975654](https://go.microsoft.com/fwlink/?LinkId=184691) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=184691). 

Führen Sie die folgenden Installations- und Konfigurationsschritte.
  
### <a name="to-install-and-the-dns-server-service-using-server-manager"></a>Installation und der DNS-Serverdienst mit Server-Manager  
  
1.  Öffnen Sie Server-Manager, und klicken Sie auf **Hinzufügen von Rollen und Features**.  
2.  Klicken Sie im Assistenten zum Hinzufügen von Rollen Wenn die **Vorbemerkungen** Seite angezeigt wird, klicken Sie auf **Weiter**.  
3.  Auf der **Installationstyp** Bildschirm wählen **Role-based oder Feature-basierte Installation**, und klicken Sie auf **Weiter**.
4.  Auf der **Serverauswahl** Bildschirm, wählen Sie den Server, und klicken Sie auf **Weiter**.
5.  Auf der **Serverrollen** Bildschirm wählen **DNS-Server**, klicken Sie auf Aufforderung **Features hinzufügen**, und klicken Sie auf **Weiter**.
6.  Auf der **Features** Bildschirm auf **Weiter**.
7.  Lesen Sie die Informationen auf der **DNS-Server** Seite, und klicken Sie dann auf **Weiter**.
![DNS-Server](media/AD-Forest-Recovery-Configure-DNS/dns1.png)  
8.  Auf der **Bestätigung** sicher, dass die DNS-Serverrolle installiert werden, und klicken Sie dann auf **installieren**.  
  
     
### <a name="to-configure-the-dns-server-service"></a>So konfigurieren Sie den DNS-Serverdienst 
1.  Öffnen Sie Server-Manager, klicken Sie auf **Tools**, und klicken Sie auf **DNS**.
![DNS-Server](media/AD-Forest-Recovery-Configure-DNS/dns2.png)    
2.  Erstellen Sie DNS-Zonen für die gleichen DNS-Domänennamen, die gehostet wurden auf die DNS-Server vor der kritischen Fehler. Weitere Informationen finden Sie unter Hinzufügen einer Forward-Lookupzone ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574)).  
3.  Konfigurieren Sie die DNS-Daten vor kritischen Fehlfunktion vorhanden war. Zum Beispiel:  
  
    -   Konfigurieren Sie DNS-Zonen in AD DS gespeichert werden. Weitere Informationen finden Sie unter Ändern des Zonentyps ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579)).  
  
    -   Konfigurieren Sie die DNS-Zone, die für Domänencontroller (DC-Locator) Ressource-Locatoreinträgen sichere dynamische Updates zulassen autorisierend ist. Weitere Informationen finden Sie unter ermöglichen nur sichere dynamische Updates ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580)).  
  
4. Stellen Sie sicher, dass die übergeordneten DNS-Zone Delegation-Ressourceneinträge (name Server (NS) und Kleben Host (A) Ressource Datensätze) für die untergeordnete Zone enthält, die auf diesen DNS-Server gehostet wird. Weitere Informationen finden Sie unter Erstellen einer Zonendelegierung ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562)).  
5. Wenn Sie DNS konfiguriert haben, können Sie die Registrierung der NETLOGON-Einträge beschleunigen.  
  
    > [!NOTE]
    >  Sichere dynamische Updates funktionieren nur, wenn ein globaler Katalogserver verfügbar ist.  
  
     Geben Sie den folgenden Befehl an der Eingabeaufforderung, und drücken Sie dann die EINGABETASTE:  
  
     **Net Stop netlogon**  
  
6. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:  
  
     **Net Start netlogon**  

![DNS-Server](media/AD-Forest-Recovery-Configure-DNS/dns3.png)  

## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)

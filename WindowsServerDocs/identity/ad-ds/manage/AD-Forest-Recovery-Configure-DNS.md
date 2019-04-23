---
title: Wiederherstellung der Active Directory-Gesamtstruktur - Konfigurieren von DNS-Serverdienst
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b2c37428a0fb685e6a7fa4875366f3cd13401bd9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842961"
---
# <a name="ad-forest-recovery---configuring-the-dns-server-service"></a>Wiederherstellung der Active Directory-Gesamtstruktur - Konfigurieren des DNS-Server-Diensts

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Wenn die DNS-Serverrolle nicht auf dem Domänencontroller, die Sie aus einer Sicherung wiederherstellen installiert ist, müssen Sie installieren und konfigurieren den DNS-Server. 

## <a name="install-and-configure-the-dns-server-service"></a>Installieren Sie und konfigurieren Sie den DNS-Serverdienst

Führen Sie diesen Schritt für jede wiederhergestellte DC, der nicht als ein DNS-Server ausgeführt wird, nachdem die Wiederherstellung abgeschlossen ist. 

> [!NOTE]
> Wenn der Domänencontroller, die Sie aus einer Sicherung wiederhergestellt, Windows Server 2008 R2 ausgeführt wird, müssen Sie den DC mit einem isolierten Netzwerk verbinden, um die DNS-Server installieren. Verbinden Sie alle wiederhergestellten DNS-Server klicken Sie dann mit einem Netzwerk sich gegenseitig gemeinsam genutzten, isoliert. Führen Sie Repadmin/replsum, um sicherzustellen, dass die Replikation zwischen den wiederhergestellten DNS-Server funktioniert. Nachdem Sie die Replikation überprüfen, können können Sie den wiederhergestellten Domänencontroller mit im Produktionsnetzwerk verbinden, wenn die DNS-Serverrolle bereits installiert ist, Sie einen Hotfix, der es macht es möglich, dass ein DNS-Server zu starten, während der Server nicht mit einem Netzwerk verbunden ist. Sie sollten den Hotfix in das Betriebssystemabbild-Installation während der Buildprozesse automatisierte slipstream. Weitere Informationen zu diesem Hotfix finden Sie unter [Artikel 975654](https://go.microsoft.com/fwlink/?LinkId=184691) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=184691). 

Die folgenden Schritte Installation und Konfiguration ausführen.

### <a name="to-install-and-the-dns-server-service-using-server-manager"></a>Installieren und den DNS-Serverdienst, der mit dem Server-Manager  

1. Öffnen Sie Server-Manager, und klicken Sie auf **Rollen und Features hinzufügen**. 
2. Wenn im Assistenten zum Hinzufügen von Rollen die Seite **Vorbemerkungen** angezeigt wird, klicken Sie auf **Weiter**. 
3. Auf der **Installationstyp** Bildschirm wählen **rollenbasierte oder featurebasierte Installation** , und klicken Sie auf **Weiter**.
4. Auf der **Serverauswahl** Bildschirm Wählen Sie den Server, und klicken Sie auf **Weiter**.
5. Auf der **Serverrollen** Bildschirm wählen **DNS-Server**, wenn Sie aufgefordert, klicken Sie auf **Features hinzufügen** , und klicken Sie auf **Weiter**.
6. Auf der **Features** Bildschirm auf **Weiter**.
7. Lesen Sie die Informationen auf der **DNS-Server** Seite, und klicken Sie dann auf **Weiter**.
   ![DNS-Server](media/AD-Forest-Recovery-Configure-DNS/dns1.png)  
8. Auf der **Bestätigung** Seite, stellen Sie sicher, dass die DNS-Serverrolle installiert werden, und klicken Sie dann auf **installieren**. 

### <a name="to-configure-the-dns-server-service"></a>So konfigurieren Sie den DNS-Serverdienst

1. Öffnen Sie Server-Manager, klicken Sie auf **Tools** , und klicken Sie auf **DNS**.
   ![DNS-Server](media/AD-Forest-Recovery-Configure-DNS/dns2.png)
2. Erstellen Sie DNS-Zonen für die gleiche DNS-Domänennamen, die gehostet wurden, auf die DNS-Server, bevor Sie die kritischen Fehler. Weitere Informationen finden Sie unter Hinzufügen einer Forward-Lookupzone ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574)).
3. Konfigurieren Sie die DNS-Daten, wie sie vor der Fehlfunktion kritische vorhanden waren. Zum Beispiel:  

   - Konfigurieren Sie DNS-Zonen, die in AD DS gespeichert werden. Weitere Informationen finden Sie unter Ändern des Zonentyps ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579)).
   - Konfigurieren Sie die DNS-Zone, die für Domänencontroller (DC Locator) Ressource-Locatoreinträgen um sichere dynamische Updates ermöglichen autorisierend ist. Weitere Informationen finden Sie ermöglichen nur sichere dynamische Updates ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580)).

4. Stellen Sie sicher, dass die übergeordneten DNS-Zone Delegation-Ressourceneinträge (Namen der Namenserver (NS) und "Klebstoff", Host (A) Ressource Datensätze) für die untergeordnete Zone enthält, die auf diesen DNS-Server gehostet wird. Weitere Informationen finden Sie unter Erstellen einer Zonendelegierung ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562)).
5. Nachdem Sie einen DNS konfigurieren, können Sie die Registrierung der NETLOGON-Datensätze beschleunigen.

   > [!NOTE]
   > Sichere dynamische Updates können nur auf, wenn ein globaler Katalogserver verfügbar ist. 

   Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie die EINGABETASTE:  

   **Net Stop netlogon**  

6. Geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE:  

   **Net Start netlogon**  

   ![DNS-Server](media/AD-Forest-Recovery-Configure-DNS/dns3.png)  

## <a name="next-steps"></a>Nächste Schritte

- [Für die Wiederherstellung des AD-Gesamtstruktur](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)

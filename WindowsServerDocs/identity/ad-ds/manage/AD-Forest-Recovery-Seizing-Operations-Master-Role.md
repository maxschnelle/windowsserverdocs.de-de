---
title: 'AD-Gesamtstruktur-Wiederherstellung: übernehmen eine Rolle des Betriebsschemamasters'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 7e6bb370-f840-4416-b5e2-86b0ba715f4f
ms.technology: identity-adds
ms.openlocfilehash: 1994d49652ee9eb10f6afc73cf5b4630b4718e77
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858461"
---
# <a name="ad-forest-recovery---seizing-an-operations-master-role"></a>Wiederherstellung der AD-Gesamtstruktur - Übernahme eine Betriebsmasterfunktion  

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Verwenden Sie das folgende Verfahren, um eine Betriebsmasterfunktion (auch bekannt als eine flexible single master Operation (FSMO)-Rolle) übernehmen. Sie können Ntdsutil.exe, ein Befehlszeilentool verwenden, die automatisch auf allen Domänencontrollern installiert wird.  
  
## <a name="to-seize-an-operations-master-role"></a>Um eine Betriebsmasterfunktion übernehmen  
  
1. Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie die EINGABETASTE:  

   ```  
   ntdsutil  
   ```  

2. Auf der **Ntdsutil:** aufgefordert, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE:  

   ```  
   roles  
   ```  

3. Auf der **FSMO-Wartung:** aufgefordert, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE:  

   ```  
   connections  
   ```  

4. Auf der **serververbindungen:** aufgefordert, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE:  

   ```  
   Connect to server ServerFQDN  
   ```  

   In denen *"ServerFQDN"* ist die vollqualifizierten Domänennamen (FQDN) dieses Domänencontrollers, z. B.: **Verbindung mit Server nycdc01.example.com**.  

   Wenn *"ServerFQDN"* nicht erfolgreich ist, verwenden Sie den NetBIOS-Namen des Domänencontrollers.  

5. Auf der **serververbindungen:** aufgefordert, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE:  

   ```  
   quit  
   ```  

6. Abhängig von der Rolle, die zu übernehmen, an die **FSMO-Wartung:** Eingabeaufforderung, geben Sie den entsprechenden Befehl aus, wie in der folgenden Tabelle beschrieben und dann die EINGABETASTE drücken.  
  
|Role-Eigenschaft|Anmeldeinformationen|Befehl|  
|----------|-----------------|-------------|  
|Domänennamenmaster|Organisations-Admins|**Übernehmen Sie Namensmaster**|  
|Schemamaster|Schema-Admins|**Übernehmen der Schemamaster**|  
|Infrastrukturmaster **beachten:**  Nachdem Sie die Infrastrukturmasterrolle, erhalten Fehler später Sie, wenn Sie Adprep/rodcprep ausführen müssen. Weitere Informationen finden Sie im Artikel KB [949257](https://support.microsoft.com/kb/949257).|Domänen-Admins|**Übernehmen Sie die Infrastruktur-master**|  
|PDC-Emulationsmaster|Domänen-Admins|**Übernehmen Sie die pdc**|  
|-RID-Master|Domänen-Admins|**Übernehmen Sie die rid-master**|  

Nachdem Sie die Anforderung bestätigt haben, versucht, Active Directory oder AD DS die Rolle nicht übertragen. Bei die Übertragung ein Fehler auftritt, einige Fehlerinformationen angezeigt wird, und Active Directory oder AD DS, die mit der Übernahme wird fortgesetzt. Nach der Übernahme abgeschlossen ist, wird eine Liste von Rollen und den Lightweight Directory Access Protocol (LDAP)-Namen des Servers, der derzeit jede Rolle enthält. Sie können auch ausführen **Netdom Query FSMO** eine Eingabeaufforderung mit erhöhten Rechten, um zu überprüfen, ob aktuelle Rolleninhaber.  
  
> [!NOTE]
> Wenn auf diesem Computer keine RID-Master vor Auftreten des Fehlers konnten, und Sie versuchen, übernehmen Sie die RID-Masterrolle, versucht der Computer mit einem Replikationspartner synchronisieren, bevor Sie dieser Rolle zu akzeptieren. Aber da dieser Schritt ausgeführt wird, wenn der Computer isoliert ist, ist es nicht erfolgreich in die Synchronisierung mit einem Partner. Aus diesem Grund wird ein Dialogfeld angezeigt, die fragt, ob Sie den Vorgang trotz dieser Computer nicht die Möglichkeit zum Synchronisieren mit einem Partner fortfahren möchten. Klicken Sie auf **Ja**.  
  
## <a name="next-steps"></a>Nächste Schritte

- [Für die Wiederherstellung des AD-Gesamtstruktur](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)

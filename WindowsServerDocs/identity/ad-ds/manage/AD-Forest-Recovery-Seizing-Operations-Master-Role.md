---
title: "Wiederherstellung des AD-Gesamtstruktur - Übernahme einer Betriebsmasterfunktion"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 7e6bb370-f840-4416-b5e2-86b0ba715f4f
ms.technology: identity-adfs
ms.openlocfilehash: 7ca6e3746586feeb3573b1ad6ba02831d1f5addd
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---seizing-an-operations-master-role"></a>Wiederherstellung des AD-Gesamtstruktur - Übernahme eine Betriebsmasterfunktion  

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2

 Verwenden Sie das folgende Verfahren, eine Betriebsmasterrolle (auch bekannt als eine flexible einfache Mastervorgänge (FSMO)-Rolle) übernehmen. Sie können Ntdsutil.exe, ein Befehlszeilentool, die automatisch auf alle Domänencontroller installiert ist.  
  
## <a name="to-seize-an-operations-master-role"></a>So übernehmen Sie die Funktion des Betriebsmasters  
  
1.  Geben Sie den folgenden Befehl an der Eingabeaufforderung, und drücken Sie dann die EINGABETASTE:  
  
    ```  
    ntdsutil  
    ```  
  
2.  Bei der **Ntdsutil:** aufgefordert, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE:  
  
    ```  
    roles  
    ```  
  
3.  Bei der **FSMO-Wartung:** aufgefordert, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE:  
  
    ```  
    connections  
    ```  
  
4.  Bei der **serververbindungen:** aufgefordert, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE:  
  
    ```  
    Connect to server ServerFQDN  
    ```  
  
     Wo *FQDN des Servers* ist die vollqualifizierten Domänennamen (FQDN) von diesem Domänencontroller, z.B.: **Verbinden mit Server nycdc01.example.com**.  
  
     Wenn *ServerFQDN* nicht erfolgreich ausgeführt werden kann, verwenden Sie den NetBIOS-Namen des Domänencontrollers.  
  
5.  Bei der **serververbindungen:** aufgefordert, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE:  
  
    ```  
    quit  
    ```  
  
6.  Abhängig von der Rolle, die Sie übernehmen möchten an die **FSMO-Wartung:** auffordern, geben Sie den entsprechenden Befehl ein, wie in der folgenden Tabelle beschrieben, und drücken Sie dann die EINGABETASTE.  
  
    |Rolle|Anmeldeinformationen|Befehl|  
    |----------|-----------------|-------------|  
    |Domänennamenmaster|Organisations-Admins|**Übernehmen der Domänennamenmaster gesucht**|  
    |Schemamaster|Schema-Admins|**Schemamaster übernehmen**|  
    |Infrastrukturmaster **Hinweis:** Nachdem Sie die Infrastrukturmasterrolle, erhalten Sie möglicherweise einen Fehler später ggf. zum Ausführen von Adprep /Rodcprep. Weitere Informationen finden Sie im KB-Artikel [949257](https://support.microsoft.com/kb/949257).|Domänen-Admins|**Infrastrukturmaster übernehmen**|  
    |PDC-Emulationsmasters|Domänen-Admins|**Übernehmen Sie für den primären Domänencontroller**|  
    |RID-master|Domänen-Admins|**Übernehmen Sie die RID-master**|  
  
     Nachdem Sie die Anforderung bestätigt haben, versucht, Active Directory oder AD DS die Rolle nicht übertragen. Bei die Übertragung ein Fehler auftritt, einige Fehlerinformationen angezeigt wird, und Active Directory oder AD DS, die mit der Übernahme wird fortgesetzt. Nachdem die Übernahme abgeschlossen ist, wird eine Liste von Rollen und der Lightweight Directory Access Protocol (LDAP)-Name des Servers, der derzeit für jede Rolle angezeigt. Sie können auch ausführen **Netdom Query FSMO** an einer Eingabeaufforderung mit erhöhten Funktionsinhaber überprüfen.  
  
    > [!NOTE]
    >  Wenn dieser Computer nicht vor Auftreten des Fehlers RID-Master konnte, und Sie versuchen, übernehmen Sie die RID-Masterrolle, versucht der Computer mit einem Replikationspartner zu synchronisieren, bevor Sie diese Rolle annehmen. Jedoch, da dieser Schrittausgeführt wird, wenn der Computer isoliert ist, wird dies nicht erfolgreich in die Synchronisierung mit einem Partner. Aus diesem Grund wird ein Dialogfeld angezeigt, die fragt, ob das Fortsetzen des Vorgangs trotz dieser Computer wird nicht mit einem Partner synchronisiert werden sollen. Klicken Sie auf **Ja**.  
  
## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)

---
title: "Wiederherstellung der Active Directory-Gesamtstruktur - Auslösen von RID-Pools"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c37bc129-a5e0-4219-9ba7-b4cf3a9fc9a4
ms.technology: identity-adfs
ms.openlocfilehash: e6b5dc8b9c0b701fe2cd1b0c88f7edc22802c393
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---raising-the-value-of-available-rid-pools"></a>Wiederherstellung des AD-Gesamtstruktur - auslösen den Wert des verfügbaren RID-Pools 

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2
 
 Verwenden Sie das folgende Verfahren, um den Wert von der RID (relative ID) auszulösen Pools, den RID-Betriebsmaster reservieren wird nach diesem DC wiederhergestellt wird. Durch das Auslösen des Wert des verfügbaren RID-Pools, können Sie sicherstellen, dass kein Domänencontroller RID für einen Sicherheitsprinzipal zuordnet, die nach der Sicherung erstellt wurde, die zum Wiederherstellen der Domänenbenutzers verwendet wurde.  
 
## <a name="about-active-directory-rid-pools-and-ridavailablepool"></a>Informationen zu Active Directory RID-Pools und rIDAvailablePool
 Jede Domäne verfügt über ein Objekt **CN = RID Manager$, CN = System, DC**=<*Domänenname*>. Dieses Objekt besitzt ein Attribut mit dem Namen **rIDAvailablePool**. Wert dieses Attributs wird den globalen RID-Raum für eine gesamte Domäne erhalten. Der Wert ist eine große ganze Zahl mit oberen und unteren teilen. Im oberen Bereich definiert die Anzahl der Sicherheitsprinzipale, die für jede Domäne (0x3FFFFFFF oder nur über 1 Milliarde) zugeordnet werden kann. Der untere Teil ist die Anzahl der RIDs, die in der Domäne zugewiesen wurden.  
  
> [!NOTE]
>  In Windows Server2016 und 2012 wird die Anzahl der Sicherheitsprinzipale, die zugeordnet werden kann, nur über 2 Milliarden erhöht. Weitere Informationen finden Sie unter [Verwalten von RID-Ausstellung](https://technet.microsoft.com/library/jj574229.aspx).  
  
-   Beispielwert: 4611686014132422708  
  
-   Unterer Teil: 2100 (Anfang der nächsten RID-Pool zugeordnet werden soll)  
  
-   Obere Teil: 1073741823 (Gesamtanzahl von RIDs, die in einer Domäne erstellt werden können)  
  
 Wenn Sie den Wert für die große ganze Zahl erhöhen, erhöhen Sie den Wert, der den unteren Teil. Wenn Sie die Beispielwert des 4611686014132422708 Summe 4611686014132522708 100.000 hinzufügen, ist das neue niedrige Teil z.B. 102100. Dies bedeutet, dass es sich bei der nächste RID-Pool, der durch den RID-Master zugeordnet werden, die mit 102100 anstelle von 2100 beginnen soll.  
  
### <a name="to-raise-the-value-of-available-rid-pools-using-adsiedit-and-the-calculator--"></a>Den Wert des verfügbaren RID-Pools mit Adsiedit und Rechner auslösen "  
1.  Öffnen Sie Server-Manager, klicken Sie auf **Tools**, und klicken Sie auf **ADSI Edit**.    
2.  Mit der rechten Maustaste, wählen **Verbinden mit** und verbinden Sie führen die Standard-Namenskontext und auf **OK**.
![ADSI-Bearbeitung](media/AD-Forest-Recovery-Raise-RID-Pool/adsi1.png) 
3. Navigieren Sie zu den folgenden DN-Pfad: **CN = RID Manager$, CN = System, DC =<domain name>**.
![ADSI-Bearbeitung](media/AD-Forest-Recovery-Raise-RID-Pool/adsi2.png) 
3.  Mit der rechten Maustaste und, und wählen Sie die Eigenschaften von CN = RID Manager$.  
4.  Wählen Sie das Attribut **rIDAvailablePool**, klicken Sie auf **bearbeiten**, und klicken Sie dann die große ganze Zahl in die Zwischenablage kopieren.
![ADSI-Bearbeitung](media/AD-Forest-Recovery-Raise-RID-Pool/adsi3.png)  
5.  Starten Sie Rechner, und von der **Ansicht** wählen Sie im Menü **wissenschaftlichen Modus**.  6.  Fügen Sie den aktuellen Wert 100.000 hinzu.  
![ADSI-Bearbeitung](media/AD-Forest-Recovery-Raise-RID-Pool/adsi4.png) 
7.  Mithilfe von STRG+c, oder die **Kopie** Befehl die **bearbeiten** im Menü den Wert in die Zwischenablage kopieren.  
8.  Wählen Sie im Dialogfeld "Bearbeiten" von Adsiedit fügen Sie den neuen Wert. 
![ADSI-Bearbeitung](media/AD-Forest-Recovery-Raise-RID-Pool/adsi5.png) 
9. Klicken Sie auf **OK** klicken Sie im Dialogfeld und **übernehmen** auf der Eigenschaftenseite zum Aktualisieren der **rIDAvailablePool** Attribut.  
  
### <a name="to-raise-the-value-of-available-rid-pools-using-ldp"></a>Den Wert des verfügbaren RID-Pools mithilfe von "Ldp" auslösen.  
  
1.  Geben Sie den folgenden Befehl an der Eingabeaufforderung, und drücken Sie dann die EINGABETASTE:  
  
     **"Ldp"**  
  
2.  Klicken Sie auf **Verbindung**, klicken Sie auf **verbinden**, geben Sie den Namen des RID-Manager, und klicken Sie dann auf **OK **.  
!["LDP"](media/AD-Forest-Recovery-Raise-RID-Pool/ldp1.png)
3.  Klicken Sie auf **Verbindung**, klicken Sie auf **binden**Option **Bindung mit Anmeldeinformationen** und geben Sie Ihre Administratoranmeldeinformationen, und klicken Sie dann auf **OK **.  
!["LDP"](media/AD-Forest-Recovery-Raise-RID-Pool/ldp2.png)
4.  Klicken Sie auf **Ansicht**, klicken Sie auf **Struktur** und geben Sie den folgenden DN-Pfad: CN = RID Manager$, CN = System, DC =*Domänennamen*  
!["LDP"](media/AD-Forest-Recovery-Raise-RID-Pool/ldp3.png)
5.  Klicken Sie auf **Durchsuchen**, und klicken Sie dann auf **ändern **.  
6.  Hinzufügen von 100.000 an den aktuellen **rIDAvailablePool** Wert, und geben Sie die Summe in **Werte **.  
7.  In **Dn**, Typ `cn=RID Manager$,cn=System,dc=`*< Domäne Tokentypen >*.  
8.  In **Attributeingabe bearbeiten**, Typ `rIDAvailablePool`.  
9. Wählen Sie **ersetzen** als Vorgang aus, und klicken Sie dann auf **EINGABETASTE **. </br>
!["LDP"](media/AD-Forest-Recovery-Raise-RID-Pool/ldp4.png) 
10. Klicken Sie auf **ausführen** den Vorgang auszuführen.  Klicken Sie auf **schließen **.
11. Um die Änderung zu überprüfen, klicken Sie auf **Ansicht**, klicken Sie auf **Struktur**, und geben Sie den folgenden DN-Pfad: CN = RID Manager$, CN = System, DC =*Domänennamen *.    Überprüfen Sie die **rIDAvailablePool** Attribut.  
!["LDP"](media/AD-Forest-Recovery-Raise-RID-Pool/ldp5.png)

## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)
 

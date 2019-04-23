---
title: 'AD-Gesamtstruktur-Wiederherstellung: Auslösen von RID-pools'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c37bc129-a5e0-4219-9ba7-b4cf3a9fc9a4
ms.technology: identity-adds
ms.openlocfilehash: c8f91226e10ea6681933d5a5dc00b92f5ab2179c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862981"
---
# <a name="ad-forest-recovery---raising-the-value-of-available-rid-pools"></a>AD-Gesamtstruktur-Wiederherstellung: Auslösen den Wert des verfügbaren RID-pools 

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Verwenden Sie das folgende Verfahren zum Auslösen des Werts von der relativen ID (RID) pools, dass nach der Wiederherstellung dieser Domänencontroller der RID-Betriebsmaster zuordnet. Erhöhen den Wert des verfügbaren RID-Pools, können Sie sicherstellen, dass kein DC eine RID für einen Sicherheitsprinzipal zugeordnet werden, die nach der Sicherung erstellt wurde, die zum Wiederherstellen der Domäne verwendet wurde. 

## <a name="about-active-directory-rid-pools-and-ridavailablepool"></a>Informationen zu Active Directory-RID-Pools und rIDAvailablePool

Jede Domäne verfügt über ein Objekt **CN = RID Manager$, CN = System, DC**=<*Domain_name*>. Dieses Objekt verfügt über ein Attribut namens **rIDAvailablePool**. Wert dieses Attributs verwaltet der globale RID-Raum für eine gesamte Domäne. Der Wert ist eine große Ganzzahl obere und untere teilen. Der obere Teil definiert die Anzahl der Sicherheitsprinzipale, die für jede Domäne (0x3FFFFFFF oder nur über 1 Milliarde) zugeordnet werden können. Im untere Teil ist die Anzahl der RIDs, die in der Domäne zugeordnet wurden. 
  
> [!NOTE]
> In Windows Server 2016 und 2012 wird die Anzahl der Sicherheitsprinzipale, die zugeordnet werden kann, etwas mehr als 2 Milliarden erhöht. Weitere Informationen finden Sie unter [der Verwaltung von RID-Ausstellung](https://technet.microsoft.com/library/jj574229.aspx). 
  
- Beispielwert: 4611686014132422708  
- Niedriger Teil: 2100 (Anfang des nächsten RID-Pools zugeordnet werden)  
- Oberen Teil: 1073741823 (Gesamtzahl von RIDs, die in einer Domäne erstellt werden kann)  
  
Wenn Sie den Wert, der die große ganze Zahl erhöhen, erhöhen Sie den Wert von der untere Bereich. Wenn Sie den Beispielwert, der 4611686014132422708 für die Summe der 4611686014132522708 100.000 hinzugefügt haben, ist der neue untere Bereich z. B. 102100. Dies bedeutet, dass es sich bei der nächsten RID-Pool, der vom RID-Master zugeordnet wird mit 102100 statt 2100 begonnen wird. 
  
### <a name="to-raise-the-value-of-available-rid-pools-using-adsiedit-and-the-calculator"></a>Den Wert des verfügbaren RID-Pools mithilfe von Adsiedit und der Rechner ausgelöst werden soll.

1. Öffnen Sie Server-Manager, klicken Sie auf **Tools** , und klicken Sie auf **ADSI Edit**.
2. Mit der rechten Maustaste, wählen **Herstellen einer Verbindung mit** , und verbinden Sie keinen Standard Namenskontext und auf **OK**.
   ![ADSI-Bearbeitung](media/AD-Forest-Recovery-Raise-RID-Pool/adsi1.png) 
3. Navigieren Sie in den folgenden distinguished Namenspfad: **CN=RID Manager$,CN=System,DC=<domain name>**.
   ![ADSI-Bearbeitung](media/AD-Forest-Recovery-Raise-RID-Pool/adsi2.png) 
3. Mit der rechten Maustaste, und wählen Sie die Eigenschaften von CN = RID Manager$. 
4. Wählen Sie das Attribut **rIDAvailablePool**, klicken Sie auf **bearbeiten**, und klicken Sie dann den Wert für die große ganze Zahl in die Zwischenablage zu kopieren.
   ![ADSI-Bearbeitung](media/AD-Forest-Recovery-Raise-RID-Pool/adsi3.png)  
5. Rechner, starten und von der **Ansicht** , wählen Sie im Menü **wissenschaftlichen Modus**. 
6. Fügen Sie auf den aktuellen Wert 100.000 hinzu.
   ![ADSI-Bearbeitung](media/AD-Forest-Recovery-Raise-RID-Pool/adsi4.png) 
7. Mit STRG + c, oder die **Kopie** Befehl die **bearbeiten** im Menü den Wert in die Zwischenablage zu kopieren. 
8. Fügen Sie im Dialogfeld "Bearbeiten" von Adsiedit den neuen Wert ein. 
   ![ADSI-Bearbeitung](media/AD-Forest-Recovery-Raise-RID-Pool/adsi5.png) 
9. Klicken Sie auf **OK** im Dialogfeld und **übernehmen** im Eigenschaftenblatt zum Aktualisieren der **rIDAvailablePool** Attribut. 
  
### <a name="to-raise-the-value-of-available-rid-pools-using-ldp"></a>Den Wert des verfügbaren RID-Pools mithilfe von "Ldp" ausgelöst werden soll.  
  
1. Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie die EINGABETASTE:  
   **ldp**  
2. Klicken Sie auf **Verbindung**, klicken Sie auf **Connect**, geben Sie den Namen des RID-Manager, und klicken Sie dann auf **OK**. 
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp1.png)
3. Klicken Sie auf **Verbindung**, klicken Sie auf **binden**Option **Bindung mit Anmeldeinformationen** und geben Sie Ihre Administratoranmeldeinformationen ein, und klicken Sie dann auf **OK**. 
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp2.png)
4. Klicken Sie auf **Ansicht**, klicken Sie auf **Struktur** und geben Sie dann den folgenden distinguished Namenspfad:  CN = RID Manager$, CN = System, DC =*Domänennamen*  
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp3.png)
5. Klicken Sie auf **Durchsuchen**, und klicken Sie dann auf **ändern**. 
6. Fügen Sie dem aktuellen 100.000 **rIDAvailablePool** Wert ein, und geben Sie die Summe in **Werte**. 
7. In **Dn**, Typ `cn=RID Manager$,cn=System,dc=` *< Domänenname\>*. 
8. In **Attributeingabe bearbeiten**, Typ `rIDAvailablePool`. 
9. Wählen Sie **ersetzen** als Vorgang aus, und klicken Sie dann auf **EINGABETASTE**.
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp4.png) 
10. Klicken Sie auf **ausführen** , den Vorgang auszuführen. Klicken Sie auf **Schließen**.
11. Um die Änderung zu überprüfen, klicken Sie auf **Ansicht**, klicken Sie auf **Struktur**, und geben Sie dann den folgenden distinguished Namenspfad:   CN = RID Manager$, CN = System, DC =*Domänennamen*.   Überprüfen Sie die **rIDAvailablePool** Attribut. 
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp5.png)

## <a name="next-steps"></a>Nächste Schritte

- [Für die Wiederherstellung des AD-Gesamtstruktur](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Gesamtstruktur der Active Directory - Prozeduren](AD-Forest-Recovery-Procedures.md)

---
title: 'AD-Gesamtstruktur Wiederherstellung: RID-Pools werden erhöht'
ms.author: iainfou
author: iainfoulds
manager: daveba
ms.date: 08/09/2018
ms.topic: article
ms.assetid: c37bc129-a5e0-4219-9ba7-b4cf3a9fc9a4
ms.openlocfilehash: 96e27aac4f63008c2ae694c2fe365d6391d3c949
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88941560"
---
# <a name="ad-forest-recovery---raising-the-value-of-available-rid-pools"></a>AD-Gesamtstruktur Wiederherstellung: erhöhen des Werts verfügbarer RID-Pools

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Verwenden Sie das folgende Verfahren, um den Wert der RID-Pools (relative ID) zu erhöhen, die der RID-Betriebs Master nach der Wiederherstellung des Domänen Controllers zuweist. Wenn Sie den Wert der verfügbaren RID-Pools erhöhen, können Sie sicherstellen, dass kein Domänen Controller eine Rid für einen Sicherheits Prinzipal zuweist, der nach der Sicherung erstellt wurde, die zum Wiederherstellen der Domäne verwendet wurde.

## <a name="about-active-directory-rid-pools-and-ridavailablepool"></a>Informationen zu Active Directory RID-Pools und ridavailablepool

Jede Domäne verfügt über das Objekt **CN = RID Manager $, CN = System, DC** =< *domain_name*>. Dieses Objekt verfügt über ein Attribut mit dem Namen **ridavailablepool**. Dieser Attribut Wert behält den globalen RID-Raum für eine gesamte Domäne bei. Der Wert ist eine große Ganzzahl mit oberen und unteren teilen. Der obere Teil definiert die Anzahl der Sicherheits Prinzipale, die für jede Domäne zugeordnet werden können (0x3fffffff oder direkt über 1 Milliarde). Der untere Teil ist die Anzahl der RIDs, die in der Domäne zugeordnet wurden.

> [!NOTE]
> In Windows Server 2016 und 2012 wird die Anzahl der Sicherheits Prinzipale, die zugewiesen werden können, auf einen Wert über 2 Milliarden festgestellt. Weitere Informationen finden Sie unter [Verwalten der RID-Ausstellung](./managing-rid-issuance.md).

- Beispiel Wert: 4611686014132422708
- Niedriger Teil: 2100 (Anfang des nächsten RID-Pools, der zugeordnet werden soll)
- Oberer Teil: 1073741823 (Gesamtzahl der RIDs, die in einer Domäne erstellt werden können)

Wenn Sie den Wert der großen Ganzzahl vergrößern, erhöhen Sie den Wert des unteren Teils. Wenn Sie z. b. 100.000 zum Beispiel Wert 4611686014132422708 für eine Summe von 4611686014132522708 hinzufügen, ist der neue niedrige Teil 102100. Dies weist darauf hin, dass der nächste RID-Pool, der vom RID-Master zugewiesen wird, mit 102100 anstelle von 2100 beginnt.

### <a name="to-raise-the-value-of-available-rid-pools-using-adsiedit-and-the-calculator"></a>So erhöhen Sie den Wert verfügbarer RID-Pools mithilfe von ADSIEdit und dem Rechner

1. Öffnen Sie Server-Manager, klicken Sie auf **Extras und dann auf** **ADSI-Bearbeitung**.
2. Klicken Sie mit der rechten Maustaste auf **Verbinden mit** , und verbinden Sie den Standard namens Kontext, und klicken Sie auf **OK**.
   ![ADSI-Editor](media/AD-Forest-Recovery-Raise-RID-Pool/adsi1.png)
3. Navigieren Sie zum folgenden Distinguished Name Path: **CN = RID Manager $, CN = System, DC = <domain name> **.
   ![ADSI-Editor](media/AD-Forest-Recovery-Raise-RID-Pool/adsi2.png)
3. Klicken Sie mit der rechten Maustaste, und wählen Sie die Eigenschaften CN = RID Manager $ aus.
4. Wählen Sie das Attribut **ridavailablepool**aus, klicken Sie auf **Bearbeiten**, und kopieren Sie dann den großen ganzzahligen Wert in die Zwischenablage.
   ![ADSI-Editor](media/AD-Forest-Recovery-Raise-RID-Pool/adsi3.png)
5. Starten Sie den Rechner, und wählen Sie im Menü **Ansicht** die Option **wissenschaftlicher Modus**aus.
6. Fügen Sie 100.000 zum aktuellen Wert hinzu.
   ![ADSI-Editor](media/AD-Forest-Recovery-Raise-RID-Pool/adsi4.png)
7. Wenn Sie Strg + c oder den Befehl **Kopieren** im Menü **Bearbeiten** verwenden, kopieren Sie den Wert in die Zwischenablage.
8. Fügen Sie im Dialogfeld "Bearbeiten" von ADSIEdit den neuen Wert ein.
   ![ADSI-Editor](media/AD-Forest-Recovery-Raise-RID-Pool/adsi5.png)
9. Klicken **OK** Sie im Dialogfeld auf OK **, und über** nehmen Sie das Eigenschaften Blatt, um das **ridavailablepool** -Attribut zu aktualisieren.

### <a name="to-raise-the-value-of-available-rid-pools-using-ldp"></a>So erhöhen Sie den Wert der verfügbaren RID-Pools mithilfe von LDP

1. Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE: **LDP** .
2. Klicken Sie auf **Verbindung**, auf **verbinden**, geben Sie den Namen des RID-Managers ein, und klicken Sie dann auf **OK**.
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp1.png)
3. Klicken Sie auf **Verbindung**und dann auf **binden**, wählen Sie **mit Anmelde Informationen binden** aus, und geben **Sie Ihre**Administrator Anmelde Informationen ein.
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp2.png)
4. Klicken Sie auf **Ansicht**, klicken **Sie auf Struktur, und geben** Sie dann den folgenden Distinguished Name-Pfad ein: CN = RID Manager $, CN = System, DC =*Domänen Name* 
    ![ LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp3.png)
5. Klicken Sie auf **Durchsuchen**und dann auf **ändern**.
6. Fügen Sie 100.000 zum aktuellen **ridavailablepool** -Wert hinzu, und geben Sie dann die Summe in **Werte**ein.
7. Geben **Dn**Sie in DN `cn=RID Manager$,cn=System,dc=` *<Domänen \> Namen*ein.
8. Geben Sie unter **Eingabe Attribut bearbeiten**den Namen ein `rIDAvailablePool` .
9. Wählen Sie als Vorgang **ersetzen** aus, und drücken Sie dann die **Eingabe**Taste.
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp4.png)
10. Klicken Sie auf **Ausführen** , um den Vorgang auszuführen. Klicken Sie auf **Schließen**.
11. Klicken Sie zum Überprüfen der Änderung auf **Ansicht**, klicken **Sie auf Struktur, und**geben Sie dann den folgenden Distinguished Name-Pfad ein: CN = RID-Manager $, CN = System, DC =*Domänen Name*.   Überprüfen Sie das **ridavailablepool** -Attribut.
   ![LDP](media/AD-Forest-Recovery-Raise-RID-Pool/ldp5.png)

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)

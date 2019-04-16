---
ms.assetid: 4d21d27d-5523-4993-ad4f-fbaa43df7576
title: Erweiterte AD DS-Verwaltung mit dem Active Directory-Verwaltungscenter (Stufe 200)
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 19e83ce0123bd484c61d5a4522ebdd90cd40241e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="advanced-ad-ds-management-using-active-directory-administrative-center-level-200"></a>Erweiterte AD DS-Verwaltung mit dem Active Directory-Verwaltungscenter (Stufe 200)

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema behandelt das aktualisierte Active Directory Administrative Center mit den neuen Active Directory-Papierkorb, differenzierten Kennwortrichtlinien und Windows PowerShell-Verlaufsanzeige im Detail, inklusive Architektur, Beispielen für gängige Aufgaben und Informationen zur Problembehandlung. Eine Einführung finden Sie unter [Introduction to Active Directory Administrative Center Enhancements & #40; Stufe 100 & #41; ](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md).  
  
-   [Active Directory-Verwaltungscenter-Architektur](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_Arch)  
  
-   [Aktivieren und Verwalten von Active Directory-Papierkorbs im Active Directory-Verwaltungscenter](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_EnableRecycleBin)  
  
-   [Konfigurieren und Verwalten von differenzierten Kennwortrichtlinien mit Active Directory-Verwaltungscenter](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_FGPP)  
  
-   [Mithilfe der Active Directory-Verwaltungscenter Windows PowerShell-Verlaufsanzeige](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_HistoryViewer)  
  
-   [Problembehandlung bei AD DS-Verwaltung](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_Tshoot)  
  
## <a name="BKMK_Arch"></a>Active Directory-Verwaltungscenter-Architektur  
  
### <a name="adprep-executables-dlls"></a>Ausführbare ADPrep-Dateien, DLL-Dateien  
Das Modul und zugrunde liegende Architektur des Active Directory-Verwaltungscenters wurde mit dem neuen Papierkorb, FGPP und Verlaufsanzeige nicht geändert.  
  
-   Microsoft.ActiveDirectory.Management.UI.dll  
  
-   Microsoft.ActiveDirectory.Management.UI.resources.dll  
  
-   Microsoft.ActiveDirectory.Management.dll  
  
-   Microsoft.ActiveDirectory.Management.resources.dll  
  
-   ActiveDirectoryPowerShellResources.dll  
  
Die zugrunde liegende Windows PowerShell und Operationsebene für die neuen Papierkorb-Funktionalität sind im folgenden dargestellt:  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/adds_adrestore.png)  
  
## <a name="BKMK_EnableRecycleBin"></a>Aktivieren und Verwalten von Active Directory-Papierkorbs im Active Directory-Verwaltungscenter  
  
### <a name="capabilities"></a>Funktionen  
  
-   Die Windows Server 2012 Active Directory-Verwaltungscenter können Sie konfigurieren und Verwalten der Active Directory-Papierkorb für beliebige Domänenpartitionen in einer Gesamtstruktur. Es ist nicht mehr erforderlich, verwenden Sie Windows PowerShell oder Ldp.exe zum Aktivieren der Active Directory-Papierkorb oder Wiederherstellen von Objekten in Domänenpartitionen.  
  
-   Das Active Directory-Verwaltungscenter bietet erweiterte Filterkriterien und erleichtert gezielte Wiederherstellung in großen Umgebungen mit vielen absichtlich gelöschten Objekten.  
  
### <a name="limitations"></a>Einschränkungen  
  
-   Da das Active Directory-Verwaltungscenter nur Domänenpartitionen verwaltet werden, kann nicht gelöschte Objekte aus der Konfiguration, DNS-Domäne oder Gesamtstruktur-DNS-Partitionen wiederherstellen (Sie können keine Objekte aus der Schemapartition löschen). Verwenden Sie zum Wiederherstellen von Objekten aus nicht-Domänenpartitionen [Restore-ADObject](https://technet.microsoft.com/library/ee617262.aspx).  
  
-   Das Active Directory-Verwaltungscenter können keine Unterstrukturen von Objekten in einer einzigen Aktion wiederherstellen. Beispielsweise, wenn Sie eine OU mit verschachtelten OUs, Benutzer, Gruppen und Computer löschen, wird beim Wiederherstellen der Stamm-OU nicht die untergeordneten Objekte wiederhergestellt.  
  
    > [!NOTE]  
    > Die Wiederherstellung der Active Directory-Verwaltungscenter-Stapel wird ein "Höchstleistung" Sortierung der gelöschten Objekte *in die Auswahl nur* damit Eltern, bevor Sie die untergeordneten Elemente der Liste Wiederherstellen angeordnet werden. In einfachen Testfällen möglicherweise Unterstrukturen von Objekten in einer einzigen Aktion wiederhergestellt werden. Aber für Sonderfälle wie z. B. eine Auswahl, die enthält Teilstrukturen - Strukturen, in denen einige der gelöschten übergeordneten Knoten fehlen- oder für Sonderfälle wie z. B. die untergeordneten Objekte zu überspringen, wenn die Wiederherstellung übergeordneter Elemente fehlschlägt, funktioniert möglicherweise nicht wie erwartet. Aus diesem Grund sollten Sie Unterstrukturen von Objekten als separate Aktion auf immer wiederherstellen, nachdem Sie die übergeordneten Objekte wiederhergestellt haben.  
  
Active Directory-Papierkorb benötigt eine Windows Server 2008 R2 Gesamtstrukturfunktionsebene, und Sie müssen ein Mitglied der Gruppe "Organisations-Admins" sein. Nach der Aktivierung können Sie Active Directory-Papierkorb nicht deaktivieren. Active Directory-Papierkorb erhöht die Größe des Active Directory-Datenbank (NTDS. DIT) auf jedem Domänencontroller in der Gesamtstruktur. Vom Papierkorb verwendete Speicherplatz wird weiterhin mit der Zeit zunehmen, Objekte und all ihren Attributdaten bleiben erhalten.  
  
Weitere Informationen finden Sie unter [Active Directory schrittweise Anleitung zum Papierkorb](https://technet.microsoft.com/library/dd392261(v=WS.10).aspx) und [Bewerten von Hardwareanforderungen (für Active Directory-Papierkorb)](https://technet.microsoft.com/library/cc753439(WS.10).aspx).  
  
Sie können *niedrigeren* der Gesamtstruktur und Domäne Funktionsebenen von Windows Server 2012 für Windows Server 2008 R2 auch nach der Aktivierung der Active Directory-Papierkorb. Dies erfordert, dass Sie verwenden die **Set-ADForestMode** und **Set-ADDomainMode** Active Directory-Cmdlets.  
  
Zum Beispiel:  
  
```  
Set-AdForestMode -identity corp.contoso.com -server dc1.corp.contoso.com -forestmode Windows2008R2Forest  
Set-AdDomainMode -identity research.corp.contoso.com -server dc3.research.corp.contoso.com -domainmode Windows2008R2Domain  
  
```  
  
Sie können das Active Directory-Verwaltungscenter verwenden, um diese Änderung - Funktionsebenen nur ausgelöst.  
  
### <a name="enabling-active-directory-recycle-bin-using-active-directory-administrative-center"></a>Aktivieren der Active Directory-Papierkorbs im Active Directory-Verwaltungscenter  
Um den Active Directory-Papierkorb zu aktivieren, öffnen Sie die **Active Directory Administrative Center** , und klicken Sie auf den Namen Ihrer Gesamtstruktur klicken Sie im Navigationsbereich. Von der **Aufgaben** Bereich, klicken Sie auf **Papierkorb aktivieren**.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_EnableRecycleBin.png)  
  
Das Active Directory-Verwaltungscenter zeigt die **Papierkorbaktivierung bestätigen** Dialogfeld. Dieses Dialogfeld weist Sie die Aktivierung des Papierkorbs rückgängig gemacht werden. Klicken Sie auf **OK** der Active Directory-Papierkorb zu aktivieren. Das Active Directory-Verwaltungscenter zeigt ein weiteres Dialogfeld Sie daran erinnern, dass die Active Directory-Papierkorb nicht voll funktionsfähig ist, bis alle Domänencontroller der Änderung der Konfiguration replizieren.  
  
> [!IMPORTANT]  
> Die Option zum Aktivieren der Active Directory-Papierkorb ist nicht verfügbar, wenn:  
>   
> -   Funktionsebene der Gesamtstruktur ist kleiner als Windows Server 2008 R2  
> -   Es ist bereits aktiviert.  
  
Das entsprechende Active Directory Windows PowerShell-Cmdlet ist:  
  
```  
Enable-ADOptionalFeature  
```  
  
Weitere Informationen zur Verwendung von Windows PowerShell zum Aktivieren der Active Directory-Papierkorb finden Sie unter der [Active Directory schrittweise Anleitung zum Papierkorb](https://technet.microsoft.com/library/dd392261(v=WS.10).aspx).  
  
### <a name="managing-active-directory-recycle-bin-using-active-directory-administrative-center"></a>Verwalten von Active Directory-Papierkorbs im Active Directory-Verwaltungscenter  
In diesem Abschnittwird das Beispiel einer vorhandenen Domäne mit dem Namen **corp.contoso.com**. In dieser Domäne sind Benutzer in eine übergeordnete OU mit dem Namen **UserAccounts**. Die **UserAccounts** Organisationseinheit enthält drei untergeordnete OUs mit den Abteilungsnamen, die jeweils weitere OUs, Benutzer und Gruppen enthalten.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_EnableRecycleBinExampleOU.png)  
  
#### <a name="storage-and-filtering"></a>Speicherung und Filterung  
Der Active Directory-Papierkorb bewahrt alle Objekte in der Gesamtstruktur gelöscht. Er speichert diese Objekte werden gemäß der **MsDS-DeletedObjectLifetime** -Attribut, das standardmäßig festgelegt ist, entsprechen die **TombstoneLifetime** -Attribut der Gesamtstruktur. In jeder Gesamtstruktur erstellten mithilfe von Windows Server 2003 SP1 oder höher der Wert der **TombstoneLifetime** ist standardmäßig auf 180 Tage festgelegt. In jeder Gesamtstruktur ein Upgrade von Windows 2000 oder Windows Server 2003 (ohne Servicepack) installiert das TombstoneLifetime-Standardattribut nicht festgelegt ist und Windows verwendet daher den internen Standardwert von 60 Tagen. All dies ist konfigurierbar. Das Active Directory-Verwaltungscenter können Sie aus den Domänenpartitionen der Gesamtstruktur Gelöschte Objekte wiederherzustellen. Sie müssen weiterhin das Cmdlet **Restore-ADObject** zum Wiederherstellen gelöschter Objekte aus anderen Partitionen, z. B. die Konfiguration der Active Directory-Papierkorb macht die **Gelöschte Objekte** Container Partitionen im Active Directory-Verwaltungscenter sichtbar.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_DeletedObjectsContainer.png)  
  
Die **Gelöschte Objekte** -Container enthält alle wiederherstellbaren Objekte der jeweiligen Domänenpartition. Stellen Sie gelöschte Objekte, die älter als **MsDS-DeletedObjectLifetime** werden als wiederverwendete Objekte bezeichnet. Das Active Directory-Verwaltungscenter wiederverwendete Objekte nicht angezeigt, und diese Objekte mit dem Active Directory-Verwaltungscenter können nicht wiederhergestellt werden.  
  
Eine detailliertere Beschreibung von Architektur und Verarbeitungsregeln des Papierkorbs, finden Sie unter [The AD Recycle Bin: Understanding, implementieren, bewährte Methoden und Problembehandlung](http://blogs.technet.com/b/askds/archive/2009/08/27/the-ad-recycle-bin-understanding-implementing-best-practices-and-troubleshooting.aspx).  
  
Das Active Directory-Verwaltungscenter beschränkt künstlich die Standardanzahl der Objekte auf 20.000 pro Container zurückgegebenen. Sie können dieses Limit maximal 100.000 anheben auslösen, indem Sie auf die **verwalten** klicken Sie dann im Menü **Verwaltungslistenoptionen**.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_MgmtList.png)  
  
#### <a name="restoration"></a>Wiederherstellung  
  
##### <a name="filtering"></a>Filtern  
Active Directory-Verwaltungscenter bietet umfassende Kriterien und Filteroptionen, denen Sie mit vertraut werden soll, bevor Sie sie in einer tatsächlichen Wiederherstellung verwenden müssen. Domänen löschen absichtlich viele Objekte über die Lebensdauer. Mit einer wahrscheinlich gelöschten Objektlebensdauer von 180 Tagen kann nicht einfach alle Objekte bei der Wiederherstellung Unfall auftritt.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_AddCriteria.png)  
  
Anstatt komplexe LDAP-Filter schreiben und UTC-Werte in Datums- und Uhrzeitangaben konvertieren, verwenden Sie die grundlegenden und erweiterten **Filter** Menü, um nur relevante Objekte aufzulisten. Wenn Sie den Tag der Löschung, die Namen von Objekten oder andere Schlüsseldaten kennen, verwenden Sie, beim Filtern von Vorteil. Setzen Sie die erweiterten Filteroptionen, indem Sie auf das Chevron neben dem Suchfeld.  
  
Die Wiederherstellung unterstützt alle Standardoptionen Kriterien Optionen, das gleiche wie jede andere Suche. Integrierte Filter sind in der Regel die wichtigsten Ziele für das Wiederherstellen von Objekten:  
  
-   *ANR (Auflösung mehrdeutiger Namen - nicht aufgeführt, klicken Sie im Menü, aber verwendet, wenn die Eingabe in die *** Filter *** Feld)*  
  
-   Zuletzt zwischen den angegebenen Datumswerten geändert  
  
-   Objekt ist User/Inetorgperson/Computer/Group/Organisation  
  
-   Name  
  
-   Beim Löschen  
  
-   Letztes bekanntes übergeordnetes Element  
  
-   Typ  
  
-   Beschreibung  
  
-   Stadt  
  
-   Land/Region  
  
-   Abteilung  
  
-   Mitarbeiter-ID  
  
-   Vorname  
  
-   Position  
  
-   Nachname  
  
-   "SAMAccountName"  
  
-   Bundesland/Kanton  
  
-   Telefonnummer  
  
-   UPN  
  
-   PLZ/Postleitzahl  
  
Sie können mehrere Kriterien hinzufügen. Beispielsweise finden Sie alle Benutzerobjekte gelöscht am 24. September<sup>th</sup> 2012 aus Chicago, Illinois mit der Berufsbezeichnung Manager.  
  
Sie können auch hinzufügen, ändern Sie oder neu anzuordnen Sie die Spaltenüberschriften, um weitere Informationen bereitgestellt, wenn Sie die wiederherzustellenden Objekte zu bewerten.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ColumnHeaders.png)  
  
Weitere Informationen zur Auflösung mehrdeutiger Namen finden Sie unter [ANR-Attribute](https://msdn.microsoft.com/library/ms675092(VS.85).aspx).  
  
##### <a name="single-object"></a>Einzelnes Objekt  
Wiederherstellen gelöschter Objekte war schon immer eine einzelne Operation.  Das Active Directory-Verwaltungscenter vereinfacht diese Operation. So stellen Sie ein gelöschtes Objekt, z. B. einen einzelnen Benutzer wieder her:  
  
1.  Klicken Sie auf den Domänennamen, klicken Sie im Navigationsbereich des Active Directory-Verwaltungscenter.  
  
2.  Doppelklicken Sie auf **Gelöschte Objekte** in der Verwaltungsliste angezeigt.  
  
3.  Maustaste auf das Objekt, und klicken Sie dann auf **wiederherstellen**, oder klicken Sie auf **wiederherstellen** aus der **Aufgaben** Bereich.  
  
Das Objekt wird an ihrem ursprünglichen Speicherort wiederhergestellt.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestoreSingle.gif)  
  
Klicken Sie auf **wiederherstellen... ** Speicherort für die Wiederherstellung zu ändern. Dies ist hilfreich, wenn der übergeordnete Container des gelöschten Objekts ebenfalls gelöscht wurde, jedoch nicht das übergeordnete Element wiederherstellen möchten.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestoreToSingle.gif)  
  
##### <a name="multiple-peer-objects"></a>Mehrere Objekte auf derselben Ebene  
Sie können mehrere Peer-Objekte auf, z. B. alle Benutzer in einer Organisationseinheit wiederherstellen. Halten Sie die STRG-Taste gedrückt, und klicken Sie auf eine oder mehrere Gelöschte Objekte, die Sie wiederherstellen möchten. Klicken Sie auf **wiederherstellen** über den Aufgabenbereich. Sie können alle angezeigten Objekte auch auswählen, indem Sie die STRG-Taste und eine Taste gedrückt halten oder einen Bereich von Objekten per UMSCHALTTASTE und Klick.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestorePeers.png)  
  
##### <a name="multiple-parent-and-child-objects"></a>Mehrere über- und untergeordnete Objekte  
Es ist wichtig, um den Wiederherstellungsprozess für eine Wiederherstellung mehrere über-und untergeordnete zu verstehen, da das Active Directory-Verwaltungscenter verschachtelte Strukturen gelöschter Objekte mit einer einzigen Aktion wiederhergestellt werden kann.  
  
1.  Wiederherstellen der oberste Objekt in einer Struktur.  
  
2.  Stellen Sie die direkt untergeordneten Objekte dieses übergeordneten Objekts wieder her.  
  
3.  Stellen Sie die direkt untergeordneten Objekte dieser übergeordneten Objekte wieder her.  
  
4.  Wiederholen Sie ggf., bis alle Objekte wiederherstellen.  
  
Sie können kein untergeordnetes Objekt vor der Wiederherstellung des übergeordnete Element wiederherstellen. Es wird versucht, diese Wiederherstellung wird der folgende Fehler:  
  
**Der Vorgang konnte nicht ausgeführt werden, da das übergeordnete Objekt instanziiert oder gelöscht wurde.**  
  
Die **Letztes bekanntes übergeordnetes Element** Attribut zeigt die übergeordnete Beziehung des jeweiligen Objekts. Die **Letztes bekanntes übergeordnetes Element** Attribut aus dem gelöschten Speicherort löschort zum Wiederherstellungsort ändert, wenn Sie das Active Directory-Verwaltungscenter nach der Wiederherstellung eines übergeordneten Elements aktualisieren. Aus diesem Grund können Sie das untergeordnete Objekt wiederherstellen, wenn der Speicherort des übergeordneten Objekts der distinguished Name des Containers Gelöschte Objekte nicht mehr angezeigt.  
  
Nehmen wir ein Szenario, in dem ein Administrator versehentlich die Sales-OU löscht untergeordneten OUs und Benutzer enthält.  
  
Achten Sie zuerst den Wert der der **Letztes bekanntes übergeordnetes Element** -Attribut für alle gelöschten Benutzer und wie es liest * *OU = Sales\0ADEL:*< Guid + Objektcontainers definierter Name >***:  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParent.gif)  
  
Filtern der mehrdeutigen Namen "Sales" auf die gelöschte OU anzuzeigen und wiederherzustellen:  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSales.png)  
  
Aktualisieren Sie die Active Directory-Verwaltungscenter zum Ändern der wiederhergestellten OU "Sales" definierten Namen der gelöschten Benutzerobjekte Letztes bekanntes übergeordnetes Element-Attribut finden Sie unter:  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSalesRestored.gif)  
  
Filter für alle Verkäufe Benutzer. Halten Sie die STRG-Taste und einen Schlüssel alle gelöschten Verkäufe Benutzer auswählen. Klicken Sie auf **wiederherstellen** so verschieben Sie Objekte aus der **Gelöschte Objekte** Container auf die OU "Sales" Gruppenmitgliedschaften und Attribute intakt.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSalesUndelete.png)  
  
Wenn die **Sales** Organisationseinheit enthalten untergeordnete OUs enthält einen eigenen und dann würden Sie zuerst ihre Kinder vor dem Wiederherstellen von untergeordneten OUs wiederherstellen, und so weiter.  
  
Zum Wiederherstellen aller verschachtelten Objekte durch Angabe eines gelöschten übergeordneten Containers finden Sie unter [Anhang B: Wiederherstellen mehrerer gelöschte Active Directory-Objekte (Beispielskript)](https://technet.microsoft.com/library/dd379504(WS.10).aspx).  
  
Das Active Directory Windows PowerShell-Cmdlet zum Wiederherstellen gelöschter Objekte ist:  
  
```  
Restore-adobject  
  
```  
  
Die **Restore-ADObject** die Funktionen der Cmdlets haben sich nicht zwischen Windows Server 2008 R2 und Windows Server 2012 geändert.  
  
##### <a name="server-side-filtering"></a>Serverseitige Filterung  
Es ist möglich, dass Container der gelöschten Objekte wird im Laufe der Zeit über 20.000 (oder sogar 100.000) Objekte in mittelgroßen und großen Unternehmen gesammelt und Anzeige aller Objekte haben. Da der Filtermechanismus in Active Directory-Verwaltungscenter clientseitig Filtern nutzt, kann nicht diese zusätzlichen Objekte angezeigt werden. Diese Einschränkung zu umgehen, verwenden Sie die folgenden Schritte aus, um eine serverseitige Suche durchführen:  
  
1.  Klicken Sie mit der rechten Maustaste auf die **Gelöschte Objekte** Container, und klicken Sie dann auf **unter diesem Knoten suchen**.  
  
2.  Klicken Sie auf das Chevron verfügbar machen die **+ Kriterien hinzufügen** Menü auswählen und hinzufügen **zwischen zuletzt angegebenen Datumswerten geändert**. Zeitpunkt der letzten Änderung (die **Änderungszeitpunkt** Attribut) ist eine Annäherung des Löschzeitpunkts; in den meisten Umgebungen sind identisch. Diese Abfrage führt eine serverseitige Suche.  
  
3.  Suchen Sie nach der gelöschten Objekte mithilfe von Filterung, Sortierung, usw. in den Ergebnissen wiederherstellen und stellen sie dann normal.  
  
## <a name="BKMK_FGPP"></a>Konfigurieren und Verwalten von differenzierten Kennwortrichtlinien mit Active Directory-Verwaltungscenter  
  
### <a name="configuring-fine-grained-password-policies"></a>Konfigurieren fein abgestimmter Kennwortrichtlinien  
Das Active Directory-Verwaltungscenter können Sie zum Erstellen und Verwalten der differenzierten Kennwort Richtlinie (FGPP)-Objekte. Windows Server 2008 eingeführt, das FGPP-Feature, aber Windows Server 2012 hat die erste grafische Verwaltungsoberfläche für sie. Sie fein abgestimmte Kennwortrichtlinien auf Domänenebene angewendet, und es ermöglicht das Überschreiben der von Windows Server 2003 benötigte einzelne Domänenkennwort. Erstellen Sie unterschiedliche FGPP mit unterschiedlichen Einstellungen, Abrufen einzelner Benutzer oder Gruppen Kennwortrichtlinien in einer Domäne.  
  
Informationen zu fein abgestimmten Kennwortrichtlinien finden Sie unter [abgestimmter Kennwort- und Kontosperrungsrichtlinien Step-by-Step Guide (Windows Server2008 R2)](https://technet.microsoft.com/library/cc770842(WS.10).aspx).  
  
Klicken Sie im Navigationsbereich, klicken Sie Strukturansicht klicken Sie auf Ihrer Domäne **System**, klicken Sie auf **Password Settings Container**, und klicken Sie dann im Aufgabenbereich auf **neu** und **Kennworteinstellungen**.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_PasswordSettings.png)  
  
### <a name="managing-fine-grained-password-policies"></a>Verwalten fein abgestimmter Kennwortrichtlinien  
FGPPS erstellen oder Bearbeiten einer vorhandenen zeigt die **Kennworteinstellungen** Editor. Hier konfigurieren Sie alle gewünschten Kennwortrichtlinien, wie Sie in Windows Server 2008 oder WindowsServer 2008 R2, nur jetzt mit einem speziell dafür entwickelten Editor müssten.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_CreatePasswordSettings.png)  
  
Füllen Sie alle Pflichtfelder (rotes Sternchen) und optionalen Felder aus, und klicken Sie dann auf **hinzufügen** festlegen, die Benutzer oder Gruppen, die diese Richtlinie gelten soll. FGPP überschreibt Domäne Standardeinstellungen für diese angegebenen Sicherheitsprinzipale. In der Abbildung oben ist gilt eine extrem restriktive Richtlinie nur für das integrierte Administratorkonto, um dessen Sicherheit zu. Die Richtlinie ist viel zu komplex für Standardbenutzer einhalten, jedoch ist perfekt für ein mit hohem Risiko-Konto nur von IT-Spezialisten verwendet.  
  
Sie auch Vorrang vor und festlegen, welche Benutzer und Gruppen die Richtlinie angewendet wird, innerhalb einer bestimmten Domäne.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_Precedence.png)  
  
Die Active Directory Windows PowerShell-Cmdlets für fein abgestimmte Kennwortrichtlinien sind:  
  
```  
Add-ADFineGrainedPasswordPolicySubject  
Get-ADFineGrainedPasswordPolicy  
Get-ADFineGrainedPasswordPolicySubject  
New-ADFineGrainedPasswordPolicy  
Remove-ADFineGrainedPasswordPolicy  
Remove-ADFineGrainedPasswordPolicySubject  
Set-ADFineGrainedPasswordPolicy  
  
```  
  
Differenzierte Kennwortrichtlinien Cmdlet-Funktionen wurden zwischen dem Windows Server 2008 R2 und Windows Server 2012 nicht geändert. Aus Gründen der Einfachheit Diagramm das folgende die zugeordneten Argumente für Cmdlets:  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_FGPP.gif)  
  
Das Active Directory-Verwaltungscenter können Sie das Richtlinienergebnissatz-FGPP-Sets für einen bestimmten Benutzer suchen. Klicken Sie mit der rechten Maustaste auf alle Benutzer, und klicken Sie auf **resultierende Kennworteinstellungen... ** zum Öffnen der *Kennworteinstellungen* Seite, die durch implizite oder explizite Zuweisung des jeweiligen Benutzers gilt:  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RSOP.png)  
  
Untersuchen der **Eigenschaften** für alle Benutzer und Gruppen werden die **direkt zugeordneten Kennworteinstellungen**, die explizit zugewiesene FGPPs sind:  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_FGPPSettings.gif)  
  
Implizite FGPP-Zuweisung wird hier nicht angezeigt. Sie müssen, verwenden die **resultierende Kennworteinstellungen... ** Option.  
  
## <a name="BKMK_HistoryViewer"></a>Mithilfe der Active Directory-Verwaltungscenter Windows PowerShell-Verlaufsanzeige  
Die Zukunft von Windows-Verwaltung ist Windows PowerShell. Verwaltung komplexer verteilter Systeme wird durch grafische Tools, die Überlagerung auf eine Aufgabe Benutzeroberflächenautomatisierungs-Framework einheitliche und effiziente zu. Sie müssen verstehen, wie Windows PowerShell funktioniert, um volles Potenzial auszuschöpfen und Ihren IT-Investitionen zu maximieren.  
  
Das Active Directory-Verwaltungscenter bietet nun eine komplette Verlaufsanzeige für alle Windows PowerShell-Cmdlets ausgeführt werden soll und deren Argumente und Werte. Sie können den Cmdlet-Verlauf an anderer Stelle für die Untersuchung oder Änderung und die Wiederverwendung kopieren. Sie können die Aufgabe Notizen isolieren welche Ihrer Active Directory Administrative Center bei, dass Befehle in Windows PowerShell hat zu erstellen. Sie können auch den Verlauf aus, um die Punkte herauszustellen filtern.  
  
Die Active Directory Administrative Center Windows PowerShell-Verlaufsanzeige des dient Sie sich über praktische Erfahrung vertraut machen.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_HistoryViewer.gif)  
  
Klicken Sie auf das Chevron (Pfeil), um Windows PowerShell History Viewer angezeigt.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RaiseViewer.png)  
  
Anschließend erstellen Sie einen Benutzer oder ändern Sie die Mitgliedschaft einer Gruppe. Die Verlaufsanzeige wird fortlaufend mit einer reduzierten Ansicht der einzelnen Cmdlets, die mit der angegebenen Argumente das Active Directory-Verwaltungscenter ausgeführt wurden aktualisiert.  
  
Erweitern Sie von Interesse für alle Werte, die bereitgestellt, um die Cmdlet-Argumente finden Sie unter:  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ViewArgs.png)  
  
Klicken Sie auf die **Aufgabe** Menü, um eine Notation manuell einzugeben erstellen, bevor Sie die Active Directory-Verwaltungscenter erstellen, ändern oder Löschen eines Objekts verwenden. Geben Sie in was Sie getan haben.  Wählen Sie nach dem Abschluss der Änderung **Task beenden**. Die Aufgabe Notiz gruppiert alle ausgeführten Aktionen in einer reduzierbaren Notiz ausgeführt, wenn Sie zum besseren Verständnis verwenden können.  
  
Geben Sie beispielsweise Folgendes ein, um die WindowsPowerShell-Befehle verwendet, um das Kennwort eines Benutzers zu ändern und ihn aus einer Gruppe entfernen:  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RemoveUser.gif)  
  
Alle anzeigen das Kontrollkästchen auch zeigt Get-* Verb Windows PowerShell-Cmdlets, die nur Daten abrufen.  
  
![Erweiterte AD DS-Verwaltung](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ShowAll.png)  
  
Die Verlaufsanzeige enthält die exakten Befehle ausführen, indem Sie das Active Directory-Verwaltungscenter und möglicherweise Beachten Sie, dass manche Cmdlets unnötigerweise ausgeführt. Beispielsweise können Sie einen neuen Benutzer mit erstellen:  
  
```  
new-aduser   
```  
  
und müssen nicht verwenden:  
  
```  
set-adaccountpassword  
enable-adaccount  
set-aduser  
  
```  
  
Der Active Directory-Verwaltungscenters Design erforderlichen Code-Nutzung und Modularität. Daher statt eine Reihe von Funktionen, die neue Benutzer erstellt, und eine andere Gruppe, die vorhandene Benutzer ändern, es minimal werden die einzelnen Funktionen, und die Cmdlets dann verkettet. Berücksichtigen Sie dies, wenn Sie Active Directory Windows PowerShell reflektiert werden. Sie können auch verwenden, die als Verfahren lernen, sehen Sie, wie einfach Sie Windows PowerShell verwenden können, um eine einzelne Aufgabe abzuschließen.  
  
## <a name="BKMK_Tshoot"></a>Problembehandlung bei AD DS-Verwaltung  
  
### <a name="introduction-to-troubleshooting"></a>Einführung in die Problembehandlung  
Aufgrund dessen Mangels und des an existierenden kundenumgebungen wurde das Active Directory-Verwaltungscenter Optionen zur Problembehandlung beschränkt.  
  
### <a name="troubleshooting-options"></a>Optionen für die Problembehandlung  
  
#### <a name="logging-options"></a>Optionen für die Protokollierung  
Das Active Directory-Verwaltungscenter enthält nun integrierte Protokollierung in Windows Server 2012 als Teil einer Ablaufverfolgungs-Konfigurationsdatei. Die folgende Datei im selben Ordner wie dsac.exe erstellen/ändern:  
  
**dsac.exe.config**  
  
Erstellen Sie den folgenden Inhalt:  
  
```  
<appSettings>  
  <add key="DsacLogLevel" value="Verbose" />  
</appSettings>  
<system.diagnostics>   
 <trace autoflush="false" indentsize="4">   
  <listeners>   
   <add name="myListener"   
    type="System.Diagnostics.TextWriterTraceListener"   
    initializeData="dsac.trace.log" />   
   <remove name="Default" />   
  </listeners>   
 </trace>   
</system.diagnostics>  
  
```  
  
Die Protokollebenen für **DsacLogLevel** sind **keine**, **Fehler**, **Warnung**, **Informationen**, und **Verbose**. Der Name der Ausgabedatei ist konfigurierbar und schreibt in demselben Ordner wie dsac.exe. Diese Ausgabe enthält weitere Informationen zu wie ADAC betrieben wird, welche Domänencontroller hergestellt, welche Windows PowerShell-Befehle ausgeführt, was die Antworten wurden und weitere Details.  
  
Bei der Verwendung von Stufe INFO, zurückgibt, z. B. alle Ergebnisse mit Ausnahme der Ablaufverfolgungsnachrichten:  
  
-   Starten DSAC.exe  
  
-   Protokollierung gestartet wird  
  
-   Domänencontroller fragt Ausgangs-Domäneninformationen zurück  
  
    ```  
    [12:42:49][TID 3][Info] Command Id, Action, Command, Time, Elapsed Time ms (output), Number objects (output)  
    [12:42:49][TID 3][Info] 1, Invoke, Get-ADDomainController, 2012-04-16T12:42:49  
    [12:42:49][TID 3][Info] Get-ADDomainController-Discover:$null-DomainName:"CORP"-ForceDiscover:$null-Service:ADWS-Writable:$null  
    ```  
  
-   Domänencontroller DC1 zurückgegeben aus Domäne Corp  
  
-   PS AD virtuelles Laufwerk geladen  
  
    ```  
    [12:42:49][TID 3][Info] 1, Output, Get-ADDomainController, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] Found the domain controller 'DC1' in the domain 'CORP'.  
    [12:42:49][TID 3][Info] 2, Invoke, New-PSDrive, 2012-04-16T12:42:49  
    [12:42:49][TID 3][Info] New-PSDrive-Name:"ADDrive0"-PSProvider:"ActiveDirectory"-Root:""-Server:"dc1.corp.contoso.com"  
    [12:42:49][TID 3][Info] 2, Output, New-PSDrive, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] 3, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49  
  
    ```  
  
-   Stamm-DSE-Informationen für die Domäne abrufen  
  
    ```  
    [12:42:49][TID 3][Info] Get-ADRootDSE  
    -Server:"dc1.corp.contoso.com"  
    [12:42:49][TID 3][Info] 3, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] 4, Invoke, Get-ADOptionalFeature, 2012-04-16T12:42:49  
  
    ```  
  
-   Domäne AD-papierkorbinformationen abrufen  
  
    ```  
    [12:42:49][TID 3][Info] Get-ADOptionalFeature  
    -LDAPFilter:"(msDS-OptionalFeatureFlags=1)"  
    -Server:"dc1.corp.contoso.com"  
    [12:42:49][TID 3][Info] 4, Output, Get-ADOptionalFeature, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] 5, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49  
    [12:42:49][TID 3][Info] Get-ADRootDSE  
    -Server:"dc1.corp.contoso.com"  
    [12:42:49][TID 3][Info] 5, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] 6, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49  
    [12:42:49][TID 3][Info] Get-ADRootDSE  
    -Server:"dc1.corp.contoso.com"  
    [12:42:49][TID 3][Info] 6, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] 7, Invoke, Get-ADOptionalFeature, 2012-04-16T12:42:49  
    [12:42:49][TID 3][Info] Get-ADOptionalFeature  
    -LDAPFilter:"(msDS-OptionalFeatureFlags=1)"  
    -Server:"dc1.corp.contoso.com"  
    [12:42:50][TID 3][Info] 7, Output, Get-ADOptionalFeature, 2012-04-16T12:42:50, 1  
    [12:42:50][TID 3][Info] 8, Invoke, Get-ADForest, 2012-04-16T12:42:50  
  
    ```  
  
-   AD-Gesamtstruktur abrufen  
  
    ```  
    [12:42:50][TID 3][Info] Get-ADForest  
    -Identity:"corp.contoso.com"  
    -Server:"dc1.corp.contoso.com"  
    [12:42:50][TID 3][Info] 8, Output, Get-ADForest, 2012-04-16T12:42:50, 1  
    [12:42:50][TID 3][Info] 9, Invoke, Get-ADObject, 2012-04-16T12:42:50  
  
    ```  
  
-   Abrufen von Schemainformationen für unterstützte Verschlüsselungstypen, FGPP und bestimmte Benutzerinformationen  
  
    ```  
    [12:42:50][TID 3][Info] Get-ADObject  
    -LDAPFilter:"(|(ldapdisplayname=msDS-PhoneticDisplayName)(ldapdisplayname=msDS-PhoneticCompanyName)(ldapdisplayname=msDS-PhoneticDepartment)(ldapdisplayname=msDS-PhoneticFirstName)(ldapdisplayname=msDS-PhoneticLastName)(ldapdisplayname=msDS-SupportedEncryptionTypes)(ldapdisplayname=msDS-PasswordSettingsPrecedence))"  
    -Properties:lDAPDisplayName  
    -ResultPageSize:"100"  
    -ResultSetSize:$null  
    -SearchBase:"CN=Schema,CN=Configuration,DC=corp,DC=contoso,DC=com"  
    -SearchScope:"OneLevel"  
    -Server:"dc1.corp.contoso.com"  
    [12:42:50][TID 3][Info] 9, Output, Get-ADObject, 2012-04-16T12:42:50, 7  
    [12:42:50][TID 3][Info] 10, Invoke, Get-ADObject, 2012-04-16T12:42:50  
  
    ```  
  
-   Erhalten Sie alle Informationen über das Domänenobjekt, um dem Administrator anzuzeigen, die auf den domänenkopf geklickt hat.  
  
    ```  
    [12:42:50][TID 3][Info] Get-ADObject  
    -IncludeDeletedObjects:$false  
    -LDAPFilter:"(objectClass=*)"  
    -Properties:allowedChildClassesEffective,allowedChildClasses,lastKnownParent,sAMAccountType,systemFlags,userAccountControl,displayName,description,whenChanged,location,managedBy,memberOf,primaryGroupID,objectSid,msDS-User-Account-Control-Computed,sAMAccountName,lastLogonTimestamp,lastLogoff,mail,accountExpires,msDS-PhoneticCompanyName,msDS-PhoneticDepartment,msDS-PhoneticDisplayName,msDS-PhoneticFirstName,msDS-PhoneticLastName,pwdLastSet,operatingSystem,operatingSystemServicePack,operatingSystemVersion,telephoneNumber,physicalDeliveryOfficeName,department,company,manager,dNSHostName,groupType,c,l,employeeID,givenName,sn,title,st,postalCode,managedBy,userPrincipalName,isDeleted,msDS-PasswordSettingsPrecedence  
    -ResultPageSize:"100"  
    -ResultSetSize:"20201"  
    -SearchBase:"DC=corp,DC=contoso,DC=com"  
    -SearchScope:"Base"  
    -Server:"dc1.corp.contoso.com"  
  
    ```  
  
Festlegen der Verbose auch die .NET Stapel für jede Funktion zeigt, aber diese enthalten nicht genügend Daten ist besonders hilfreich bei der Problembehandlung von Dsac.exe ein zugriffsverletzungen oder abstürzen.  
  
> [!IMPORTANT]  
> Es gibt auch eine Out-of-Band-Version des Diensts mit dem Namen der [Active Directory-Verwaltungsgateway](https://www.microsoft.com/download/en/details.aspx?displaylang=en&id=2852), das auf Windows Server 2008 SP2 und Windows Server 2003 SP2 ausgeführt wird.  
  
Die zwei Hauptgründe für dieses Problem sind:  
  
-   Der ADWS-Dienst wird auf allen erreichbaren Domänencontroller nicht ausgeführt.  
  
-   Die Netzwerkkommunikation sind auf der ADWS-Dienst vom Computer mit dem Active Directory-Verwaltungscenter gesperrt.  
  
Sind Fehler angezeigt, wenn keine Active Directory-Webdienste-Instanzen verfügbar sind:  
  
|||  
|-|-|  
|Fehler|Vorgang|  
|"Keine Domänen herstellen. Aktualisieren, oder versuchen Sie es erneut, wenn die Verbindung verfügbar ist"|Angezeigt beim Start der Active Directory-Verwaltungscenter-Anwendung|  
|"Kann nicht gefunden werden einen verfügbaren Server in der * <NetBIOS domain name> * Domäne, die Active Directory-Webdienst (ADWS) ausgeführt wird"|Angezeigt beim Versuch, einen Domänenknoten in der Active Directory-Verwaltungscenter-Anwendung auswählen|  
  
Gehen Sie folgendermaßen vor, um dieses Problem zu beheben:  
  
1.  Überprüfen Sie die Active Directory-Webdienste-Dienst auf mindestens einem Domänencontroller in der Domäne (und vorzugsweise alle Domänencontroller in der Gesamtstruktur) gestartet wird. Stellen Sie sicher, dass es für den automatischen start auf allen Domänencontrollern sowie festgelegt ist.  
  
2.  Vom Computer mit dem Active Directory-Verwaltungscenter überprüfen Sie, dass Sie einen Server mit ADWS folgenden NLTest.exe-Befehle finden können:  
  
    ```  
    nltest /dsgetdc:<domain NetBIOS name> /ws /force   
    nltest /dsgetdc:<domain fully qualified DNS name> /ws /force  
  
    ```  
  
    Wenn diese Tests fehlschlagen, obwohl der ADWS-Dienst ausgeführt wird, liegt das Problem namensauflösung oder LDAP und nicht ADWS oder Active Directory-Verwaltungscenter. Dieser Test schlägt fehl mit Fehler "1355 0x54B ERROR_NO_SUCH_DOMAIN" Wenn ADWS nicht jedoch auf allen Domänencontrollern ausgeführt wird, also bevor Sie Schlussfolgerungen ziehen überprüfen.  
  
3.  Sichern Sie auf dem von NLTest zurückgegebenen Domänencontroller Liste geöffneter Ports mit dem Befehl ein:  
  
    ```  
    Netstat -anob > ports.txt  
  
    ```  
  
    Überprüfen Sie die Datei Ports.txt und überprüfen Sie, dass der ADWS-Dienst auf Port 9389 geöffnet hat. Beispiel:  
  
    ```  
    TCP    0.0.0.0:9389    0.0.0.0:0    LISTENING    1828  
    [Microsoft.ActiveDirectory.WebServices.exe]  
  
    TCP    [::]:9389       [::]:0       LISTENING    1828  
    [Microsoft.ActiveDirectory.WebServices.exe]  
  
    ```  
  
    Wenn hören, überprüfen Sie die Windows-Firewall-Regeln und stellen Sie sicher, dass die 9389 TCP erlaubt eingehende. Standardmäßig aktivieren Domänencontroller die Firewallregel "Active Directory-Webdienste (TCP eingehend)". Wenn nicht überwacht, erneut prüfen Sie, ob der Dienst auf diesem Server ausgeführt wird, und starten Sie ihn neu. Überprüfen Sie, dass kein anderer Prozess bereits Port 9389 geöffnet hat.  
  
4.  Installieren Sie NetMon oder ein anderes netzwerkerfassungs, auf dem Computer mit Active Directory-Verwaltungscenter und auf dem von NLTEST zurückgegebenen Domänencontroller. Erstellen Sie parallele netzwerkerfassungen auf beiden Computern erfasst, in dem Sie Active Directory-Verwaltungscenter starten und der Fehler wird angezeigt, bevor Sie die Erfassungen anhalten. Überprüfen Sie, dass der Client kann zum Senden und Empfangen von dem Domänencontroller auf TCP-Port 9389. Wenn Pakete gesendet werden, aber niemals ankommen, oder ankommen und die Antwort des Domänencontrollers nicht des-Clients erreicht, ist es vermutlich eine Firewall zwischen den Computern im Netzwerk auf diesen Port Pakete verwirft. Diese Firewall möglicherweise Software oder Hardware, und möglicherweise Teil eines Drittanbieters (Virenschutz) endpunktschutzsoftware.  
  
#### <a name="knownlikely-issues-and-support-scenarios"></a>Bekannte/häufige Probleme und Supportszenarien  
Das einzige wahrscheinliche Problem mit dem Active Directory-Verwaltungscenter ist nicht für die Verbindung zu den Active Directory-Webdienst (ADWS) auf einem Windows Server 2012 oder Windows Server 2008 R2-Domänencontroller ausgeführt wird.  
  
## <a name="see-also"></a>Siehe auch  
[Einführung in Active Directory Administrative Center Enhancements & #40; Stufe 100 & #41;](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md)  
  


---
ms.assetid: 40bc24b1-2e7d-4e77-bd0f-794743250888
title: SPN- und UPN-Eindeutigkeit
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: c3e2cac6cb4d7cb5e76c4c59bfa2b8431f2401c6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972377"
---
# <a name="spn-and-upn-uniqueness"></a>SPN- und UPN-Eindeutigkeit

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**Autor**: Justin Turner, Senior Support Eskalations Techniker mit der Windows-Gruppe

> [!NOTE]
> Dieser Inhalt wurde von einem Mitarbeiter des Microsoft-Kundendiensts geschrieben und richtet sich an erfahrene Administratoren und Systemarchitekten, die einen tieferen technischen Einblick in die Funktionen und Lösungen von Windows Server 2012 R2 suchen, als Ihnen die Themen im TechNet bieten können. Allerdings wurde er nicht mit der gleichen linguistischen Sorgfalt überprüft wie für die Artikel des TechNet üblich, so dass die Sprache gelegentlich holprig klingen mag.

## <a name="overview"></a>Übersicht
Domänen Controller, auf denen Windows Server 2012 R2 ausgeführt wird, blockieren die Erstellung doppelter Dienst Prinzipal Namen (SPN) und Benutzer Prinzipal Namen (UPN). Dies schließt ein, wenn die Wiederherstellung oder neuanimation eines gelöschten Objekts oder das Umbenennen eines Objekts zu einem Duplikat führen würde.

### <a name="background"></a>Hintergrund
Doppelte Dienst Prinzipal Namen (SPN) treten häufig auf und führen zu Authentifizierungs Fehlern und können zu einer übermäßigen LSASS-CPU-Auslastung führen. Es gibt keine in-Box-Methode, mit der das Hinzufügen eines doppelten SPN oder UPN blockiert wird. *

Doppelte UPN-Werte unterbrechen die Synchronisierung zwischen lokalem AD und Office 365.

* Setspn.exe wird häufig zum Erstellen neuer SPNs verwendet, und funktional wurde in die mit Windows Server 2008 veröffentlichte Version integriert, mit der eine Überprüfung auf Duplikate hinzugefügt wird.

**Tabelle \\ \* : Tabelle Arabisch 1: UPN-und SPN-Eindeutigkeit**

|Feature|Comment|
|-----------|-----------|
|UPN-Eindeutigkeit|Doppelte UPNs unterbrechen die Synchronisierung von lokalen AD-Konten mit Windows Azure AD-basierten Diensten wie z. b. Office 365.|
|SPN-Eindeutigkeit|Kerberos erfordert SPNs für die gegenseitige Authentifizierung.  Doppelte SPNs führen zu Authentifizierungs Fehlern.|

Weitere Informationen zu den Eindeutigkeits Anforderungen für UPNs und SPNs finden Sie unter Unique- [Einschränkungen](/openspecs/windows_protocols/ms-adts/3c154285-454c-4353-9a99-fb586e806944).

## <a name="symptoms"></a>Symptome
Fehlercodes 8467 oder 8468 oder Ihre hexadezimalen, symbolischen oder Zeichen folgen Entsprechungen werden in verschiedenen Bildschirm Dialoge und in der Ereignis-ID 2974 im Verzeichnisdienst-Ereignisprotokoll protokolliert. Der Versuch, einen doppelten UPN oder SPN zu erstellen, wird nur unter den folgenden Umständen blockiert:

-   Der Schreibvorgang wird von einem Windows Server 2012 R2-DC verarbeitet.

**Tabelle, Tabelle \\ \* Arabisch 2: Fehlercodes der UPN-und SPN-Eindeutigkeit**

|Decimal|Hex|Trächtigsten|String|
|-----------|-------|------------|----------|
|8467|21c7|ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST|Der Vorgang ist fehlgeschlagen, weil der für Addition/Änderung angegebene SPN-Wert nicht eindeutig Gesamtstruktur weit ist.|
|8648|21c8|ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST|Der Vorgang ist fehlgeschlagen, weil der für die Hinzufügung/Änderung angegebene Wert für den Benutzerprinzipalnamen (User Principal Name, UPN) in der Gesamtstruktur nicht eindeutig ist.|

## <a name="new-user-creation-fails-if-upn-is-not-unique"></a>Fehler beim Erstellen eines neuen Benutzers, wenn der UPN nicht eindeutig ist.

### <a name="dsamsc"></a>DSA. msc
Der Benutzer Anmelde Name, den Sie ausgewählt haben, wird in diesem Unternehmen bereits verwendet. Wählen Sie einen anderen Anmelde Namen aus, und wiederholen Sie den Vorgang.

![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig01_DupUPN.gif)

Vorhandenes Konto ändern:

Der angegebene Benutzer Anmelde Name ist bereits im Unternehmen vorhanden. Geben Sie eine neue ein, indem Sie entweder das Präfix ändern oder ein anderes Suffix aus der Liste auswählen.

![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig02_DupUPNMod.gif)

### <a name="active-directory-administrative-center-dsacexe"></a>Active Directory-Verwaltungscenter (DSAC.exe)
Der Versuch, einen neuen Benutzer in Active Directory-Verwaltungscenter mit einem bereits vorhandenen UPN zu erstellen, führt zu folgendem Fehler.

![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig03_DupUPNADAC.gif)

**Abbildung * Abbildung \\ \* Arabisch 1 Fehler wird im AD-Verwaltungs Center angezeigt, wenn die Erstellung eines neuen Benutzers aufgrund eines doppelten UPN fehlschlägt**

### <a name="event-2974-source-activedirectory_domainservice"></a>Ereignis 2974 Quelle: ActiveDirectory_DomainService
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig04_Event2974.gif)

**Abbildung * Abbildung \\ \* Arabisch 2 Ereignis-ID 2974 mit Fehler 8648**

Das Ereignis 2974 listet den Wert auf, der blockiert wurde, und eine Liste mit einem oder mehreren Objekten (bis zu 10), die diesen Wert bereits enthalten.  In der folgenden Abbildung sehen Sie, dass der UPN-Attribut Wert **<em>dhunt@blue.contoso.com</em>** bereits in vier anderen Objekten vorhanden ist.  Da es sich hierbei um ein neues Feature in Windows Server 2012 R2 handelt, treten die versehentliche Erstellung doppelter UPN und SPNs in einer gemischten Umgebung weiterhin auf, wenn der Schreib Versuch von DCS der untergeordneten Ebene verarbeitet wird.

![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig05_Event2974ShowAllDups.gif)

**Abbildung SEQ Abbildung \\ \* Arabisch 3 Ereignis 2974 mit allen Objekten, die den doppelten UPN enthalten**

> [!TIP]
> Ereignis-ID 2974s regelmäßig überprüfen für:
>
> -   Erkennen von versuchen, doppelte UPN oder SPNs zu erstellen
> -   Objekte identifizieren, die bereits Duplikate enthalten

8648 = "der Vorgang ist fehlgeschlagen, weil der für Addition/Änderung angegebene UPN-Wert nicht eindeutig Gesamtstruktur weit ist."

### <a name="setspn"></a>Setspn
In Setspn.exe wurde seit der Verwendung der Option **"-S"** in der Windows Server 2008-Version eine doppelte SPN-Erkennung integriert.  Sie können den doppelten SPN-Erkennungsdienst mit der Option **"-A"** umgehen.  Die Erstellung eines doppelten SPN wird blockiert, wenn ein Windows Server 2012 R2-DC mithilfe von Setspn mit der Option-a als Ziel verwendet wird.  Die angezeigte Fehlermeldung ist identisch mit der Option, die bei Verwendung der Option "-S" angezeigt wird: "doppelter SPN gefunden, Vorgang wird abgebrochen!"

### <a name="adsiedit"></a>ADSIEdit

```
Operation failed. Error code: 0x21c8
The operation failed because UPN value provided for addition/modification is not unique forest-wide.
000021C8: AtrErr: DSID-03200BBA, #1: 0: 000021C8: DSID-03200BBA, problem 1005 (CONSTRAINT_ATT_TYPE), data 0, Att 90290 (userPrincipalName)
```

![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig06_ADSI21c8.gif)

**Abbildung * Abbildung \\ \* Arabisch 4 Fehlermeldung wird in ADSIEdit angezeigt, wenn das Hinzufügen eines doppelten UPN blockiert wird**

### <a name="windows-powershell"></a>Windows PowerShell
Windows Server 2012 R2:

![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig07_SetADUser2012.gif)

PS, der von Server 2012 aus als Ziel eines Windows Server 2012 R2-DC ausgeführt wird:

![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig08_SetADUser2012R2.gif)

DSAC.exe, die unter Windows Server 2012 ausgeführt werden und auf einen Windows Server 2012 R2-DC abzielen:

![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig09_UserCreateError.gif)

**Abbildung * Abbildung \\ \* Arabisch 5 Dsac-Benutzer Erstellungs Fehler auf nicht-Windows Server 2012 R2 bei Windows Server 2012 R2 DC**

![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig10_UserModError.gif)

**Abbildung * Abbildung \\ \* Arabisch 6 Dsac-Benutzer Änderungs Fehler auf nicht-Windows Server 2012 R2 bei Windows Server 2012 R2 DC**

### <a name="restore-of-an-object-that-would-result-in-a-duplicate-upn-fails"></a>Beim Wiederherstellen eines Objekts, das zu einem doppelten UPN führt, tritt ein Fehler auf:
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig11_RestoreDupUPN.gif)

![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig12_RestoreDupUPNError.gif)

Wenn ein Objekt aufgrund eines doppelten UPN/SPN nicht wieder hergestellt werden kann, wird kein Ereignis protokolliert.

Der UPN des Objekts muss eindeutig sein, damit es wieder hergestellt werden kann.

1.  Identifizieren des UPN, der für das Objekt im Papierkorb vorhanden ist

2.  Alle Objekte identifizieren, die denselben Wert aufweisen

3.  Entfernen Sie die doppelten UPN (s).

### <a name="identify-the-conflicting-upn-on-the-deleted-objectusing-repadminexe"></a>Identifizieren Sie den in Konflikt stehenden UPN für das gelöschte objectusing repadmin.exe

```
Repadmin /showattr DCName "DN of deleted objects container" /subtree /filter:"(msDS-LastKnownRDN=<NAME>)" /deleted /atts:userprincipalname
```

```
repadmin /showattr DCName "CN=Deleted Objects,DC=blue,DC=contoso,DC=com" /subtree /filter:"(msDS-LastKnownRDN=Dianne Hunt2)" /deleted /atts:userprincipalname

C:\>repadmin /showattr winbluedc1 "cn=deleted objects,dc=blue,dc=contoso,dc=com" /subtree /filter:"(msds-lastknownrdn=Dianne Hunt2)" /deleted /atts:userprincipalname
DN: CN=Dianne Hunt2\0ADEL:dd3ab8a4-3005-4f2f-814f-d6fc54a1a1c0,CN=Deleted Object
s,DC=blue,DC=contoso,DC=com
    1> userPrincipalName: dhunt@blue.contoso.com
```

### <a name="to-identify-all-objects-with-the-same-upnusing-repadminexe"></a>So identifizieren Sie alle Objekte mit demselben UPN: Verwenden von Repadmin.exe

```
repadmin /showattr WinBlueDC1 "DC=blue,DC=contoso,DC=com" /subtree /filter:"(userPrincipalName=dhunt@blue.contoso.com)" /deleted /atts:DN

C:\>repadmin /showattr winbluedc1 "dc=blue,dc=contoso,dc=com" /subtree /filter:"(userPrincipalName=dhunt@blue.contoso.com)" /deleted /atts:DN
DN: CN=Administrator,CN=Users,DC=blue,DC=contoso,DC=com
DN: CN=xouser1,CN=Users,DC=blue,DC=contoso,DC=com
DN: CN=xouser10,CN=Users,DC=blue,DC=contoso,DC=com
DN: CN=xouser100,CN=Users,DC=blue,DC=contoso,DC=com
DN: CN=Dianne Hunt,OU=Marketing,DC=blue,DC=contoso,DC=com
DN: CN=Dianne Hunt2\0ADEL:dd3ab8a4-3005-4f2f-814f-d6fc54a1a1c0,CN=Deleted Objects,DC=blue,DC=contoso,DC=com
```

> [!TIP]
> Der zuvor nicht dokumentierte **/deleted** -Parameter in repadmin.exe wird zum einschließen gelöschter Objekte im Resultset verwendet.

### <a name="using-global-search"></a>Verwenden der globalen Suche

-   Öffnen Sie Active Directory-Verwaltungscenter, und navigieren Sie zu **globale Suche** .

-   Aktivieren Sie das Optionsfeld **in LDAP konvertieren** .

-   Type **(UserPrincipalName =*ConflictingUPN*)**

    -   Ersetzen Sie ***ConflictingUPN*** durch den tatsächlichen UPN, der in Konflikt steht.

-   Auswahl **anwenden**

![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig13_GlobalSearch.gif)

### <a name="using-windows-powershell"></a>Verwenden von Windows PowerShell

```
Get-ADObject -LdapFilter "(userPrincipalName=dhunt@blue.contoso.com)" -IncludeDeletedObjects -SearchBase "DC=blue,DC=Contoso,DC=com" -SearchScope Subtree -Server winbluedc1.blue.contoso.com
```

![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig13_GlobalSearchPS.gif)

Wenn das Objekt wieder hergestellt werden muss, müssen Sie die doppelten UPNs aus den anderen Objekten entfernen.  Nur für ein Objekt ist es einfach genug, das Duplikat mit ADSIEdit zu entfernen.  Wenn mehrere Objekte mit Duplikaten vorhanden sind, ist Windows PowerShell möglicherweise das bessere Tool.

So legen Sie das userPrincipalName-Attribut mithilfe von Windows PowerShell auf NULL fest:

![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig15_NullUPN.gif)

> [!NOTE]
> Das userPrincipalName-Attribut ist ein einwertiges Attribut, daher entfernt diese Prozedur nur den doppelten UPN.

### <a name="duplicate-spn"></a>Doppelter SPN
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig16_DupSPN.gif)

**Abbildung * Abbildung \\ \* Arabisch 8 Fehlermeldung wird in ADSIEdit angezeigt, wenn das Hinzufügen eines doppelten SPNs blockiert wird**

Im Verzeichnisdienst-Ereignisprotokoll ist eine **ActiveDirectory_DomainService** Ereignis-ID **2974**. protokolliert.

```
Operation failed. Error code: 0x21c7
The operation failed
The attribute value provided is not unique in the forest or partition. Attribute:
servicePrincipalName Value=<SPN>
<Object DN> Winerror: 8467
```

![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig17_DupSPN2974.gif)

**Abbildung * Abbildung \\ \* Arabisch 9 Fehler protokolliert, wenn die Erstellung eines doppelten SPN blockiert ist**

### <a name="workflow"></a>Workflow

-   **Wenn DC = = GC**

    -   Kein offboxbefehl erforderlich, Abfrage kann lokal ausgeführt werden.

    -   ***UPN-Fall***

        -   Abfrage der lokalen Gesamtstruktur weiten UPN-Index für den angegebenen UPN (*userPrincipalName; ein globaler Index*)

            -   Wenn zurückgegebene Einträge = = 0-> Schreibvorgänge fortgesetzt

            -   Wenn die zurückgegebenen Einträge! = 0-> Schreibvorgang fehlschlägt

                -   Protokolliertes Ereignis

                -   Außerdem wird der erweiterte Fehler zurückgegeben:

                    -   **8648:**

                        *ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST*

    -   ***SPN-Fall***

        -   Abfragen des lokalen Gesamtstruktur-SPN-Indexes für den bereitgestellten SPN (*servicePrincipalName; ein globaler Index*)

            -   Wenn zurückgegebene Einträge = = 0-> Schreibvorgänge fortgesetzt

            -   Wenn die zurückgegebenen Einträge! = 0-> Schreibvorgang fehlschlägt

                -   Protokolliertes Ereignis

                -   Außerdem wird der erweiterte Fehler zurückgegeben:

                    -   **8647:**

                        **ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST**

-   **Wenn DC! = GC**

    -   Der offboxanganrufe ist **wünschenswert** , aber nicht kritisch, d. h., dies ist eine Eindeutigkeits Überprüfung

        -   Die Überprüfung wird nur bei der lokalen dit durchgeführt, wenn GC nicht gefunden

        -   Ereignis protokolliert, um dies anzuzeigen

    -   ***UPN-Fall***

        -   Senden Sie eine LDAP-Abfrage an die nächstgelegene GC? der Gesamtstruktur weite UPN-Index der Abfrage GC für den angegebenen UPN (*userPrincipalName; ein globaler Index*)

            -   Wenn zurückgegebene Einträge = = 0-> Schreibvorgänge fortgesetzt

            -   Wenn die zurückgegebenen Einträge! = 0-> Schreibvorgang fehlschlägt

                -   Protokolliertes Ereignis

                -   Außerdem wird der erweiterte Fehler zurückgegeben:

                    -   **8648:**

                        *ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST*

    -   ***SPN-Fall***

        -   Senden Sie eine LDAP-Abfrage an die nächstgelegene GC? der Gesamtstruktur übergreifende SPN-Index der Abfrage für den bereitgestellten SPN (*servicePrincipalName; ein globaler Index*)

            -   Wenn zurückgegebene Einträge = = 0-> Schreibvorgänge fortgesetzt

            -   Wenn die zurückgegebenen Einträge! = 0-> Schreibvorgang fehlschlägt

                -   Protokolliertes Ereignis

                -   Außerdem wird der erweiterte Fehler zurückgegeben:

                    -   **8647:**

                        *ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST*

Wenn gelöschte Objekte erneut animiert werden, werden die SPN-oder UPN-Werte auf Eindeutigkeit geprüft. Wenn ein Duplikat gefunden wird, schlägt die Anforderung fehl.

-   Bei bestimmten Attribut Änderungen wie dem DNS-Hostnamen, dem SAM-Kontonamen usw., wenn die Änderung vorgenommen wird, werden die SPNs entsprechend aktualisiert. Beim Prozess werden die veralteten SPNs gelöscht, und es werden neue SPNs erstellt und der Datenbank hinzugefügt. Die erforderlichen Attribut Änderungen, bei denen dieser Pfad ausgelöst wird, lauten:

    -   ATT_DNS_HOST_NAME

    -   ATT_MS_DS_ADDITIONAL_DNS_HOST_NAME

    -   ATT_SAM_ACCOUNT_NAME

    -   ATT_MS_DS_ADDITIONAL_SAM_ACCOUNT_NAME

    -   ATT_SERVER_REFERENCE_BL

    -   ATT_USER_ACCOUNT_CONTROL

Wenn einer der neuen SPN-Werte ein Duplikat ist, tritt bei der Änderung ein Fehler auf. In der obigen Liste sind die wichtigen Attribute ATT_DNS_HOST_NAME (Computername) und ATT_SAM_ACCOUNT_NAME (SAM-Kontoname).

### <a name="try-this-exploring-spn-and-upn-uniqueness"></a>Versuchen Sie Folgendes: Untersuchen von SPN und UPN-Eindeutigkeit
Dies ist die erste von mehreren "**try this**"-Aktivitäten im Modul.  Es gibt keine separate Lab-Anleitung für dieses Modul.  Die **try this** -Aktivitäten sind im Wesentlichen frei Form Aktivitäten, mit denen Sie die Lektion in der Lab-Umgebung untersuchen können.  Sie haben die Möglichkeit, die Eingabeaufforderung zu befolgen oder das Skript zu erstellen und ihre eigene Aktivität zu erstellen.

> [!NOTE]
> -   Dies ist die erste von mehreren "**try this**"-Aktivitäten.
> -   Es gibt keine separate Lab-Anleitung für dieses Modul.
> -   Die **try this** -Aktivitäten sind im Wesentlichen frei Form Aktivitäten, mit denen Sie die Lektion in der Lab-Umgebung untersuchen können.
> -   Sie haben die Möglichkeit, die Eingabeaufforderung zu befolgen oder das Skript zu erstellen und ihre eigene Aktivität zu erstellen.
> -   Obwohl nicht für alle Abschnitte eine **try this** -Eingabeaufforderung vorhanden ist, wird empfohlen, den Lektion-Inhalt des Labs, falls zutreffend, zu untersuchen.

Experimentieren Sie mit der Eindeutigkeit von SPN und UPN.  Befolgen Sie diese Anweisungen, oder vervollständigen Sie Ihre eigenen.

1.  Erstellen neuer Benutzer mit UPN

2.  Erstellen von Konten mit SPNs

3.  Erstellen Sie entweder einen neuen Benutzer mit einem bereits zuvor definierten UPN, oder ändern Sie den UPN eines vorhandenen Kontos.  Führen Sie die gleichen Schritte für einen SPN für ein anderes Konto aus.

    1.  Auffüllen eines vorhandenen Benutzerkontos mit einem bereits verwendeten UPN

        1.  Verwenden von PowerShell, ADSIEdit oder Active Directory-Verwaltungscenter (DSAC.exe)

    2.  Auffüllen eines vorhandenen Kontos mit einem bereits verwendeten SPN

        1.  Verwenden von Windows PowerShell, ADSIEdit oder Setspn

4.  Beachten Sie die Fehler.

**Optional**

1.  Überprüfen Sie mit dem Classroom-Dozenten, dass es in Ordnung ist, den *[AD-Papier](../../get-started/adac/advanced-ad-ds-management-using-active-directory-administrative-center--level-200-.md#BKMK_EnableRecycleBin)* Korb in Active Directory-Verwaltungscenter zu aktivieren.  Wenn dies der Fall ist, fahren Sie mit dem nächsten Schritt fort.

2.  Auffüllen des UPN für ein Benutzerkonto

3.  Löschen des Kontos

4.  Ein anderes Konto mit dem gleichen UPN wie das gelöschte Konto auffüllen

5.  Versuch der Verwendung der Papierkorb-GUI zum Wiederherstellen des Kontos

6.  Stellen Sie sich vor, dass Ihnen soeben der Fehler angezeigt wird, den Sie im vorherigen Schritt gesehen haben.  (und haben keinen Verlauf der soeben ausgeführten Schritte) Ihr Ziel ist es, die Wiederherstellung des Kontos abzuschließen.  Weitere Informationen finden Sie in der Arbeitsmappe.


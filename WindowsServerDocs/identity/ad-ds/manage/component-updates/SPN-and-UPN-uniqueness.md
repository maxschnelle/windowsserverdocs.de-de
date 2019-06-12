---
ms.assetid: 40bc24b1-2e7d-4e77-bd0f-794743250888
title: SPN- und UPN-Eindeutigkeit
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 13259f7f12a37c4ceb8bdd2e35ae2fe131ec35cf
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442817"
---
# <a name="spn-and-upn-uniqueness"></a>SPN- und UPN-Eindeutigkeit

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**Autor**: Justin Turner, Senior Support Escalation Engineer für die Windows-Gruppe  
  
> [!NOTE]  
> Dieser Inhalt wurde von einem Mitarbeiter des Microsoft-Kundendiensts geschrieben und richtet sich an erfahrene Administratoren und Systemarchitekten, die einen tieferen technischen Einblick in die Funktionen und Lösungen von Windows Server 2012 R2 suchen, als Ihnen die Themen im TechNet bieten können. Allerdings wurde er nicht mit der gleichen linguistischen Sorgfalt überprüft wie für die Artikel des TechNet üblich, so dass die Sprache gelegentlich holprig klingen mag.  
  
## <a name="overview"></a>Übersicht  
Domänencontroller unter Windows Server 2012 R2 blockieren die Erstellung doppelter Dienstprinzipalnamen (SPN) und Benutzerprinzipalnamen (UPN). Dies schließt, wenn es sich bei der Wiederherstellung oder der Wiederbelebung eines gelöschten Objekts oder das Umbenennen eines Objekts zu einem Duplikat führen würde.  
  
### <a name="background"></a>Hintergrund  
Doppelte Dienstprinzipalnamen (SPN) häufig auftreten und entstehen Authentifizierungsfehler und kann zu übermäßiger LSASS-CPU-Auslastung führen. Es gibt keine integrierte Methode blockiert das Hinzufügen eines doppelten SPN oder UPN. *  
  
UPN Duplikatwerte unterbrechen Synchronisierung zwischen lokalem AD und Office 365.  
  
*Setspn.exe wird häufig verwendet werden, um die neue SPNs zu erstellen, und Funktionen in die mit Windows Server 2008, die eine Überprüfung auf Duplikate hinzufügt Version erstellt wurde.  
  
**Tabelle SEQ Tabelle \\ \* Arabisch 1: UPN und die SPN-Eindeutigkeit**  
  
|Feature|Kommentar|  
|-----------|-----------|  
|UPN-Eindeutigkeit|Doppelte Benutzerprinzipalnamen-Break-Synchronisierung von lokalen AD-Konten mit Windows Azure AD-basierten Diensten wie Office 365.|  
|SPN-Eindeutigkeit|Kerberos ist ein SPN für die gegenseitige Authentifizierung erforderlich.  Doppelte SPNs entstehen Authentifizierungsfehler.|  
  
Weitere Informationen zu den Anforderungen hinsichtlich der Eindeutigkeit für UPNs und SPNs, finden Sie unter [Eindeutigkeit](https://msdn.microsoft.com/library/dn392337.aspx).  
  
## <a name="symptoms"></a>Symptome  
8467 oder 8468 oder ihre symbolischen Hexadezimal oder Fehlercodes identische Zeichenfolgen werden protokolliert in verschiedenen auf dem Bildschirm Dialoge und Ereignis-ID-2974-– im Verzeichnisdienste-Ereignisprotokoll. Der Versuch, ein doppelter UPN oder SPN zu erstellen, wird nur unter folgenden Umständen blockiert:  
  
-   Der Schreibvorgang wird von einem Windows Server 2012 R2-Domänencontroller verarbeitet werden.  
  
**Tabelle SEQ Tabelle \\ \* Arabisch 2: UPN und die SPN-Fehlercodes für Eindeutigkeit**  
  
|Dezimalzahl|Hex|Symbolische|Zeichenfolge|  
|-----------|-------|------------|----------|  
|8467|21C7|ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST|Vorgangsfehler, da für die Hinzufügung/Änderung angegebene SPN-Wert nicht eindeutig eine gesamtstrukturweite ist.|  
|8648|21C8|ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST|Vorgangsfehler, da das UPN-Wert für die Hinzufügung/Änderung bereitgestellt, nicht eindeutige Gesamtstruktur ist.|  
  
## <a name="new-user-creation-fails-if-upn-is-not-unique"></a>Erstellen des neuen Benutzers schlägt fehl, wenn es sich bei UPN nicht eindeutig ist.  
  
### <a name="dsamsc"></a>DSA.msc  
Anmeldenamen des Benutzers ein, die, den Sie ausgewählt haben, ist bereits in dieser Organisation verwendet. Wählen Sie einen anderen Anmeldenamen, und versuchen Sie es dann erneut.  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig01_DupUPN.gif)  
  
Ändern Sie ein vorhandenes Konto an:  
  
Der angegebene Benutzername für die Anmeldung bereits im Unternehmen. Geben Sie eine neue, entweder durch das Präfix ändern oder ein anderes Suffix in der Liste auswählen.  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig02_DupUPNMod.gif)  
  
### <a name="active-directory-administrative-center-dsacexe"></a>Active Directory Administrative Center (DSAC.exe)  
Der Versuch, einen neuen Benutzer in Active Directory Administrative Center, mit dem UPN erstellen, die bereits vorhanden ist, wird den folgenden Fehler ergeben.  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig03_DupUPNADAC.gif)  
  
**Figure SEQ Abbildung \\ \* Arabisch 1 Fehler, die im Active Directory-Verwaltungscenter angezeigt wird, wenn die benutzererstellung neuer aufgrund von doppelten UPN fehlschlägt**  
  
### <a name="event-2974-source-activedirectorydomainservice"></a>Ereignis 2974 – Quelle: ActiveDirectory_DomainService  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig04_Event2974.gif)  
  
**Figure SEQ Abbildung \\ \* Arabisch 2-Ereignis-ID 2974 Fehler 8648**  
  
Das Ereignis 2974 – Listet den Wert, der blockiert wurde und eine Liste von ein oder mehrere Objekte (bis zu 10), die bereits auf diesen Wert enthalten.  In der folgenden Abbildung sehen Sie, UPN-Attributwert **<em>dhunt@blue.contoso.com</em>** ist auf vier weitere Objekte bereits vorhanden.  Da dies ein neues Feature in Windows Server 2012 R2 ist, werden versehentliche Erstellung der doppelten UPN und SPNs in einer gemischten Umgebung weiterhin auftreten, wenn es sich bei älteren DCs der versuchte Schreibvorgang verarbeiten.  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig05_Event2974ShowAllDups.gif)  
  
**Figure SEQ Abbildung \\ \* Arabisch 3 Ereignis 2974 Anzeige aller Objekte, die mit der doppelten UPN**  
  
> [!TIP]  
> Ereignis-ID 2974s regelmäßig zu überprüfen:  
>   
> -   versucht, doppelte UPN oder SPN zu erstellen, zu identifizieren  
> -   Identifizieren von Objekten, die bereits auf Duplikate enthalten  
  
8648 = "Den Vorgang ist fehlgeschlagen, da das UPN-Wert für die Hinzufügung/Änderung bereitgestellt, nicht eindeutige Gesamtstruktur ist."  
  
### <a name="setspn"></a>SetSPN:  
Setspn.exe wurden doppelte SPN-Erkennung, die seit der Veröffentlichung von Windows Server 2008 integriert, bei Verwendung der **"-S"** Option.  Sie können die Erkennung von Duplikaten SPN umgehen, indem Sie mit der **"-ein"** jedoch option.  Erstellen eines doppelten SPN wird blockiert, wenn ein Windows Server 2012 R2-Domänencontroller, mithilfe von SetSPN mit der Option – ein.  Die angezeigte Fehlermeldung ist identisch mit der angezeigt wird, wenn die Option ' -s' verwenden: "Doppelter Dienstprinzipalname gefunden, Vorgang wird abgebrochen."  
  
### <a name="adsiedit"></a>ADSI EDIT:  
  
```  
Operation failed. Error code: 0x21c8  
The operation failed because UPN value provided for addition/modification is not unique forest-wide.  
000021C8: AtrErr: DSID-03200BBA, #1: 0: 000021C8: DSID-03200BBA, problem 1005 (CONSTRAINT_ATT_TYPE), data 0, Att 90290 (userPrincipalName)  
```  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig06_ADSI21c8.gif)  
  
**Figure SEQ Abbildung \\ \* Arabisch 4-Fehlermeldung, die in ADSI Edit angezeigt wird, beim Hinzufügen von doppelten UPN blockiert wird**  
  
### <a name="windows-powershell"></a>Windows PowerShell  
Windows Server 2012 R2:  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig07_SetADUser2012.gif)  
  
PS von Server 2012 auf einem Windows Server 2012 R2-Domänencontroller ausgeführt:  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig08_SetADUser2012R2.gif)  
  
DSAC.exe auf Windows Server 2012 auf einem Windows Server 2012 R2-Domänencontroller ausgeführt wird:  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig09_UserCreateError.gif)  
  
**Figure SEQ Abbildung \\ \* Arabisch 5 gilt Folgendes Erstellung Benutzerfehler auf nicht - Windows Server 2012 R2 beim Abzielen auf Windows Server 2012 R2-Domänencontroller**  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig10_UserModError.gif)  
  
**Figure SEQ Abbildung \\ \* Arabisch 6 gilt Folgendes Änderung Benutzerfehler auf nicht - Windows Server 2012 R2 beim Abzielen auf Windows Server 2012 R2-Domänencontroller**  
  
### <a name="restore-of-an-object-that-would-result-in-a-duplicate-upn-fails"></a>Wiederherstellen eines Objekts, das einen doppelten UPN führen würde ein Fehler auftritt:  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig11_RestoreDupUPN.gif)  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig12_RestoreDupUPNError.gif)  
  
Es wird kein Ereignis protokolliert, wenn ein Objekt nicht aufgrund einer doppelten UPN wiederherstellen / SPN.  
  
Der UPN des Objekts muss in der Reihenfolge, damit er wiederhergestellt werden, eindeutig sein.  
  
1.  Identifizieren Sie den UPN, der für das Objekt im Papierkorb vorhanden ist.  
  
2.  Identifizieren Sie alle Objekte, die den gleichen Wert haben  
  
3.  Entfernen Sie die doppelten UPN(s)  
  
### <a name="identify-the-conflicting-upn-on-the-deleted-objectusing-repadminexe"></a>Identifizieren Sie den in Konflikt stehende UPN der gelöschten ObjectUsing repadmin.exe  
  
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
  
### <a name="to-identify-all-objects-with-the-same-upnusing-repadminexe"></a>Identifizieren Sie alle Objekte mit dem gleichen UPN: Repadmin.exe verwenden  
  
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
> Die zuvor nicht dokumentierte **/ deleted** Parameter Repadmin.exe wird verwendet, um gelöschte Objekte in das Resultset einschließen  
  
### <a name="using-global-search"></a>Mithilfe der globalen Suche  
  
-   Öffnen Sie Active Directory Administrative Center, und navigieren Sie zu **globale Suche**  
  
-   Wählen Sie die **in LDAP konvertieren** Optionsfeld  
  
-   Typ **("userPrincipalName" =*ConflictingUPN*)**  
  
    -   Ersetzen Sie dies ***ConflictingUPN*** mit den tatsächlichen UPN in Konflikt stehende  
  
-   Wählen Sie **anwenden**  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig13_GlobalSearch.gif)  
  
### <a name="using-windows-powershell"></a>Verwenden von Windows PowerShell  
  
```  
Get-ADObject -LdapFilter "(userPrincipalName=dhunt@blue.contoso.com)" -IncludeDeletedObjects -SearchBase "DC=blue,DC=Contoso,DC=com" -SearchScope Subtree -Server winbluedc1.blue.contoso.com  
```  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig13_GlobalSearchPS.gif)  
  
Wenn das Objekt werden wiederhergestellt muss, werden Sie die doppelten UPNs aus den anderen Objekten entfernen müssen.  Nur ein Objekt ist es einfach genug, um die ADSIEdit verwenden, um das Duplikat zu entfernen.  Wenn mehrere Objekte ohne Duplikate vorhanden sind, möglicherweise Windows PowerShell zu verwendenden bessere Tools.  
  
Auf null zu setzen das UserPrincipalName-Attribut, das mithilfe von Windows PowerShell:  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig15_NullUPN.gif)  
  
> [!NOTE]  
> Das Attribut "userPrincipalName" ist einwertiges Attribut, damit diese Prozedur nur den doppelten UPN entfernt.  
  
### <a name="duplicate-spn"></a>Doppelten SPN  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig16_DupSPN.gif)  
  
**Figure SEQ Abbildung \\ \* Arabische 8-Fehlermeldung, die in ADSI Edit angezeigt wird, wenn, Hinzufügen von doppelten SPN blockiert wird**  
  
In den Verzeichnisdiensten, die Kapazität des Ereignisprotokolls protokolliert eine **ActiveDirectory_DomainService** Ereignis-ID **2974**.  
  
```  
Operation failed. Error code: 0x21c7  
The operation failed   
The attribute value provided is not unique in the forest or partition. Attribute:  
servicePrincipalName Value=<SPN>  
<Object DN> Winerror: 8467  
```  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig17_DupSPN2974.gif)  
  
**Figure SEQ Abbildung \\ \* Arabische 9-Fehler protokolliert, wenn die Erstellung von doppelten SPN blockiert wird**  
  
### <a name="workflow"></a>Workflow  
  
-   **If DC == GC**  
  
    -   Kein Aufruf Offbox erforderlich, die Abfrage lokal ausgeführt werden können  
  
    -   ***UPN Groß-/Kleinschreibung***  
  
        -   Lokale Gesamtstruktur UPN abfragenindex für den angegebenen UPN ( *"userPrincipalName"; einen globalen Index*)  
  
            -   Wenn Einträge zurückgegeben == 0 -> Schreibvorgang durchgeführt wird  
  
            -   Wenn Einträge zurückgegeben! = 0 -> Schreibvorgang ein Fehler auftritt.  
  
                -   Ereignis  
  
                -   Gibt auch erweiterten Fehler zurück:  
  
                    -   **8648:**  
  
                        *ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
    -   ***SPN Groß-/Kleinschreibung***  
  
        -   Lokale Gesamtstruktur SPN abfragenindex für angegebene SPN ( *%ServicePrincipalName; einen globalen Index*)  
  
            -   Wenn Einträge zurückgegeben == 0 -> Schreibvorgang durchgeführt wird  
  
            -   Wenn Einträge zurückgegeben! = 0 -> Schreibvorgang ein Fehler auftritt.  
  
                -   Ereignis  
  
                -   Gibt auch erweiterten Fehler zurück:  
  
                    -   **8647:**  
  
                        **ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST**  
  
-   **If DC != GC**  
  
    -   Offbox Aufruf **wünschenswert** jedoch nicht kritisch ist, d. h. Dies ist eine Best-Effort-Prinzip eindeutigkeitsprüfung  
  
        -   Überprüfung erfolgt für lokale DIT nur dann, wenn GC nicht gefunden werden kann  
  
        -   Ereignis protokolliert, um anzugeben, z. B.  
  
    -   ***UPN Groß-/Kleinschreibung***  
  
        -   Senden von LDAP-Abfrage an den nächstgelegenen GC? der GC-Abfrage eine gesamtstrukturweite UPN-Index für den angegebenen UPN ( *"userPrincipalName"; einen globalen Index*)  
  
            -   Wenn Einträge zurückgegeben == 0 -> Schreibvorgang durchgeführt wird  
  
            -   Wenn Einträge zurückgegeben! = 0 -> Schreibvorgang ein Fehler auftritt.  
  
                -   Ereignis  
  
                -   Gibt auch erweiterten Fehler zurück:  
  
                    -   **8648:**  
  
                        *ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
    -   ***SPN Groß-/Kleinschreibung***  
  
        -   Senden von LDAP-Abfrage an den nächstgelegenen GC? der GC-Abfrage eine gesamtstrukturweite SPN-Index für die angegebene SPN ( *%ServicePrincipalName; einen globalen Index*)  
  
            -   Wenn Einträge zurückgegeben == 0 -> Schreibvorgang durchgeführt wird  
  
            -   Wenn Einträge zurückgegeben! = 0 -> Schreibvorgang ein Fehler auftritt.  
  
                -   Ereignis  
  
                -   Gibt auch erweiterten Fehler zurück:  
  
                    -   **8647:**  
  
                        *ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
Wenn gelöschte Objekte erneut animierte sind, werden SPN oder UPN Werte auf Eindeutigkeit überprüft. Wenn ein Duplikat gefunden wird, schlägt die Anforderung fehl.  
  
-   Wenn die Änderung vorgenommen wird, werden SPNs für bestimmte attributänderungen wie DNS-Hostnamen, SAM-Kontos Namen usw. entsprechend aktualisiert. Im Prozess die veralteten SPNs werden gelöscht und neue SPNs erstellt werden, und der Datenbank hinzugefügt werden sollen. Die erforderlichen attributänderungen, die für die ausgelöst wird, diesen Pfad sind:  
  
    -   ATT_DNS_HOST_NAME  
  
    -   ATT_MS_DS_ADDITIONAL_DNS_HOST_NAME  
  
    -   ATT_SAM_ACCOUNT_NAME  
  
    -   ATT_MS_DS_ADDITIONAL_SAM_ACCOUNT_NAME  
  
    -   ATT_SERVER_REFERENCE_BL  
  
    -   ATT_USER_ACCOUNT_CONTROL  
  
Wenn keines der neuen SPN-Wert ist ein Duplikat, fehl, wir die Änderung. Von der Liste oben sind die wichtigen Attribute ATT_DNS_HOST_NAME (Computername) und ATT_SAM_ACCOUNT_NAME (SAM-Kontoname).  
  
### <a name="try-this-exploring-spn-and-upn-uniqueness"></a>Versuchen Sie Folgendes aus: Untersuchen von SPN- und UPN-Eindeutigkeit  
Dies ist die erste von mehreren "**Probieren Sie dies**" Aktivitäten im Modul.  Eine separate Lab-Handbuch für dieses Modul besteht nicht.  Die **Probieren Sie dies** Aktivitäten sind im Wesentlichen Freiform-Aktivitäten, mit denen Sie das Lektion Material in der laborumgebung untersuchen.  Sie haben die Möglichkeit, befolgen die Eingabeaufforderung oder das Skript an und ich und Entwickeln Ihrer eigenen Aktivität.  
  
> [!NOTE]  
> -   Dies ist die erste von mehreren "**Probieren Sie dies**" Aktivitäten.  
> -   Eine separate Lab-Handbuch für dieses Modul besteht nicht.  
> -   Die **Probieren Sie dies** Aktivitäten sind im Wesentlichen Freiform-Aktivitäten, mit denen Sie das Lektion Material in der laborumgebung untersuchen.  
> -   Sie haben die Möglichkeit, befolgen die Eingabeaufforderung oder das Skript an und ich und Entwickeln Ihrer eigenen Aktivität.  
> -   Zwar nicht alle Abschnitte einer **Probieren Sie dies** dazu aufgefordert werden, es wird weiterhin empfohlen, den Lektionsinhalt im Labor gegebenenfalls untersuchen.  
  
Experimentieren Sie mit SPN und UPN-Eindeutigkeit.  Befolgen Sie diese Anweisungen, oder führen Sie Ihre eigenen.  
  
1.  Erstellen Sie neue Benutzer mit UPN  
  
2.  Erstellen von Konten mithilfe von SPNs  
  
3.  Erstellen eines neuen Benutzers mit einem bereits zuvor definierten UPN oder ändern Sie ein vorhandenes Konto UPN.  Gleiches gilt für einen SPN für ein anderes Konto  
  
    1.  Füllen Sie ein bestehendes Benutzerkonto an, mit dem UPN bereits in Verwendung  
  
        1.  Mithilfe von PowerShell, ADSIEDIT oder Active Directory-Verwaltungscenter (DSAC.exe)  
  
    2.  Füllen Sie ein vorhandenes Konto mit einem SPN bereits in Verwendung  
  
        1.  Mithilfe von Windows PowerShell, ADSIEDIT oder SetSPN  
  
4.  Beachten Sie die Fehler  
  
**Optionally**  
  
1.  Mit der seminarleiter überprüfen, ob es zum Aktivieren "ok" die *[AD-Papierkorb](https://technet.microsoft.com/library/jj574144.aspx#BKMK_EnableRecycleBin)* im Active Directory-Verwaltungscenter.  Wenn dies der Fall ist, fahren Sie mit der im nächsten Schritt.  
  
2.  Füllen Sie den UPN eines Benutzerkontos  
  
3.  Das Konto löschen  
  
4.  Füllen Sie ein anderes Konto mit dem gleichen UPN als das gelöschte Konto  
  
5.  Auf der grafischen Benutzeroberfläche Wiederverwenden von "bin" zu verwenden, um das Konto wiederherstellen  
  
6.  Angenommen Sie, Sie einfach mit dem Fehler angezeigt wurden, die im vorherigen Schritt angezeigt.  (und nicht über einen Verlauf der soeben ausgeführten Schritte) Ihr Ziel ist zum Abschließen des Wiederherstellungsvorgangs des Kontos.  Finden Sie in die Arbeitsmappe beispielsweise die Schritte.  
  



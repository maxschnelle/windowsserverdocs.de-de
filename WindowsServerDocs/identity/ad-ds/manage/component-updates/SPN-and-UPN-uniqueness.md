---
ms.assetid: 40bc24b1-2e7d-4e77-bd0f-794743250888
title: SPN- und UPN-Eindeutigkeit
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 81d686c81082ad29384585d541c1304d654e1924
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="spn-and-upn-uniqueness"></a>SPN- und UPN-Eindeutigkeit

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

**"Author"**: Justin Turner, Senior Support Escalation Engineer mit der Windows-Gruppe  
  
> [!NOTE]  
> Dieser Inhalt wird von Microsoft Customer Support-Mitarbeiter geschrieben und richtet erfahrene Administratoren und Systemarchitekten, die als Themen auf TechNet finden Sie in der Regel einen tieferen technischen Einblick Funktionen und Lösungen in Windows Server 2012 R2 suchen. Allerdings hat es nicht die gleichen linguistischen damit einige der Sprache möglicherweise weniger glänzend als was in der Regel auf TechNet-Website gefunden wird.  
  
## <a name="overview"></a>(Übersicht)  
Domänencontroller unter Windows Server2012 R2 blockieren die Erstellung doppelter Dienstprinzipalnamen (SPN) und Benutzerprinzipalnamen (UPN). Dazu gehören die Wiederherstellung oder die Wiederherstellung eines gelöschten Objekts oder das Umbenennen eines Objekts ein Duplikat ergeben würde.  
  
### <a name="background"></a>Hintergrund  
Doppelte Dienstprinzipalnamen (SPN) häufig auftreten und zu Authentifizierungsfehlern führen und kann dazu führen, dass eine übermäßige LSASS CPU-Auslastung. Es gibt keine in-Box-Methode, um das Hinzufügen eines doppelten SPN oder UPN zu blockieren. *  
  
Doppelten UPN-Werte unterbrechen Synchronisierung zwischen lokalem AD und Office365.  
  
*Setspn.exe wird häufig verwendet, um neue SPNs erstellen und funktional in die mit Windows Server2008, die eine Überprüfung auf Duplikate hinzufügt Version erstellt wurde.  
  
**Tabelle SEQ Tabelle \\\ * Arabisch 1: UPN und SPN-Eindeutigkeit**  
  
|Funktion|Kommentar|  
|-----------|-----------|  
|UPN-Eindeutigkeit|Doppelte Benutzerprinzipalnamen Break-Synchronisierung der lokalen AD-Konten mit Windows Azure Active Directory-basierte Dienste wie Office365.|  
|SPN-Eindeutigkeit|Kerberos ist ein Dienstprinzipalnamen (SPN) für die gegenseitige Authentifizierung erforderlich.  Doppelte Dienstprinzipalnamen (SPN) zu Authentifizierungsfehlern führen.|  
  
Weitere Informationen zu Eindeutigkeit für Benutzerprinzipalnamen und Dienstprinzipalnamen (SPN), finden Sie unter [Eindeutigkeit](https://msdn.microsoft.com/library/dn392337.aspx).  
  
## <a name="symptoms"></a>Symptome  
Fehlercodes 8467 oder 8468 oder ihre Hex symbolischen oder Zeichenfolge Entsprechungen werden protokolliert in verschiedenen auf dem Bildschirm Dialoge in Spielen und Ereignis-ID 2974 – im Verzeichnisdienste-Ereignisprotokoll. Der Versuch zum Erstellen eines doppelten UPN oder SPN ist nur unter folgenden Umständen blockiert:  
  
-   Das Schreiben wird von einem Windows Server2012 R2-Domänencontroller verarbeitet werden.  
  
**Tabelle SEQ Tabelle \\\ * Arabisch 2: UPN und SPN-Eindeutigkeit-Fehlercodes**  
  
|Dezimale Sprachen|Hex|Symbolische|Zeichenfolge|  
|-----------|-------|------------|----------|  
|8467|21C 7|ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST|Der Vorgang ist fehlgeschlagen, da SPN-Wert für die Hinzufügung/Änderung nicht eindeutigen Gesamtstruktur ist.|  
|8648|21C 8|ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST|Der Vorgang ist fehlgeschlagen, da UPN-Wert für die Hinzufügung/Änderung nicht eindeutigen Gesamtstruktur ist.|  
  
## <a name="new-user-creation-fails-if-upn-is-not-unique"></a>Die Erstellung des neuen Benutzers ein Fehler auftritt, wenn UPN nicht eindeutig ist  
  
### <a name="dsamsc"></a>DSA.msc  
Anmeldenamen des Benutzers ein, die Sie ausgewählt haben, ist bereits in diesem Unternehmen verwendet. Wählen Sie einen anderen Anmeldenamen, und versuchen Sie es dann erneut.  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig01_DupUPN.gif)  
  
Ändern Sie ein vorhandenes Konto:  
  
Der angegebene Benutzername für die Anmeldung ist im Unternehmen bereits vorhanden. Geben Sie eine neue, entweder über das Präfix ändern oder ein anderes Suffix aus der Liste auswählen.  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig02_DupUPNMod.gif)  
  
### <a name="active-directory-administrative-center-dsacexe"></a>Active Directory Administrative Center (DSAC.exe)  
Der Versuch, einen neuen Benutzer in Active Directory Administrative Center mit dem Benutzerprinzipalnamen erstellen, die bereits vorhanden ist, wird den folgenden Fehler ergeben.  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig03_DupUPNADAC.gif)  
  
**Figure SEQ Abbildung \\\ * Arabisch 1-Fehler, die in Active Directory-Verwaltungscenter angezeigt, wenn die Erstellung des neuen Benutzers aufgrund eines doppelten UPN fehl**  
  
### <a name="event-2974-source-activedirectorydomainservice"></a>Ereignis 2974 – Quelle: ActiveDirectory_DomainService  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig04_Event2974.gif)  
  
**Figure SEQ Abbildung \\\ * Arabisch 2-Ereignis-ID 2974 mit Fehler 8648**  
  
Ereignis 2974 – enthält den Wert, der blockiert wurde und eine Liste der eines oder mehrere Objekte (bis zu 10), die diesem Wert bereits enthalten.  In der folgenden Abbildungsehen Sie die UPN-Attributwert ***dhunt@blue.contoso.com***auf vier weitere Objekte bereits vorhanden ist.  Da es sich um ein neues Feature in Windows Server2012 R2 handelt, wird versehentliche Erstellung von doppelten UPN und Dienstprinzipalnamen (SPN) in einer gemischten Umgebung weiterhin auftreten, wenn älteren DCs der versuchte Schreibvorgang verarbeiten.  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig05_Event2974ShowAllDups.gif)  
  
**Figure SEQ Abbildung \\\ * Arabisch 3 Ereignis 2974 Anzeige aller Objekte, die mit der doppelten UPN**  
  
> [!TIP]  
> Ereignis-ID 2974s regelmäßig zu überprüfen:  
>   
> -   Identifizieren Sie Versuche, doppelte Benutzerprinzipalnamen oder SPN zu erstellen  
> -   Identifizieren von Objekten, die bereits Duplikate enthalten  
  
8648 = "Den Vorgang ist fehlgeschlagen, da der UPN-Wert für die Hinzufügung/Änderung nicht eindeutigen Gesamtstruktur ist."  
  
### <a name="setspn"></a>SetSPN:  
Setspn.exe wurde doppelten SPN-Erkennung seit der Veröffentlichung von Windows Server2008 integriert, bei Verwendung der **"-S"** Option.  Sie können die doppelte SPN-Erkennung umgehen, indem Sie mit der **"-A"** Option jedoch.  Erstellen einer doppelten SPN ist blockiert, wenn auf einem Windows Server2012 R2-Domänencontroller, SetSPN verwenden, mit der Option-a.  Die angezeigte Fehlermeldung ist identisch mit den angezeigt, wenn die Option -S: "Duplicate SPN gefunden, wird der Vorgang abgebrochen"!  
  
### <a name="adsiedit"></a>ADSIEDIT:  
  
```  
Operation failed. Error code: 0x21c8  
The operation failed because UPN value provided for addition/modification is not unique forest-wide.  
000021C8: AtrErr: DSID-03200BBA, #1: 0: 000021C8: DSID-03200BBA, problem 1005 (CONSTRAINT_ATT_TYPE), data 0, Att 90290 (userPrincipalName)  
```  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig06_ADSI21c8.gif)  
  
**Figure SEQ Abbildung \\\ * Arabisch 4 angezeigte Fehlermeldung in ADSIEdit beim Hinzufügen von doppelten UPN blockiert wird**  
  
### <a name="windows-powershell"></a>WindowsPowerShell  
Windows Server2012 R2:  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig07_SetADUser2012.gif)  
  
PS aus einem Windows Server2012 R2-Domänencontroller für Server2012 ausgeführt:  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig08_SetADUser2012R2.gif)  
  
DSAC.exe unter Windows Server2012 auf einem Windows Server2012 R2-Domänencontroller:  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig09_UserCreateError.gif)  
  
**Figure SEQ Abbildung \\\ * Arabisch 5 gilt Folgendes Benutzer – Fehler beim Erstellen auf nicht - Windows Server2012 R2 beim Abzielen auf Windows Server2012 R2-Domänencontroller**  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig10_UserModError.gif)  
  
**Figure SEQ Abbildung \\\ * Arabisch 6 gilt Folgendes Änderung Benutzerfehler auf nicht - Windows Server2012 R2 beim Abzielen auf Windows Server2012 R2-Domänencontroller**  
  
### <a name="restore-of-an-object-that-would-result-in-a-duplicate-upn-fails"></a>Wiederherstellen eines Objekts, das einen doppelten UPN würde ein Fehler auftritt:  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig11_RestoreDupUPN.gif)  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig12_RestoreDupUPNError.gif)  
  
Es wird kein Ereignis protokolliert, wenn ein Objekt nicht aufgrund eines doppelten UPN wiederherstellen / SPN.  
  
Der UPN des Objekts muss in der Reihenfolge wiederhergestellt werden, damit eindeutig sein.  
  
1.  Identifizieren Sie den UPN, die für das Objekt in den Papierkorb vorhanden sind.  
  
2.  Identifizieren Sie alle Objekte, die den gleichen Wert aufweisen.  
  
3.  Entfernen Sie die doppelten UPNs  
  
### <a name="identify-the-conflicting-upn-on-the-deleted-objectusing-repadminexe"></a>Identifizieren Sie den in Konflikt stehenden UPN der gelöschten ObjectUsing repadmin.exe  
  
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
  
### <a name="to-identify-all-objects-with-the-same-upnusing-repadminexe"></a>Um alle Objekte mit den gleichen UPN zu identifizieren: verwenden Repadmin.exe  
  
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
> Die zuvor nicht dokumentierte **/ gelöscht** Parameter im repadmin.exe wird verwendet, um gelöschte Objekte in dem Ergebnis einschließen  
  
### <a name="using-global-search"></a>Mithilfe der globalen Suche  
  
-   Öffnen Sie Active Directory-Verwaltungscenter und navigieren Sie zu **globale Suche**  
  
-   Wählen Sie die **in LDAP konvertieren** Optionsfeld  
  
-   Typ **(UserPrincipalName =*ConflictingUPN*) **  
  
    -   Ersetzen Sie ***ConflictingUPN*** mit der tatsächlichen UPN dem in Konflikt  
  
-   Wählen Sie **anwenden**  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig13_GlobalSearch.gif)  
  
### <a name="using-windows-powershell"></a>Mithilfe von WindowsPowerShell  
  
```  
Get-ADObject -LdapFilter "(userPrincipalName=dhunt@blue.contoso.com)" -IncludeDeletedObjects -SearchBase "DC=blue,DC=Contoso,DC=com" -SearchScope Subtree -Server winbluedc1.blue.contoso.com  
```  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig13_GlobalSearchPS.gif)  
  
Wenn das Objekt werden wiederhergestellt muss, werden Sie die doppelten UPNs von anderen Objekten entfernen müssen.  Nur ein Objekt ist es einfach ADSIEdit verwenden, um das Duplikat zu entfernen.  Wenn mehrere Objekte mit Duplikate vorhanden sind, möglicherweise Windows PowerShell die bessere Tool verwenden.  
  
Auf NULL fest, das UserPrincipalName-Attribut, das mithilfe von Windows PowerShell:  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig15_NullUPN.gif)  
  
> [!NOTE]  
> Das UserPrincipalName-Attribut ist einwertiges Attribut, damit Sie dieses Verfahren nur den doppelten UPN entfernt werden soll.  
  
### <a name="duplicate-spn"></a>Doppelten SPN  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig16_DupSPN.gif)  
  
**Figure SEQ Abbildung \\\ * Arabisch 8 angezeigte Fehlermeldung in ADSIEdit beim Hinzufügen von doppelten SPN blockiert wird**  
  
In den Verzeichnisdiensten im Ereignisprotokoll wird protokolliert eine **ActiveDirectory_DomainService** Ereignis-ID **2974**.  
  
```  
Operation failed. Error code: 0x21c7  
The operation failed   
The attribute value provided is not unique in the forest or partition. Attribute:  
servicePrincipalName Value=<SPN>  
<Object DN> Winerror: 8467  
```  
  
![SPN- und UPN-Eindeutigkeit](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig17_DupSPN2974.gif)  
  
**Figure SEQ Abbildung \\\ * Arabisch 9 Fehler protokolliert, wenn die Erstellung von doppelten SPN blockiert wird**  
  
### <a name="workflow"></a>Workflow  
  
-   **Wenn Domänencontroller == GC**  
  
    -   Kein Off-Box-Aufruf erforderlich, die Abfrage lokal erfüllt werden kann  
  
    -   ***UPN-Anfrage***  
  
        -   Abfrage lokale Gesamtstruktur UPN-Index für die angegebenen UPN (*UserPrincipalName; globaler Index*)  
  
            -   Wenn Einträge zurückgegeben == 0 -> Write-Erlöse  
  
            -   Wenn Einträge zurückgegeben! = 0 -> schreiben ein Fehler auftritt.  
  
                -   Ereignis protokolliert  
  
                -   Außerdem gibt erweiterten Fehler zurück:  
  
                    -   **8648:**  
  
                        *ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
    -   ***SPN Groß-/Kleinschreibung***  
  
        -   Abfrage lokale Gesamtstruktur SPN Index für bereitgestellten SPN (*ServicePrincipalName; globaler Index*)  
  
            -   Wenn Einträge zurückgegeben == 0 -> Write-Erlöse  
  
            -   Wenn Einträge zurückgegeben! = 0 -> schreiben ein Fehler auftritt.  
  
                -   Ereignis protokolliert  
  
                -   Außerdem gibt erweiterten Fehler zurück:  
  
                    -   **8647:**  
  
                        **ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST**  
  
-   **Wenn Domänencontroller! = GC**  
  
    -   Off-Box-Aufruf **wünschenswert** jedoch nicht wichtig sind, d.h. eine Überprüfung der bestmöglichen Eindeutigkeit  
  
        -   Überprüfen Sie vor lokalen DIT wird fortgesetzt, nur dann, wenn GC nicht gefunden werden kann  
  
        -   Ereignis protokolliert, um z.B. anzugeben  
  
    -   ***UPN-Anfrage***  
  
        -   Übermitteln Sie die LDAP-Abfrage am nächsten gelegenen GC? Abfragen des globalen Katalogs gesamtstrukturweite UPN Index für die angegebenen UPN (*UserPrincipalName; globaler Index*)  
  
            -   Wenn Einträge zurückgegeben == 0 -> Write-Erlöse  
  
            -   Wenn Einträge zurückgegeben! = 0 -> schreiben ein Fehler auftritt.  
  
                -   Ereignis protokolliert  
  
                -   Außerdem gibt erweiterten Fehler zurück:  
  
                    -   **8648:**  
  
                        *ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
    -   ***SPN Groß-/Kleinschreibung***  
  
        -   Übermitteln Sie die LDAP-Abfrage am nächsten gelegenen GC? Abfragen des globalen Katalogs gesamtstrukturweite SPN Index für bereitgestellten SPN (*ServicePrincipalName; globaler Index*)  
  
            -   Wenn Einträge zurückgegeben == 0 -> Write-Erlöse  
  
            -   Wenn Einträge zurückgegeben! = 0 -> schreiben ein Fehler auftritt.  
  
                -   Ereignis protokolliert  
  
                -   Außerdem gibt erweiterten Fehler zurück:  
  
                    -   **8647:**  
  
                        *ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
Wenn gelöschte Objekte erneut animierte sind, werden SPN oder UPN Werten auf Eindeutigkeit hin überprüft. Wenn ein Duplikat gefunden wird, schlägt die Anforderung fehl.  
  
-   Wenn die Änderung vorgenommen wird, werden Dienstprinzipalnamen (SPN) für bestimmte Attribut Änderungen wie DNS-Hostnamen, SAM-Konto Namen usw. entsprechend aktualisiert. Während dieses Prozesses die veralteten SPN gelöscht und neue SPN erstellt und der Datenbank hinzugefügt werden. Werden die erforderlichen Attribut Änderungen für die dieser Pfad ausgelöst wird:  
  
    -   ATT_DNS_HOST_NAME  
  
    -   ATT_MS_DS_ADDITIONAL_DNS_HOST_NAME  
  
    -   ATT_SAM_ACCOUNT_NAME  
  
    -   ATT_MS_DS_ADDITIONAL_SAM_ACCOUNT_NAME  
  
    -   ATT_SERVER_REFERENCE_BL  
  
    -   ATT_USER_ACCOUNT_CONTROL  
  
Wenn keines der neuen SPN-Wert ist ein Duplikat, fehl, wird die Änderung. Der oben genannten Liste sind die wichtigen Attribute ATT_DNS_HOST_NAME (Computername) und ATT_SAM_ACCOUNT_NAME (SAM-Kontoname).  
  
### <a name="try-this-exploring-spn-and-upn-uniqueness"></a>Versuchen Sie Folgendes: SPN- und UPN-Eindeutigkeit erkunden  
Dies ist der erste von mehreren "**versuchen Sie es**" Aktivitäten im Modul.  Es gibt keine separate testlab-Handbuch für dieses Modul.  Die **versuchen Sie es** Aktivitäten sind im Wesentlichen Freiform-Aktivitäten, mit denen Sie das Material Lektion in der Testumgebung durchsuchen.  Sie haben die Möglichkeit, befolgen die Eingabeaufforderung oder Skript verschwindet, und mit Ihren eigenen Aktivitäten zusammengestellt.  
  
> [!NOTE]  
> -   Dies ist der erste von mehreren "**versuchen Sie es**" Aktivitäten.  
> -   Es gibt keine separate testlab-Handbuch für dieses Modul.  
> -   Die **versuchen Sie es** Aktivitäten sind im Wesentlichen Freiform-Aktivitäten, mit denen Sie das Material Lektion in der Testumgebung durchsuchen.  
> -   Sie haben die Möglichkeit, befolgen die Eingabeaufforderung oder Skript verschwindet, und mit Ihren eigenen Aktivitäten zusammengestellt.  
> -   Zwar nicht alle Abschnitte enthalten eine **versuchen Sie es** dazu aufgefordert werden, es wird weiterhin empfohlen, den Lektionsinhalt im Labor gegebenenfalls entdecken.  
  
Experimentieren Sie mit SPN- und UPN-Eindeutigkeit.  Befolgen Sie diese Anweisungen aus, oder führen Sie Ihre eigene.  
  
1.  Erstellen Sie neue Benutzer mit UPN  
  
2.  Erstellen von Konten mit Dienstprinzipalnamen (SPN)  
  
3.  Erstellen Sie einen neuen Benutzer mit dem Benutzerprinzipalnamen bereits zuvor definierten oder ändern Sie ein vorhandenes Konto UPN.  Gleiches gilt für einen SPN für ein anderes Konto  
  
    1.  Füllen Sie ein vorhandenes Benutzerkonto mit dem Benutzerprinzipalnamen bereits in Verwendung  
  
        1.  Mithilfe von PowerShell, ADSIEDIT oder Active Directory-Verwaltungscenter (DSAC.exe)  
  
    2.  Füllen Sie ein Konto bei der SPN bereits in Verwendung  
  
        1.  Verwenden von Windows PowerShell, ADSIEDIT oder SetSPN  
  
4.  Beachten Sie die Fehler  
  
**Optional**  
  
1.  Dozenten Kursraum überprüfen Sie, ob es ok, um das Aktivieren der *[Active Directory-Papierkorb](https://technet.microsoft.com/library/jj574144.aspx#BKMK_EnableRecycleBin)* im Active Directory-Verwaltungscenter.  Wenn dies der Fall ist, fahren Sie mit dem nächsten Schritt.  
  
2.  Füllen Sie den UPN eines Benutzerkontos  
  
3.  Das Konto löschen  
  
4.  Füllen Sie ein anderes Konto mit den gleichen UPN als das gelöschte Konto  
  
5.  Versuchen Sie, die Recycle Bin GUI zu verwenden, um das Konto wiederherzustellen  
  
6.  Angenommen Sie, Sie mit dem Fehler nur gestellt worden sind, die Sie im vorherigen Schrittangezeigt.  (und keinen Verlauf der Schritte, die Sie gerade durchgeführt haben) Ihr Ziel ist die Wiederherstellung des Kontos abschließen.  Weitere Informationen finden Sie in die Arbeitsmappe z.B. die Schritte.  
  



---
ms.assetid: 7e195f5b-b194-40f3-a26d-5cf4ade5fc4d
title: Zertifizierungsstelle sichern und Wiederherstellen von Windows PowerShell-cmdlets
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: aba86ed080cc0b4043805531f0a2138b1b1d3cf8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="ca-backup-and-restore-windows-powershell-cmdlets"></a>Zertifizierungsstelle sichern und Wiederherstellen von Windows PowerShell-cmdlets

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012
>
**"Author"**: Justin Turner, Senior Support Escalation Engineer mit der Windows-Gruppe  
  
> [!NOTE]  
> Dieser Inhalt wird von Microsoft Customer Support-Mitarbeiter geschrieben und richtet erfahrene Administratoren und Systemarchitekten, die als Themen auf TechNet finden Sie in der Regel einen tieferen technischen Einblick Funktionen und Lösungen in Windows Server 2012 R2 suchen. Allerdings hat es nicht die gleichen linguistischen damit einige der Sprache möglicherweise weniger glänzend als was in der Regel auf TechNet-Website gefunden wird.  
  
## <a name="overview"></a>(Übersicht)  
Das ADCSAdministration Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.  Dieses Modul in Windows Server 2012 R2 unterstützen die Sicherung und Wiederherstellung von einer Zertifizierungsstelle wurden zwei neue Cmdlets hinzugefügt.  
  
-   Backup-CARoleService  
  
-   Restore-CARoleService  
  
## <a name="backup-caroleservice"></a>Backup-CARoleService  
**Tabelle SEQ Tabelle \\\ * Arabisch 17: Sichern und Wiederherstellen von Windows PowerShell-Cmdlets**  
  
**ADCSAdministration-Cmdlets: Backup-CARoleService**  
  
|Argumente - **fett** Argumente erforderlich sind.|Beschreibung|  
|------------------------------------------------|---------------|  
|**-Pfad**|-String - Speicherort zum Speichern der Sicherung<br />– Dies ist die einzige unbenannte parameter<br />-Positionsparameter<br /><br />**Beispiel:**<br /><br />Backup-CARoleService.-Pfad c:\adcsbackup1<br /><br />Backup-CARoleService c:\adcsbackup2|  
|-KeyOnly|-Zertifikat der Zertifizierungsstelle, ohne dass die Datenbank sichern<br /><br />**Beispiel:**<br /><br />Backup-CARoleService c:\adcsbackup3 - KeyOnly|  
|-Kennwort|-Gibt an, das Kennwort zum Schutz von ZS-Zertifikate und private Schlüssel<br />-Eine sichere Zeichenfolge muss sein werden.<br />– Mit dem Parameter - DatabaseOnly nicht gültig.<br /><br />Beispiel:<br /><br />Backup-CARoleService c:\adcsbackup4-Kennwort (Read-Host - Aufforderung "Kennwort:" - AsSecureString)<br /><br />Backup-CARoleService c:\adcsbackup5-Kennwort (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText - Force)|  
|-DatabaseOnly|-Sicherung der Datenbank ohne das Zertifikat der Zertifizierungsstelle<br /><br />Backup-CARoleService c:\adcsbackup6 - DatabaseOnly|  
|-Force|1. können Sie die Sicherung zu überschreiben, die in den angegebenen Speicherort Medienfreigabe im - Path-Parameter<br /><br />Backup-CARoleService c:\adcsbackup1-Force|  
|-Inkrementelle|-Führen Sie eine inkrementelle Sicherung<br /><br />Backup-CARoleService c:\adcsbackup7-inkrementelle|  
|-KeepLog|1. weist den Befehl an der Protokolldateien beibehalten möchten. Wenn die Option nicht angegeben ist, werden Protokolldateien standardmäßig mit Ausnahme der in der inkrementellen Szenario abgeschnitten.<br /><br />Backup-CARoleService c:\adcsbackup7 - KeepLog|  
  
### <a name="-password-secure-string"></a>-Kennwort<Secure String>  
Wenn das - Kennwort-Parameter wird verwendet, das angegebene Kennwort muss eine sichere Zeichenfolge sein.  Verwenden Sie die **Read-Host** Cmdlet, um eine interaktive Eingabeaufforderung für die Eingabe von sicheren Kennwörtern zu starten, oder verwenden Sie die **ConvertTo-SecureString** Cmdlet, um das Kennwort in Zeile angeben.  
  
Überprüfen Sie die folgenden Beispiele  
  
**Geben Sie eine sichere Zeichenfolge für den Kennwort-Parameter mit Read-Host**  
  
```powershell  
Backup-CARoleService c:\adcsbackup4 -Password (Read-Host -prompt "Password:" -AsSecureString)  
```  
  
**Geben Sie eine sichere Zeichenfolge für den Kennwort-Parameter, die mithilfe von ConvertTo-SecureString**  
  
```powershell  
Backup-CARoleService c:\adcsbackup5 -Password (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText -Force)  
```  
  
## <a name="restore-caroleservice"></a>Restore-CARoleService  
**ADCSAdministration-Cmdlets: Restore-CARoleService**  
  
|Argumente - **fett** Argumente erforderlich sind.|Beschreibung|  
|------------------------------------------------|---------------|  
|**-Pfad**|-String - Speicherort für die Sicherung wiederherstellen<br />– Dies ist die einzige unbenannte parameter<br />-Positionsparameter<br /><br />**Beispiel:**<br /><br />Wiederherstellen-CARoleService.-Pfad c:\adcsbackup1-Force<br /><br />Restore-CARoleService c:\adcsbackup2-Force|  
|-KeyOnly|-Zertifikat der Zertifizierungsstelle, ohne dass die Datenbank wiederherstellen<br />– Muss angegeben werden, wenn die Sicherung mit der Option - KeyOnly stammt<br /><br />**Beispiel:**<br /><br />Restore-CARoleService c:\adcsbackup3 - KeyOnly-Force|  
|-Kennwort|-Gibt das Kennwort für die ZS-Zertifikate und private Schlüssel<br />-Eine sichere Zeichenfolge muss sein werden.<br /><br />**Beispiel:**<br /><br />Restore-CARoleService c:\adcsbackup4-Kennwort (Read-Host - Aufforderung "Kennwort:" - AsSecureString)-Force<br /><br />Restore-CARoleService c:\adcsbackup5-Kennwort (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText - Force)-Force|  
|-DatabaseOnly|– Die Datenbank ohne das Zertifikat der Zertifizierungsstelle wiederherstellen<br /><br />Restore-CARoleService c:\adcsbackup6 - DatabaseOnly|  
|-Force|– Ermöglicht es Ihnen, die bereits vorhandene Schlüssel überschrieben.<br />-Ist ein optionaler Parameter beim direkten wiederherstellen zu können, ist jedoch wahrscheinlich erforderlich<br /><br />Restore-CARoleService c:\adcsbackup1-Force|  
  
### <a name="issues"></a>Probleme  
Eine geschützte keine Kennwörter Sicherung wird ausgeführt, wenn das ConvertTo-SecureString-Funktion ein Fehler auftritt, während der Verwendung der Backup-CARoleService mit dem Kennwort-Parameter.  
  
![Sicherung und Wiederherstellung](media/CA-Backup-and-Restore-Windows-PowerShell-cmdlets/GTR_ADDS_BackupCARole.gif)  
  
**Tabelle SEQ Tabelle \\\ * Arabisch 18: Allgemeine Fehler**  
  
|Aktion|Fehler|Kommentar|  
|----------|---------|-----------|  
|**Restore-CARoleService C:\ADCSBackup**|Restore-CARoleService: Der Prozess kann nicht die Datei zugreifen, da sie von einem anderen Prozess verwendet wird. (Ausnahme von HRESULT:<br /><br />0 x 80070020)|Beenden Sie den Active Directory Certificate Services-Dienst vor dem Ausführen des Cmdlets Restore-CARoleService|  
|**Restore-CARoleService C:\ADCSBackup**|Restore-CARoleService: Das Verzeichnis ist nicht leer. (Ausnahme von HRESULT: 0x80070091)|Mit dem - Force-Parameter auf bereits vorhandene Schlüssel überschrieben.|  
|**Backup-CARoleService C:\ADCSBackup-Kennwort (Read-Host - Aufforderung "Kennwort:" - AsSecureString) - DatabaseOnly**|Backup-CARoleService: Parametersatz kann nicht aufgelöst werden mit den angegebenen benannten Parameter.|-Kennwort-Parameter ist nur mit einem Kennwort verwendet, privaten Schlüssel zu schützen, und ist daher ungültig, wenn Sie nicht darauf sichern|  
|**Restore-CARoleService C:\ADCSBack15-Kennwort (Read-Host - Aufforderung "Kennwort:" - AsSecureString) - DatabaseOnly**|Restore-CARoleService: Parametersatz kann nicht aufgelöst werden mit den angegebenen benannten Parameter.|-Kennwort-Parameter ist nur mit einem Kennwort verwendete private Schlüssel zu schützen und ist daher ungültig, wenn Sie nicht wiederhergestellt werden|  
|**Restore-CARoleService C:\ADCSBack14-Kennwort (Read-Host - Aufforderung "Kennwort:" - AsSecureString)**|Restore-CARoleService: Das System kann nicht die angegebene Datei nicht finden. (Ausnahme von HRESULT: 0 x 80070002)|Der angegebene Pfad enthält eine gültige Sicherung nicht.  Möglicherweise ist der Pfad ungültig oder stammt die Sicherung, mit der Option - KeysOnly?|  
  
## <a name="additional-resources"></a>Zusätzliche Ressourcen  
[Active Directory Certificate Services Migration Guide](https://technet.microsoft.com/library/ee126170(v=ws.10).aspx)  
  
[Sichern der Datenbank der Zertifizierungsstelle und privaten Schlüssel](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_BackUpDB)  
  
[Wiederherstellen der Datenbank der Zertifizierungsstelle und die Konfiguration auf dem Zielserver](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_RestoreCA)  
  
## <a name="try-this-backup-the-ca-in-your-lab-using-windows-powershell"></a>Versuchen Sie Folgendes: Sicherung der Zertifizierungsstelle im Testlabor mithilfe von Windows PowerShell  
  
1.  Verwenden Sie die Befehle in dieser Lektion zum Sichern der Datenbank der Zertifizierungsstelle und den privaten Schlüssel mit einem Kennwort geschützt.  
  
2.  Halten Sie die Wiederherstellung der Zertifizierungsstelle zu diesem Zeitpunkt deaktiviert.  
  



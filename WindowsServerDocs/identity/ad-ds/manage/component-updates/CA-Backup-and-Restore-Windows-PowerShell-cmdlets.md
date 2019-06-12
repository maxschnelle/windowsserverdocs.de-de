---
ms.assetid: 7e195f5b-b194-40f3-a26d-5cf4ade5fc4d
title: CA-sichern und Wiederherstellen von Windows PowerShell-cmdlets
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 6055d9b694f72a6a874acdcb5135fde61bcf0d76
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442753"
---
# <a name="ca-backup-and-restore-windows-powershell-cmdlets"></a>CA-sichern und Wiederherstellen von Windows PowerShell-cmdlets

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
> 
> **Autor**: Justin Turner, Senior Support Escalation Engineer für die Windows-Gruppe  
> 
> [!NOTE]
> Dieser Inhalt wurde von einem Mitarbeiter des Microsoft-Kundendiensts geschrieben und richtet sich an erfahrene Administratoren und Systemarchitekten, die einen tieferen technischen Einblick in die Funktionen und Lösungen von Windows Server 2012 R2 suchen, als Ihnen die Themen im TechNet bieten können. Allerdings wurde er nicht mit der gleichen linguistischen Sorgfalt überprüft wie für die Artikel des TechNet üblich, so dass die Sprache gelegentlich holprig klingen mag.  
  
## <a name="overview"></a>Übersicht  
Das ADCSAdministration Windows PowerShell-Modul wurde in Windows Server 2012 eingeführt.  Dieses Modul in Windows Server 2012 R2 zur Unterstützung der Sicherung und Wiederherstellung von einer Zertifizierungsstelle wurden zwei neue Cmdlets hinzugefügt.  
  
-   Backup-CARoleService  
  
-   Restore-CARoleService  
  
## <a name="backup-caroleservice"></a>Backup-CARoleService  
**Tabelle SEQ Tabelle \\ \* Arabische 17: Sicherung und Wiederherstellung, Windows PowerShell-Cmdlets**  
  
**ADCSAdministration-Cmdlet: Backup-CARoleService**  
  
|Argumente - **fett** Argumente sind erforderlich|Beschreibung|  
|------------------------------------------------|---------------|  
|**-Path**|– Zeichenfolge – Speicherort zum Speichern der sicherungs<br />– Dies ist die einzige unbenannte parameter<br />-Positionsparameter<br /><br />**Beispiel:**<br /><br />Backup-CARoleService.-Path c:\adcsbackup1<br /><br />Backup-CARoleService c:\adcsbackup2|  
|-KeyOnly|– Sichern Sie das Zertifizierungsstellenzertifikat, ohne dass die Datenbank<br /><br />**Beispiel:**<br /><br />Backup-CARoleService c:\adcsbackup3 -KeyOnly|  
|-Password|-Gibt an, das Kennwort zum Schutz von ZS-Zertifikate und private Schlüssel<br />-Eine sichere Zeichenfolge muss sein<br />-Mit dem Parameter - DatabaseOnly nicht gültig.<br /><br />Beispiel:<br /><br />Backup-CARoleService c:\adcsbackup4 -Password (Read-Host -prompt "Password:" -AsSecureString)<br /><br />Backup-CARoleService c:\adcsbackup5-Kennwort (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText -Force)|  
|-DatabaseOnly|– Sichern Sie die Datenbank ohne das Zertifizierungsstellenzertifikat<br /><br />Backup-CARoleService c:\adcsbackup6 -DatabaseOnly|  
|-Force|1.  Können Sie die Sicherung zu überschreiben, die in der angegebenen Position Medienfreigabe im - Path-Parameter<br /><br />Backup-CARoleService c:\adcsbackup1 -Force|  
|-Inkrementell|– Führt eine inkrementelle Sicherung<br /><br />Backup-CARoleService c:\adcsbackup7-inkrementell|  
|-KeepLog|1.  Weist den Befehl aus, um Protokolldateien zu halten. Wenn der Schalter nicht angegeben ist, werden Protokolldateien standardmäßig außer im inkrementellen Szenario abgeschnitten.<br /><br />Backup-CARoleService c:\adcsbackup7 -KeepLog|  
  
### <a name="-password-secure-string"></a>-Kennwort <Secure String>  
Wenn das - Kennwort Parameter wird verwendet, die das angegebene Kennwort muss eine sichere Zeichenfolge sein.  Verwenden Sie die **Read-Host** Cmdlet, um eine interaktive Eingabeaufforderung zur Eingabe des sicheren Kennworts zu starten, oder verwenden Sie die **ConvertTo-SecureString** Cmdlets, um das Kennwort Inline anzugeben.  
  
Überprüfen Sie die folgenden Beispiele  
  
**Eine sichere Zeichenfolge für den Parameter für das Kennwort mit der Read-Host angeben**  
  
```powershell  
Backup-CARoleService c:\adcsbackup4 -Password (Read-Host -prompt "Password:" -AsSecureString)  
```  
  
**Eine sichere Zeichenfolge für die mithilfe von ConvertTo-SecureString-Parameter für das Kennwort angeben**  
  
```powershell  
Backup-CARoleService c:\adcsbackup5 -Password (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText -Force)  
```  
  
## <a name="restore-caroleservice"></a>Restore-CARoleService  
**ADCSAdministration-Cmdlet: Restore-CARoleService**  
  
|Argumente - **fett** Argumente sind erforderlich|Beschreibung|  
|------------------------------------------------|---------------|  
|**-Path**|– Zeichenfolge – Speicherort für die Wiederherstellung aus<br />– Dies ist die einzige unbenannte parameter<br />-Positionsparameter<br /><br />**Beispiel:**<br /><br />Restore-CARoleService.-Path c:\adcsbackup1 -Force<br /><br />Restore-CARoleService c:\adcsbackup2 -Force|  
|-KeyOnly|-Das ZS-Zertifikat, ohne dass die Datenbank wird wiederhergestellt<br />-Muss angegeben werden, wenn die Sicherung, mit der Option - KeyOnly erstellt wurde<br /><br />**Beispiel:**<br /><br />Restore-CARoleService c:\adcsbackup3 -KeyOnly -Force|  
|-Password|-Gibt an, das Kennwort für die ZS-Zertifikate und privaten Schlüssel<br />-Eine sichere Zeichenfolge muss sein<br /><br />**Beispiel:**<br /><br />Restore-CARoleService c:\adcsbackup4 -Password (read-host -prompt "Password:" -AsSecureString) -Force<br /><br />Restore-CARoleService c:\adcsbackup5-Kennwort (ConvertTo-SecureString "Pa55w0rd!" -AsPlainText -Force) -Force|  
|-DatabaseOnly|: Wiederherstellen der Datenbank ohne das Zertifizierungsstellenzertifikat<br /><br />Restore-CARoleService c:\adcsbackup6 - DatabaseOnly|  
|-Force|– Ermöglicht es Ihnen, die bereits vorhandene Schlüssel überschrieben.<br />-Ist ein optionaler Parameter, aber wenn Sie ein direktes wiederherstellen zu können, ist es wahrscheinlich erforderlich<br /><br />Restore-CARoleService c:\adcsbackup1-Force|  
  
### <a name="issues"></a>Issues  
Eine nicht kennwortgestützte geschützten Sicherung, wenn die ConvertTo-SecureString-Funktion ein Fehler auftritt, bei der Verwendung der Backup-CARoleService mit dem Kennwort-Parameter.  
  
![Sicherung und Wiederherstellung](media/CA-Backup-and-Restore-Windows-PowerShell-cmdlets/GTR_ADDS_BackupCARole.gif)  
  
**Tabelle SEQ Tabelle \\ \* Arabische 18: Häufige Fehler**  
  
|Aktion|Fehler|Kommentar|  
|----------|---------|-----------|  
|**Restore-CARoleService C:\ADCSBackup**|Restore-CARoleService: Der Prozess kann nicht auf die Datei zugreifen, da sie von einem anderen Prozess verwendet wird. (Ausnahme von HRESULT:<br /><br />0x80070020)|Beenden Sie den Dienst Active Directory Certificate Services, bevor Sie das Cmdlet "Restore-CARoleService" ausführen|  
|**Restore-CARoleService C:\ADCSBackup**|Restore-CARoleService: Das Verzeichnis ist nicht leer. (Ausnahme von HRESULT: 0x80070091)|Verwendet den - Force-Parameter zum Überschreiben der vorhandenen Schlüssel|  
|**Backup-CARoleService C:\ADCSBackup -Password (Read-Host -Prompt "Password:" -AsSecureString) -DatabaseOnly**|Backup-CARoleService: Parametersatz kann nicht mit dem Namen Parameter aufgelöst werden unter Verwendung des angegebenen.|-Password-Parameter ist nur das Kennwort zum Schützen Sie private Schlüssel und ist daher ungültig, wenn Sie nicht diese sichern|  
|**Restore-CARoleService C:\ADCSBack15 -Password (Read-Host -Prompt "Password:" -AsSecureString) -DatabaseOnly**|Restore-CARoleService: Parametersatz kann nicht mit dem Namen Parameter aufgelöst werden unter Verwendung des angegebenen.|-Password-Parameter ist nur das Kennwort zum Schützen Sie private Schlüssel und ist daher ungültig, wenn Sie nicht wiederherstellen möchten|  
|**Restore-CARoleService C:\ADCSBack14 -Password (Read-Host -Prompt "Password:" -AsSecureString)**|Restore-CARoleService: Die angegebene Datei wurde nicht gefunden. (Ausnahme von HRESULT: 0x80070002)|Der angegebene Pfad enthält keine gültige Datenbank-Sicherung.  Möglicherweise ist der Pfad ungültig, oder erstellt die Sicherung mit der Option - KeysOnly wurde?|  
  
## <a name="additional-resources"></a>Zusätzliche Ressourcen  
[Anleitung für die Migration von Active Directory Certificate Services](https://technet.microsoft.com/library/ee126170(v=ws.10).aspx)  
  
[Sichern der Datenbank der Zertifizierungsstelle und des privaten Schlüssels](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_BackUpDB)  
  
[Wiederherstellen der Datenbank und Konfiguration der Zertifizierungsstelle auf dem Zielserver](https://technet.microsoft.com/library/ee126140(v=ws.10).aspx#BKMK_RestoreCA)  
  
## <a name="try-this-backup-the-ca-in-your-lab-using-windows-powershell"></a>Versuchen Sie Folgendes aus: Sichern Sie die Zertifizierungsstelle in Ihrem Lab mithilfe von Windows PowerShell  
  
1.  Verwenden Sie die Befehle in dieser Lektion sichern Sie die Datenbank der Zertifizierungsstelle und den privaten Schlüssel, die mit einem Kennwort geschützt.  
  
2.  Warten Sie auf die Wiederherstellung der Zertifizierungsstelle zu diesem Zeitpunkt.  
  



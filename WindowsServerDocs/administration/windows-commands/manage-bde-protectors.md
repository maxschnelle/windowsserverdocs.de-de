---
title: manage-bde-Schutzvorrichtungen
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1f9b22c5-cc93-45df-9165-bedee94998da
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/06/2018
ms.openlocfilehash: c248a5d7c6a25ccb6fa2917358223fd255a3c600
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820630"
---
# <a name="manage-bde-protectors"></a>manage-bde: Schutzvorrichtungen

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Verwaltet die Schutzmethoden, die für den BitLocker-Verschlüsselungsschlüssel verwendet werden.
## <a name="syntax"></a>Syntax
```
manage-bde -protectors [{-get|-add|-delete|-disable|-enable|-adbackup|-aadbackup}] <Drive> [-computername <Name>] [{-?|/?}] [{-help|-h}]
```
#### <a name="parameters"></a>Parameter

|   Parameter   |                                                                                                                                                                                           BESCHREIBUNG                                                                                                                                                                                            |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     -Get      |                                                                                                                                            Zeigt alle auf dem Laufwerk aktivierten Schlüsselschutz Methoden an und gibt ihren Typ und Bezeichner (ID) an.                                                                                                                                             |
|     -Hinzufügen      |                                                                                                                                   Fügt mit zusätzlichen [Parametern hinzufügen](manage-bde-protectors.md#BKMK_addprotectors)Schlüsselschutz Methoden hinzu.                                                                                                                                    |
|    -delete    | Löscht Schlüsselschutz Methoden, die von BitLocker verwendet werden. Alle Schlüssel Schutzvorrichtungen werden von einem Laufwerk entfernt, es sei denn, die [Parameter "-Delete](manage-bde-protectors.md#BKMK_deleteprotectors) " werden verwendet, um anzugeben, welche Schutzvorrichtungen gelöscht werden sollen. Wenn die letzte Schutzvorrichtung auf einem Laufwerk gelöscht wird, wird der BitLocker-Schutz des Laufwerks deaktiviert, um sicherzustellen, dass der Zugriff auf die Daten nicht versehentlich verloren geht. |
|   -disable    |                      Deaktiviert den Schutz, mit dem jeder auf verschlüsselte Daten zugreifen kann, indem der Verschlüsselungsschlüssel auf dem Laufwerk nicht gesichert wird. Es werden keine Schlüssel Schutzvorrichtungen entfernt. Der Schutz wird beim nächsten Start von Windows fortgesetzt, es sei denn, mit den optionalen [Parametern "-deaktivieren](manage-bde-protectors.md#BKMK_disableprot) " können Sie die Neustart Anzahl angeben.                       |
|    -enable    |                                                                                                                             Ermöglicht den Schutz, indem der unsichere Verschlüsselungsschlüssel vom Laufwerk entfernt wird. Alle konfigurierten Schlüssel Schutzvorrichtungen auf dem Laufwerk werden erzwungen.                                                                                                                             |
|   -adbackup   |                                                                          Sichert alle Wiederherstellungs Informationen für das angegebene Laufwerk Active Directory Domain Services (AD DS). Wenn Sie nur einen einzelnen Wiederherstellungs Schlüssel in AD DS sichern möchten, fügen Sie den Parameter **-ID** an, und geben Sie die ID eines bestimmten Wiederherstellungs Schlüssels an, der gesichert werden soll.                                                                           |
|  -aadbackup   |                                                                            Sichert alle Wiederherstellungs Informationen für das angegebene Laufwerk Azure Active Directory (Azure AD). Wenn Sie nur einen einzelnen Wiederherstellungs Schlüssel in Azure AD sichern möchten, fügen Sie den Parameter **-ID** an, und geben Sie die ID eines bestimmten Wiederherstellungs Schlüssels an, der gesichert werden soll.                                                                             |
|    <Drive>    |                                                                                                                                                                          Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.                                                                                                                                                                          |
| -Computername |                                                                                                              Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden.                                                                                                              |
|    <Name>     |                                                                                                                 Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.                                                                                                                  |
|   -? oder /?    |                                                                                                                                                                            Zeigt eine kurze Hilfe an der Eingabeaufforderung an.                                                                                                                                                                            |
|  -Help oder-h  |                                                                                                                                                                          Zeigt die gesamte Hilfe an der Eingabeaufforderung an.                                                                                                                                                                           |

### <a name="-add-syntax-and-parameters"></a><a name=BKMK_addprotectors></a>-Hinzufügen von Syntax und Parametern
```
manage-bde  -protectors  -add [<Drive>] [-forceupgrade] [-recoverypassword <NumericalPassword>] [-recoverykey <pathToExternalKeydirectory>]
[-startupkey <pathToExternalKeydirectory>] [-certificate {-cf <pathToCertificateFile>|-ct <CertificateThumbprint>}] [-tpm] [-tpmandpin]
[-tpmandstartupkey <pathToExternalKeydirectory>] [-tpmandpinandstartupkey <pathToExternalKeydirectory>] [-password][-adaccountorgroup <securityidentifier> [-computername <Name>]
[{-?|/?}] [{-help|-h}]
```

|          Parameter           |                                                                                                                                                                                   BESCHREIBUNG                                                                                                                                                                                   |
|------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           <Drive>            |                                                                                                                                                                 Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.                                                                                                                                                                  |
|      -wiederherstellungkennwort       |                                                                                                                                    Fügt eine numerische Kennwort-Schutzvorrichtung hinzu. Sie können auch **-RP** als abgekürzte Version dieses Befehls verwenden.                                                                                                                                     |
|     <NumericalPassword>      |                                                                                                                                                                        Stellt das Wiederherstellungs Kennwort dar.                                                                                                                                                                        |
|         -Wiederherstellungsschlüssel         |                                                                                                                                Fügt eine externe Schlüssel Schutzvorrichtung für die Wiederherstellung hinzu. Sie können " **-RK** " auch als abgekürzte Version dieses Befehls verwenden.                                                                                                                                 |
| <pathToExternalKeydirectory> |                                                                                                                                                               Stellt den Verzeichnispfad zum Wiederherstellungs Schlüssel dar.                                                                                                                                                                |
|         -startupkey          |                                                                                                                                 Fügt eine externe Schlüssel Schutzvorrichtung zum Starten hinzu. Sie können auch **-SK** als abgekürzte Version dieses Befehls verwenden.                                                                                                                                 |
| <pathToExternalKeydirectory> |                                                                                                                                                                Stellt den Verzeichnispfad zum Systemstart Schlüssel dar.                                                                                                                                                                |
|         -Zertifikat         |                                                                                                                               Fügt eine Schutzvorrichtung für ein öffentliches Schlüssel für ein Daten Laufwerk hinzu. Sie können auch **-CERT** als abgekürzte Version dieses Befehls verwenden.                                                                                                                               |
|             -cf              |                                                                                                                                              Gibt an, dass eine Zertifikatsdatei verwendet wird, um das Zertifikat für öffentliche Schlüssel bereitzustellen.                                                                                                                                              |
|   <pathToCertificateFile>    |                                                                                                                                                             Stellt den Verzeichnispfad zur Zertifikatsdatei dar.                                                                                                                                                              |
|             -CT              |                                                                                                                                           Gibt an, dass ein Zertifikat Fingerabdruck verwendet wird, um das Zertifikat für öffentliche Schlüssel zu identifizieren.                                                                                                                                           |
|   <CertificateThumbprint>    |                                                       Gibt den Wert der Eigenschaft "Fingerabdruck" des Zertifikats an, das Sie verwenden möchten. Beispielsweise sollte der Wert des Zertifikat Fingerabdrucks A9 09 50 2D D8 2a E4 14 33 E6 F8 38 86 B0 0d 42 77 a3 2a 7B als a909502dd82ae41433e6f83886b00d4277a32a7b angegeben werden.                                                        |
|          -TPMAndPIN          |                                                                                           Fügt ein Trusted Platform Module (TPM) und eine PIN-Schutzvorrichtung (Personal Identification Number) für das Betriebssystem Laufwerk hinzu. Sie können auch **-tp** als abgekürzte Version dieses Befehls verwenden.                                                                                           |
|      -TPMAndStartupKey       |                                                                                                                    Fügt ein TPM und eine Systemstart Schlüssel-Schutzvorrichtung für das Betriebssystem Laufwerk hinzu. Sie können auch **-TSK** als abgekürzte Version dieses Befehls verwenden.                                                                                                                    |
|   -tpmandpinandstartupkey    |                                                                                                                Fügt ein TPM, eine PIN und eine Start Schlüsselschutzvorrichtung für das Betriebssystem Laufwerk hinzu. Sie können auch **-tpsk** als abgekürzte Version dieses Befehls verwenden.                                                                                                                 |
|          -password           |                                                                                                                              Fügt eine Kenn Wort Schlüssel-Schutzvorrichtung für das Daten Laufwerk hinzu. Sie können auch **-PW** als abgekürzte Version dieses Befehls verwenden.                                                                                                                              |
|      -adaccountorgroup       | Fügt eine Sicherheits-ID (SID)-basierte Identitäts Schutzvorrichtung für das Volume hinzu.  Sie können auch **-sid** als abgekürzte Version dieses Befehls verwenden. **Wichtig:** Standardmäßig ist es nicht möglich, eine adaccountorgroup-Schutzvorrichtung mithilfe von WMI oder manage-bde Remote hinzuzufügen.  Wenn Ihre Bereitstellung die Möglichkeit erfordert, diese Schutzvorrichtung Remote hinzuzufügen, müssen Sie die eingeschränkte Delegierung aktivieren. |
|        -Computername         |                                                                                                       Gibt an, dass "Manage-BDE" verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden.                                                                                                       |
|            <Name>            |                                                                                                         Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.                                                                                                         |

### <a name="-delete-syntax-and-parameters"></a><a name=BKMK_deleteprotectors></a>-Löschen von Syntax und Parametern
```
manage-bde  -protectors  -delete <Drive> [-type {recoverypassword|externalkey|certificate|tpm|tpmandstartupkey|tpmandpin|tpmandpinandstartupkey|Password|Identity}]
[-id <KeyProtectorID>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

|       Parameter        |                                                                              BESCHREIBUNG                                                                               |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        <Drive>         |                                                             Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.                                                             |
|         -Typ          |                               Identifiziert die zu löschende Schlüssel Schutzvorrichtung. Sie können auch **-t** als abgekürzte Version dieses Befehls verwenden.                               |
|    RecoveryPassword    |                                                 Gibt an, dass alle Schutz Kennwort-Schlüssel Schutzvorrichtungen gelöscht werden sollen.                                                 |
|      ExternalKey       |                                        Gibt an, dass alle dem Laufwerk zugeordneten externen Schlüsselschutz Vorrichtungen gelöscht werden sollen.                                         |
|      Zertifikat       |                                       Gibt an, dass alle dem Laufwerk zugeordneten Zertifikat Schlüsselschutz Vorrichtungen gelöscht werden sollen.                                       |
|          TPM           |                                        Gibt an, dass alle dem Laufwerk zugeordneten TPM-Schlüsselschutz Vorrichtungen gelöscht werden sollen.                                         |
|    TPMAndStartupKey    |                                Gibt an, dass alle dem Laufwerk zugeordneten TPM-und systemeigenen Schlüsselschutz Vorrichtungen gelöscht werden sollen.                                |
|       TPMAndPIN        |                                    Gibt an, dass alle dem Laufwerk zugeordneten TPM-und PIN-basierten Schlüsselschutz Vorrichtungen gelöscht werden sollen.                                    |
| tpmandpinandstartupkey |                             Gibt an, dass alle dem Laufwerk zugeordneten TPM-, PIN-und Start Schlüssel-Schlüssel Schutzvorrichtungen gelöscht werden sollen.                             |
|        password        |                                        Gibt an, dass alle dem Laufwerk zugeordneten Kennwort-Schlüsselschutz Vorrichtungen gelöscht werden sollen.                                         |
|        Identität        |                                        Gibt an, dass alle dem Laufwerk zugeordneten Identitätsschlüssel Schutzvorrichtungen gelöscht werden sollen.                                         |
|          -ID           |                Identifiziert die zu löschende Schlüssel Schutzvorrichtung mithilfe des Schlüssel Bezeichners. Dieser Parameter ist eine alternative Option für den **-Type-** Parameter.                 |
|    <KeyProtectorID>    |        Identifiziert eine einzelne Schlüssel Schutzvorrichtung auf dem zu löschenden Laufwerk. Schlüsselschutzschutzids können mithilfe des Befehls **manage-bde-Protector-Get** angezeigt werden.         |
|     -Computername      | Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden. |
|         <Name>         |    Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.     |
|        -? oder /?        |                                                               Zeigt eine kurze Hilfe an der Eingabeaufforderung an.                                                               |
|      -Help oder-h       |                                                             Zeigt die gesamte Hilfe an der Eingabeaufforderung an.                                                              |

### <a name="-disable-syntax-and-parameters"></a><a name=BKMK_disableprot></a>-Deaktivieren von Syntax und Parametern
```
manage-bde  -protectors  -disable <Drive> [-RebootCount <integer 0 - 15>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

|   Parameter   |                                                                                                                                                                                                                   BESCHREIBUNG                                                                                                                                                                                                                    |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <Drive>    |                                                                                                                                                                                                  Stellt einen von einem Doppelpunkt gefolgten Laufwerkbuchstaben dar.                                                                                                                                                                                                  |
|  Rebootcount  | Ab Windows 8 gibt an, dass der Schutz für das Betriebssystem Volume angehalten wurde und fortgesetzt wird, sobald Windows neu gestartet wurde, und zwar so oft wie im Parameter "rebootcount" angegeben. Geben Sie 0 an, um den Schutz unbegrenzt anzuhalten. Wenn dieser Parameter nicht angegeben wird, wird der BitLocker-Schutz automatisch fortgesetzt, wenn Windows neu gestartet wird. Sie können auch **-RC** als abgekürzte Version dieses Befehls verwenden. |
| -Computername |                                                                                                                                      Gibt an, dass "manage-bde. exe verwendet wird, um den BitLocker-Schutz auf einem anderen Computer zu ändern. Sie können auch **-CN** als abgekürzte Version dieses Befehls verwenden.                                                                                                                                      |
|    <Name>     |                                                                                                                                         Stellt den Namen des Computers dar, auf dem der BitLocker-Schutz geändert werden soll. Akzeptierte Werte sind der NetBIOS-Name des Computers und die IP-Adresse des Computers.                                                                                                                                          |
|   -? oder /?    |                                                                                                                                                                                                    Zeigt eine kurze Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                    |
|  -Help oder-h  |                                                                                                                                                                                                  Zeigt die gesamte Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                   |

## <a name="examples"></a>Beispiele
Veranschaulicht die Verwendung des Befehls " **-** Protector" zum Hinzufügen einer durch eine Zertifikatsdatei identifizierten Zertifikat Schlüssel Schutzvorrichtung für Laufwerk E.
```
manage-bde  -protectors  -add E: -certificate  -cf c:\File Folder\Filename.cer
```
Veranschaulicht die Verwendung des Befehls "-Protector" zum Hinzufügen einer durch Domäne und Benutzername identifizierten **adaccountorgroup** **-** Schlüssel Schutzvorrichtung zu Laufwerk E.
```
manage-bde  -protectors  -add E: -sid DOMAIN\user
```
Veranschaulicht die Verwendung des **Befehls "** Protector", um den Schutz so lange zu deaktivieren, bis der Computer dreimal neu gestartet wurde.
```
manage-bde  -protectors  -disable C: -rc 3
```
Veranschaulicht die Verwendung des Befehls "-Protector", um alle TPM **-** und systemeigenen Schlüsselschutz Vorrichtungen auf Laufwerk C zu löschen.
```
manage-bde  -protectors -delete C: -type tpmandstartupkey
```
Veranschaulicht die Verwendung des Befehls " **-** Protector", um alle Wiederherstellungs Informationen für das Laufwerk C zu AD DS zu sichern.
```
manage-bde  -protectors  -adbackup C:
```
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [manage-bde](manage-bde.md)

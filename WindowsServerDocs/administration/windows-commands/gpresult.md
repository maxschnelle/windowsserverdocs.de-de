---
title: gpresult
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dfaa3adf-2c83-486c-86d6-23f93c5c883c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c5d96e7e1fcaeadbbc6b67e1c816a8810fd0e3b6
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811183"
---
# <a name="gpresult"></a>gpresult

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Zeigt die Informationen des Richtlinienergebnissatzes (RSoP) für einen remote-Benutzer und Computer.
Um RSoP-berichterstellung für Remote-Zielcomputer über die Firewall zu verwenden, müssen Sie Firewallregeln verfügen, die eingehenden Netzwerkdatenverkehr an den Ports zu ermöglichen.

## <a name="syntax"></a>Syntax

```
gpresult [/s <system> [/u <USERNAME> [/p [<PASSWOrd>]]]] [/user [<TARGETDOMAIN>\]<TARGETUSER>] [/scope {user | computer}] {/r | /v | /z | [/x | /h] <FILENAME> [/f] | /?}
```

## <a name="parameters"></a>Parameter

> [!NOTE]
> Außer bei Verwendung von **/?** , müssen Sie entweder eine Output-Option einschließen **/r**, **/v**, **Neustartmodus anzugeben**, **/x**, oder **/h**.

|                Parameter                 |                                                                                                     Beschreibung                                                                                                      |
|------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              / s \<System\>               |                                                  Gibt den Namen oder die IP-Adresse eines Remotecomputers. Verwenden Sie keine umgekehrte Schrägstriche. Der Standardwert ist der lokale Computer.                                                   |
|             / u \<Benutzername\>              |                                Verwendet die Anmeldeinformationen des angegebenen Benutzers zum Ausführen des Befehls. Der Standardbenutzer ist der Benutzer, die auf dem Computer angemeldet ist, der den Befehl ausgibt.                                 |
|            /p [\<PASSWOrd\>]             |            Gibt das Kennwort des Benutzerkontos ein, das bereitgestellt wird die **/u** Parameter. Wenn **/p** weggelassen wird, **Gpresult** fordert das Kennwort. **/ p** kann nicht verwendet werden, mit **/x** oder **/h**.            |
| / User [\<TARGETDOMAIN\>\\]\<TARGETUSER\> |                                                                            Gibt den remote-Benutzer ist, dessen RSoP-Daten angezeigt werden.                                                                             |
|      Bereich / {Benutzer &#124; Computer}       |                                Zeigt die RSoP-Daten für den Benutzer oder der Computer an. Wenn **Bereich/** weggelassen wird, **Gpresult** RSoP-Daten für den Benutzer und dem Computer angezeigt.                                 |
|        [/x &#124; /h] <FILENAME>         | Speichert den Bericht im XML ( **/x**) oder HTML ( **/h**) Format an der Position und mit dem Namen der Datei, die angegeben wird die *FILENAME* Parameter. Kann nicht verwendet werden, mit **/u**, **/p**, **/r**, **/v**, oder **Neustartmodus anzugeben**. |
|                    /f                    |                                                           Erzwingt, dass **Gpresult** um den Dateinamen zu überschreiben, die im angegebenen die **/x** oder **/h** Option.                                                           |
|                    /r                    |                                                                                             Zeigt zusammenfassende RSoP-Daten.                                                                                              |
|                    /v                    |                                                    Zeigt ausführliche Informationen. Dies umfasst detaillierte Einstellungen, die mit einer Priorität von 1 angewendet wurden.                                                    |
|                    /z                    |                                     Zeigt alle verfügbaren Informationen zu Gruppenrichtlinien. Dies umfasst detaillierte Einstellungen, die mit einer Priorität von 1 und höher angewendet wurden.                                      |
|                    /?                    |                                                                                         Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                         |

## <a name="remarks"></a>Hinweise
- Die Gruppenrichtlinie ist das primäre Verwaltungstool für definieren und zu steuern, wie Programme, Netzwerkressourcen und das Betriebssystem für Benutzer und Computer in einer Organisation ausgeführt werden. In einer active Directory-Umgebung wird die Gruppenrichtlinie für Benutzer oder Computer, die basierend auf seiner Mitgliedschaft in der Standorte, Domänen oder Organisationseinheiten angewendet.
- Da überlappende Richtlinieneinstellungen für alle Computer oder Benutzer angewendet werden kann, generiert das Gruppenrichtlinienfeature einen resultierenden Satz von Richtlinieneinstellungen an, wenn der Benutzer anmeldet. **Gpresult** die resultierende Menge der Richtlinieneinstellungen, die erzwungen wurden auf dem Computer für den angegebenen Benutzer angezeigt wird, wenn der Benutzer sind angemeldet.
- Da **/v** und **Neustartmodus anzugeben** erzeugen viele Informationen, ist es sinnvoll, die die Ausgabe in eine Textdatei umleiten (z. B. **Gpresult/Z > von policy.txt**).
- Die **Gpresult** Befehl ist in Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows 8, Windows 7 und Windows Vista verfügbar.
  ## <a name="examples"></a>Beispiele
  Das folgende Beispiel ruft die RSoP-Daten für den Remotebenutzer **Zielbenutzername** des Computers **Srvmain**, und zeigt Sie RSoP-Daten über den Benutzer nur. Der Befehl ausgeführt wird, mit den Anmeldeinformationen des Benutzers **Maindom\hiropln**, und <strong>p@ssW23</strong> wird für diesen Benutzer als Kennwort eingegeben.

  ```
  gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /user targetusername /scope user /r
  ```
  
Im folgenden Beispiel werden alle verfügbaren Informationen zur Gruppenrichtlinie für den Remotebenutzer **Zielbenutzername** des Computers **Srvmain** in eine Datei mit dem Namen **von policy.txt**. Keine Daten, die über den Computer enthalten ist. Der Befehl ausgeführt wird, mit den Anmeldeinformationen des Benutzers **Maindom\hiropln**, und <strong>p@ssW23</strong> wird für diesen Benutzer als Kennwort eingegeben.

  ```
  gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /user targetusername /z > policy.txt
  ```
  
Das folgende Beispiel zeigt die RSoP-Daten für den Computer **Srvmain** und dem angemeldeten Benutzer. Daten, die über den Benutzer und dem Computer enthalten ist. Der Befehl ausgeführt wird, mit den Anmeldeinformationen des Benutzers **Maindom\hiropln**, und <strong>p@ssW23</strong> wird für diesen Benutzer als Kennwort eingegeben.

  ```
  gpresult /s srvmain /u maindom\hiropln /p p@ssW23 /r
  ```
  
## <a name="additional-references"></a>Zusätzliche Referenzen
- [Gruppenrichtlinien-TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

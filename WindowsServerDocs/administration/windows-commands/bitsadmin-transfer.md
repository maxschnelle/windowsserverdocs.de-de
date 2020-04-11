---
title: bitadmin-Übertragung
description: Windows-Befehls Thema für die **bitionadmin-Übertragung**, bei der eine oder mehrere Dateien übertragen werden.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe302141-b33a-4a05-835e-dc4fc4db7d5a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9402f1b4907ffbe4a1085a04392349e1177092d7
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122673"
---
# <a name="bitsadmin-transfer"></a>bitadmin-Übertragung

Überträgt eine oder mehrere Dateien.

## <a name="syntax"></a>Syntax

```
bitsadmin /transfer <name> [<type>] [/priority <job_priority>] [/ACLflags <flags>] [/DYNAMIC] <remotefilename> <localfilename>
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| Name | Der Name des Auftrags. Dieser Befehl darf keine GUID sein. |
| Typ | Optional. Legt den Typ des Auftrags fest, einschließlich:<ul><li>**Downloaden.** Der Standardwert. Wählen Sie diesen Typ für Download Aufträge aus.</li><li>**Uploads.** Wählen Sie diesen Typ für hochgeladene Aufträge aus.</li></ul> |
| priority | Optional. Legt die Priorität des Auftrags fest, einschließlich:<ul><li>FOREGROUND (Vordergrund)</li><li>HIGH (Hoch)</li><li>NORMAL</li><li>LOW (Niedrig)</li></ul> |
| Aclflags | Optional. Gibt an, dass Sie den Besitzer und die ACL-Informationen mit der heruntergeladenen Datei verwalten möchten. Geben Sie einen oder mehrere der Werte an, einschließlich:<ul><li>**o** -Besitzer Informationen mit Datei kopieren.</li><li>**g** -Gruppeninformationen in Datei kopieren.</li><li>**d** : Kopieren Sie die DACL-Informationen ("-Zugriffs Steuerungs Liste") mit der Datei.</li><li>**s** -Informationen zur System Zugriffs Steuerungs Liste (SACL) mit Datei kopieren.</li></ul> |
| /DYNAMIC | Konfiguriert den Auftrag mithilfe von [**BITS_JOB_PROPERTY_DYNAMIC_CONTENT**](https://docs.microsoft.com/windows/win32/api/bits5_0/ne-bits5_0-bits_job_property_id), wodurch die serverseitigen Anforderungen entspannt werden. |
| remotefilename | Der Name der Datei, nachdem Sie an den Server übertragen wurde. |
| localfilename | Der Name der lokalen Datei. |

## <a name="remarks"></a>Hinweise

Standardmäßig erstellt der bitadmin-Dienst einen Download Auftrag, der mit **normaler** Priorität ausgeführt wird, und aktualisiert das Befehlsfenster mit Statusinformationen, bis die Übertragung abgeschlossen ist oder ein kritischer Fehler auftritt.

Der Dienst schließt den Auftrag ab, wenn er alle Dateien erfolgreich überträgt und den Auftrag abbricht, wenn ein kritischer Fehler auftritt. Der Dienst erstellt den Auftrag nicht, wenn dem Auftrag keine Dateien hinzugefügt werden können oder wenn Sie einen ungültigen Wert für *Typ* oder *job_priority*angeben. Geben Sie mehrere `<RemoteFileName>-<LocalFileName>` Paare an, um mehr als eine Datei zu übertragen. Die Paare müssen durch Leerzeichen getrennt werden.

> [!NOTE]
> Der bitionsadmin-Befehl wird weiterhin ausgeführt, wenn ein vorübergehender Fehler auftritt. Um den Befehl zu beenden, drücken Sie STRG + C.

## <a name="examples"></a>Beispiele

Im folgenden Beispiel wird ein Übertragungs Auftrag mit dem Namen *mydownloadjob*gestartet.

```
C:\>bitsadmin /transfer myDownloadJob http://prodserver/audio.wma c:\downloads\audio.wma
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
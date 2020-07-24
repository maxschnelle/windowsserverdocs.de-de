---
title: TCP-Verbindung wird während der Überprüfung für das Aushandeln abgebrochen
description: Erläutert, wie das SMB-Problem behoben wird, wenn die TCP-Verbindung während der Überprüfung der Aushandlung abgebrochen wird.
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 762ad3b20c389771a9c0e6783d2a6fb1e73b8f0d
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961002"
---
# <a name="tcp-connection-is-aborted-during-validate-negotiate"></a>TCP-Verbindung wird während der Überprüfung für das Aushandeln abgebrochen

In der Netzwerk Ablauf Verfolgung für das SMB-Problem bemerken Sie, dass während des Prozesses zum Überprüfen von Aushandlungen ein TCP-Zurücksetzungs Abbruch aufgetreten ist. In diesem Artikel wird beschrieben, wie Sie die Situation beheben.

## <a name="cause"></a>Ursache

Dieses Problem kann durch eine fehlgeschlagene Aushandlung der Aushandlung verursacht werden. Dies tritt normalerweise auf, weil ein WAN-Accelerator das ursprüngliche SMB-Aushandlungs Paket ändert.

Microsoft gestattet nicht mehr das Überprüfen von Aushandlungs Paketen aus irgendeinem Grund. Dies liegt daran, dass dieses Verhalten ein schwerwiegendes Sicherheitsrisiko darstellt.

Die folgenden Anforderungen gelten für das Paket zum Überprüfen von Aushandlungen:

- Der Prozess zum Überprüfen der Aushandlung verwendet den Befehl "Informationen überprüfen" der Befehlszeilen Überprüfung \_ \_ \_ .

- Die Antwort zum Überprüfen der Aushandlung muss signiert sein. Andernfalls wird die Verbindung abgebrochen.

- Sie sollten die FSCTL \_ Validate- \_ \_ Informationsmeldungen mit den Aushandlungs Nachrichten vergleichen, um sicherzustellen, dass nichts geändert wurde.

## <a name="workaround"></a>Problemumgehung

Sie können den Prozess zum Überprüfen der Aushandlung temporär deaktivieren. Suchen Sie hierzu den folgenden Registrierungs Unterschlüssel:

**HKEY \_ local \_ Machine \\ System \\ CurrentControlSet \\ Services \\ LanmanWorkstation- \\ Parameter**

Legen Sie unter dem **Parameter** Schlüssel den Wert "Requirements **securenegotiate** " auf **0**fest.

In Windows PowerShell können Sie den folgenden Befehl ausführen, um diesen Wert festzulegen:

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters" RequireSecureNegotiate -Value 0 -Force
```

> [!NOTE]
> Der Prozess zum Überprüfen der Aushandlung kann in Windows 10, Windows Server 2016 oder höheren Versionen von Windows nicht deaktiviert werden.

Wenn der Client oder der Server den Befehl "aushandeln überprüfen" nicht unterstützen kann, können Sie dieses Problem umgehen, indem Sie die SMB-Signierung als erforderlich festlegen. SMB-Signaturen gelten als sicherer als Überprüfungs Aushandlungen. Es kann jedoch auch zu Leistungseinbußen kommen, wenn eine Signierung erforderlich ist.

## <a name="reference"></a>Referenz

Weitere Informationen finden Sie in den folgenden Artikeln:

[3.3.5.15.12 Verarbeiten einer Anforderung zum Überprüfen von Aushandlungs Informationen](/openspecs/windows_protocols/ms-smb2/0b7803eb-d561-48a4-8654-327803f59ec6)

[3.2.5.14.12 behandeln einer Antwort zum Überprüfen von Aushandlungs Informationen](/openspecs/windows_protocols/ms-smb2/6a5bc90d-3c08-4498-905b-e7dab30b2e0e)

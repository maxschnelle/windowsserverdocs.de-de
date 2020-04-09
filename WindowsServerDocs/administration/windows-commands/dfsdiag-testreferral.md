---
title: Dfsdiag testreferral
description: Windows-Befehls Thema für Dfsdiag testreferral, das verteiltes Dateisystem (DFS)-Verweise prüft.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 877c60dc-e993-4bd5-87dd-e892e3f98a1a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5c0a75d557d816ac9e19a1e22b3273195b93f53
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846245"
---
# <a name="dfsdiag-testreferral"></a>Dfsdiag testreferral

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Prüft verteiltes Dateisystem (DFS)-Verweise durch Ausführen der folgenden Tests:

- Wenn Sie den dfspath-Parameter ohne Argumente verwenden, überprüft dieser Befehl, ob die Verweis Liste alle vertrauenswürdigen Domänen enthält.

- Wenn Sie eine Domäne angeben, führt der Befehl eine Integritäts Überprüfung von Domänen Controllern (Dfsdiag/testdcs) durch und testet die Site Zuordnungen und den Domänen Cache des lokalen Hosts.

- Wenn Sie eine Domäne und \Sysvol oder \netlogon angeben und die gleichen Integritätsprüfungen wie bei der Angabe einer Domäne durchführen, prüft der Befehl, ob die Gültigkeitsdauer (\ttl) der SYSVOL-oder Netlogon-Verweise mit dem Standardwert von 900 Sekunden übereinstimmt.

- Wenn Sie einen Namespace Stamm angeben und die gleichen Integritäts Überprüfungen wie bei der Angabe einer Domäne durchführen, führt der Befehl eine DFS-Konfigurations Überprüfung (Dfsdiag/TestDFSConfig) und eine Namespace Integritätsprüfung (Dfsdiag/TestDFSIntegrity) aus.

- Wenn Sie einen DFS-Ordner (Link) angeben und die gleichen Integritätsprüfungen wie bei der Angabe eines Namespace Stamms durchführen, überprüft der Befehl die Standort Konfiguration für Ordner Ziele (Dfsdiag/Testsites) und überprüft die Standort Zuordnung des lokalen Hosts.

## <a name="syntax"></a>Syntax

```
dfsdiag /TestReferral /DFSpath:<DFS path for getting referrals> [/Full]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
| /DFSpath:<path for getting referrals>|Dieser DFS-Pfad kann eine der folgenden sein:<p>-   \(leeres\): testet vertrauenswürdige Domänen.<br />-   \\\\Domäne: Domänen Controller Verweise.<br />-   \\\\Domänen\\SYSVOL: SYSVOL-Verweise.<br />-   \\\\Doma in\\Netlogon: Netlogon-Referenzen.<br />-   \\\\<Domain or server>\\<Namespace Root>: Namespace-Stamm Verweise.<br />-   \\\\<Domain or server>\\<Namespace root>\\<DFS folder>: DFS-Ordner \(Verknüpfungen\) verweisen.|
|/Full|Wird nur auf Domänen-und Stamm Verweise angewendet. überprüft die Konsistenz der Standort Zuordnungs Informationen zwischen der Registrierung und den Active Directory-Domänen Diensten \(AD DS\).|

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

```
dfsdiag /TestReferral /DFSpath:\\Contoso.com\MyNamespace
```

```
dfsdiag /TestReferral /DFSpath:
```

## <a name="additional-references"></a>Weitere Verweise

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)



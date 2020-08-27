---
ms.assetid: fd3bc84a-48eb-4f00-9dc2-846bf2c2668b
title: Problembehandlung für AD DS
description: Übersicht über den Abschnitt zur Problembehandlung für AD DS
ms.author: iainfou
author: iainfoulds
manager: dcscontentpm
ms.date: 11/22/2019
ms.topic: article
ms.openlocfilehash: 485b78bcefbdf7d399f5bae041c653f300bc817a
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88939960"
---
# <a name="ad-ds-troubleshooting"></a>Problembehandlung für AD DS

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

Dieser Abschnitt enthält Empfehlungen zur Problembehandlung und Verfahren für die Diagnose und Behebung von Problemen, die bei der Active Directory Replikation auftreten können. Der Schwerpunkt liegt auf der Reaktion auf Verzeichnisdienst-Ereignisprotokoll Einträge und der Interpretation von Nachrichten, die von Tools wie Repadmin.exe und Dcdiag.exe gemeldet werden.

Repadmin.exe und Dcdiag.exe sind auf allen Domänen Controllern verfügbar, auf denen Windows Server 2012 R2 oder höhere Versionen ausgeführt werden. Weitere Informationen zur Verwendung dieser Tools zur Problembehandlung finden Sie in den folgenden Artikeln.

- [Konfigurieren eines Computers für die Problembehandlung Active Directory](../manage/troubleshoot/Configuring-a-Computer-for-Troubleshooting.md)
- [Behandeln von Active Directory-Replikationsproblemen](../manage/troubleshoot/Troubleshooting-Active-Directory-Replication-Problems.md)

Eine weitere nützliche Technologie ist die Ereignis Ablauf Verfolgung für Windows (ETW). Sie können etw zur Problembehandlung der LDAP-Kommunikation zwischen den Domänen Controllern verwenden. Weitere Informationen finden Sie unter [Verwenden von etw zur Problembehandlung bei LDAP-Verbindungen](../manage/troubleshoot/troubleshoot-ldap-using-etw.md).

Sie können auch Remoteserver-Verwaltungstools (RSAT) auf einem Mitglieds Server installieren, auf dem Windows 10 ausgeführt wird. Weitere Informationen zum Installieren von RSAT finden Sie unter [Remoteserver-Verwaltungstools](../../../remote/remote-server-administration-tools.md).

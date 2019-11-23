---
title: Netzwerkrichtlinien
description: Dieses Thema bietet einen Überblick über die Netzwerk Richtlinien für den Netzwerk Richtlinien Server unter Windows Server 2016 und enthält Links zu weiteren Anleitungen zu NPS.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: e4a9b134-6d1d-40d7-a49c-5f46d5fdb419
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c241191f54080ed92a1f1a274c0b2aff0b8c564c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405349"
---
# <a name="network-policies"></a>Netzwerkrichtlinien

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema finden Sie einen Überblick über die Netzwerk Richtlinien in NPS.

>[!NOTE]
>Zusätzlich zu diesem Thema ist die folgende Dokumentation zur Netzwerk Richtlinie verfügbar.
> - [Zugriffsberechtigung](nps-np-access.md)
> - [Konfigurieren von Netzwerkrichtlinien](nps-np-configure.md)

Netzwerk Richtlinien sind Sätze von Bedingungen, Einschränkungen und Einstellungen, mit denen Sie festlegen können, wer zum Herstellen einer Verbindung mit dem Netzwerk autorisiert ist, sowie die Umstände, unter denen eine Verbindung hergestellt werden kann.

Beim Verarbeiten von Verbindungsanforderungen als Remote Authentication Dial-in User Service Server (RADIUS) führt NPS sowohl die Authentifizierung als auch die Autorisierung für die Verbindungsanforderung aus. Während des Authentifizierungs Vorgangs überprüft NPS die Identität des Benutzers oder Computers, der eine Verbindung mit dem Netzwerk herstellt. Während des Autorisierungs Vorgangs bestimmt NPS, ob der Benutzer oder der Computer auf das Netzwerk zugreifen darf.

Um diese Determinationen vorzunehmen, verwendet NPS Netzwerk Richtlinien, die in der NPS-Konsole konfiguriert sind. NPS überprüft auch die DFÜ-Eigenschaften des Benutzerkontos in Active Directory&reg; Domänen Diensten \(AD DS\), um die Autorisierung auszuführen.

## <a name="network-policies---an-ordered-set-of-rules"></a>Netzwerk Richtlinien: eine geordnete Gruppe von Regeln

Netzwerk Richtlinien können als Regeln angezeigt werden. Jede Regel verfügt über eine Reihe von Bedingungen und Einstellungen. NPS vergleicht die Bedingungen der Regel mit den Eigenschaften von Verbindungsanforderungen. Wenn eine Entsprechung zwischen der Regel und der Verbindungsanforderung auftritt, werden die in der Regel definierten Einstellungen auf die Verbindung angewendet.

Wenn mehrere Netzwerk Richtlinien in NPS konfiguriert sind, handelt es sich um einen geordneten Satz von Regeln. NPS überprüft jede Verbindungsanforderung anhand der ersten Regel in der Liste, dann der zweiten usw., bis eine Entsprechung gefunden wird.

Jede Netzwerk Richtlinie verfügt über eine **Richtlinien Zustands** Einstellung, die es Ihnen ermöglicht, die Richtlinie zu aktivieren oder zu deaktivieren. Wenn Sie eine Netzwerk Richtlinie deaktivieren, wertet NPS die Richtlinie nicht aus, wenn Verbindungsanforderungen autorisiert werden.

>[!NOTE]
>Wenn Sie möchten, dass NPS eine Netzwerk Richtlinie auswerten, wenn Sie eine Autorisierung für Verbindungsanforderungen durchführen, müssen Sie die Einstellung **Richtlinien Status** konfigurieren, indem Sie das Kontrollkästchen aktivierte Richtlinie aktivieren.

## <a name="network-policy-properties"></a>Netzwerk Richtlinien Eigenschaften

Es gibt vier Kategorien von Eigenschaften für jede Netzwerk Richtlinie:

### <a name="overview"></a>Übersicht

 Mithilfe dieser Eigenschaften können Sie angeben, ob die Richtlinie aktiviert ist, ob die Richtlinie den Zugriff gewährt oder verweigert und ob eine bestimmte Netzwerk Verbindungsmethode oder der Typ des Netzwerk Zugriffs Servers (NAS) für Verbindungsanforderungen erforderlich ist. Mit den Übersichts Eigenschaften können Sie auch angeben, ob die Einwähleigenschaften von Benutzerkonten in AD DS ignoriert werden. Wenn Sie diese Option auswählen, werden nur die Einstellungen in der Netzwerk Richtlinie von NPS verwendet, um zu bestimmen, ob die Verbindung autorisiert ist.


### <a name="conditions"></a>Bedingungen

 Mithilfe dieser Eigenschaften können Sie die Bedingungen angeben, die die Verbindungsanforderung aufweisen muss, damit Sie der Netzwerk Richtlinie entspricht. Wenn die in der Richtlinie konfigurierten Bedingungen der Verbindungsanforderung entsprechen, wendet NPS die in der Netzwerk Richtlinie festgelegten Einstellungen auf die Verbindung an. Wenn Sie z. b. die NAS-IPv4-Adresse als Bedingung der Netzwerk Richtlinie angeben und NPS eine Verbindungsanforderung von einem NAS-Gerät erhält, das über die angegebene IP-Adresse verfügt, entspricht die Bedingung in der Richtlinie der Verbindungsanforderung. 


### <a name="constraints"></a>Einschränkungen

 Einschränkungen sind zusätzliche Parameter der Netzwerk Richtlinie, die für die Anpassung der Verbindungsanforderung erforderlich sind. Wenn eine Einschränkung nicht mit der Verbindungsanforderung übereinstimmt, lehnt NPS die Anforderung automatisch ab. Anders als bei der NPS-Antwort auf nicht übereinstimmende Bedingungen in der Netzwerk Richtlinie, wenn eine Einschränkung nicht übereinstimmt, verweigert NPS die Verbindungsanforderung, ohne zusätzliche Netzwerk Richtlinien zu bewerten.

### <a name="settings"></a>Einstellungen

 Mithilfe dieser Eigenschaften können Sie die Einstellungen angeben, die NPS für die Verbindungsanforderung anwendet, wenn alle Netzwerk Richtlinien Bedingungen für die Richtlinie übereinstimmen.

Wenn Sie mit der NPS-Konsole eine neue Netzwerk Richtlinie hinzufügen, müssen Sie den Assistenten für neue Netzwerk Richtlinien verwenden. Nachdem Sie mithilfe des Assistenten eine Netzwerk Richtlinie erstellt haben, können Sie die Richtlinie anpassen, indem Sie in der NPS-Konsole auf die Richtlinie doppelklicken, um die Richtlinien Eigenschaften zu erhalten.

Beispiele für Muster Vergleichs Syntax zum Angeben von Netzwerk Richtlinien Attributen finden Sie unter [Verwenden regulärer Ausdrücke in NPS](nps-crp-reg-expressions.md).

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).

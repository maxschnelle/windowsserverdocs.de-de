---
title: Richtlinien für Netzwerke
description: Dieses Thema enthält eine Übersicht über Netzwerkrichtlinien für Netzwerkrichtlinienserver in Windows Server2016 und enthält Links zu weiteren Anleitungen zum NPS.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: e4a9b134-6d1d-40d7-a49c-5f46d5fdb419
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7e1604f4839bd955e5ea10d9eafea5ef0c978977
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="network-policies"></a>Richtlinien für Netzwerke

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können eine Übersicht über die Netzwerkrichtlinien auf dem Netzwerkrichtlinienserver.

>[!NOTE]
>Zusätzlich zu diesem Thema ist die folgenden Netzwerk-Richtlinie-Dokumentation verfügbar.
> - [Zugriffsberechtigung](nps-np-access.md)
> - [Konfigurieren von Netzwerkrichtlinien](nps-np-configure.md)

Netzwerkrichtlinien sind Bedingungen, Einschränkungen und Einstellungen, mit denen Sie festlegen, wer berechtigt ist, eine Verbindung mit dem Netzwerk und die Umstände, unter denen sie können oder keine Verbindung herstellen.

Bei der Verarbeitung von Verbindungsanforderungen als Server Remote Authentication Dial-in User Service (RADIUS) führt NPS die Authentifizierung und Autorisierung für die Verbindungsanforderung. Während des Authentifizierungsprozesses überprüft NPS die Identität des Benutzers oder der Computer, der mit dem Netzwerk verbunden ist. Während des Autorisierungsprozesses bestimmt NPS, ob der Benutzer oder Computer zulässig ist, auf das Netzwerk zugreifen.

Um diese Bestimmung zu machen, verwendet NPS Netzwerkrichtlinien, die in der NPS-Konsole konfiguriert sind. NPS überprüft auch die DFÜ-Eigenschaften des Benutzerkontos in Active Directory&reg; Domänendienste \(AD DS\) für die Autorisierung.

## <a name="network-policies---an-ordered-set-of-rules"></a>Netzwerkrichtlinien - einen geordneten Satz von Regeln

Netzwerkrichtlinien können als Regeln angezeigt werden. Jede Regel verfügt über eine Reihe von Einstellungen und Bedingungen. NPS vergleicht die Bedingungen für die Regel für die Eigenschaften der Verbindungsanforderungen. Wenn eine Übereinstimmung zwischen der Regel und die Verbindungsanforderung auftritt, werden die Einstellungen in der Regel definierten auf die Verbindung angewendet.

Wenn mehrere Netzwerkrichtlinien auf dem Netzwerkrichtlinienserver konfiguriert sind, sind sie einen geordneten Satz von Regeln. NPS überprüft jede Verbindungsanfrage vor der ersten Regel in der Liste aus, und klicken Sie dann die zweite usw., bis eine Übereinstimmung gefunden wird.

Jede Netzwerkrichtlinie weist eine **Richtlinienstatus** festlegen, können Sie zum Aktivieren oder deaktivieren die Richtlinie. Wenn Sie eine Netzwerkrichtlinie deaktivieren, wertet NPS nicht die Richtlinie, wenn Verbindungsanforderungen zu autorisieren.

>[!NOTE]
>Wenn Sie NPS eine Netzwerkrichtlinie ausgewertet, bei der Autorisierung für Verbindungsanforderungen durchführen möchten, müssen Sie konfigurieren die **Richtlinienstatus** Einstellung durch Auswahl der Richtlinie das Kontrollkästchen aktiviert.

## <a name="network-policy-properties"></a>Die Eigenschaften von

Es gibt vier Kategorien von Eigenschaften für jede Netzwerkrichtlinie:

### <a name="overview"></a>(Übersicht)

 Diese Eigenschaften können Sie angeben, ob die Richtlinie aktiviert ist, gibt an, ob die Richtlinie Zugriff gewährt oder verweigert, und gibt an, ob eine bestimmte Netzwerkverbindungsmethode oder der Typ des Netzwerkzugriffsservers (NAS), für Verbindungsanforderungen erforderlich ist. Übersicht die Übersichtseigenschaften können Sie angeben, ob die DFÜ-Eigenschaften von Benutzerkonten in AD DS ignoriert werden. Wenn Sie diese Option auswählen, werden nur die Einstellungen in der Netzwerkrichtlinie von NPS verwendet, um festzustellen, ob die Verbindung autorisiert ist.


### <a name="conditions"></a>Bedingungen

 Diese Eigenschaften können Sie die Bedingungen angegeben, die die Verbindungsanforderung verfügen muss, um die Netzwerkrichtlinie übereinstimmen. Wenn die Bedingungen, die in der Richtlinie konfiguriert die Verbindungsanforderung übereinstimmen, gilt NPS die Einstellungen in der Netzwerkrichtlinie für die Verbindung festgelegt. Wenn Sie die NAS-IPv4-Adresse als Bedingung für die Netzwerkrichtlinie angeben und NPS empfängt eine Verbindung von einem NAS, die die angegebene IP-Adresse verfügt, entspricht die Bedingung in der Richtlinie die Verbindungsanforderung. 


### <a name="constraints"></a>Einschränkungen

 Einschränkungen sind zusätzliche Parameter der Netzwerkrichtlinie, die erforderlich sind, um die Verbindungsanforderung entsprechen. Wenn eine Einschränkung durch Anforderung der Verbindung keine Übereinstimmung vorliegt, lehnt NPS automatisch die Anforderung ab. Im Gegensatz zu der NPS-Antwort an nicht übereinstimmende Bedingungen in der Netzwerkrichtlinie verweigert NPS, wenn eine Einschränkung nicht übereinstimmt wird, die Verbindungsanforderung ohne zusätzliche Netzwerkrichtlinien auszuwerten.

### <a name="settings"></a>Einstellungen

 Diese Eigenschaften können Sie die Einstellungen angeben, die NPS für die Verbindungsanforderung gilt, wenn alle der Netzwerk-richtlinienbedingungen für die Richtlinie zugeordnet werden.

Wenn Sie eine neue Netzwerkrichtlinie mit der NPS-Konsole hinzufügen, müssen Sie den Assistenten für neue Netzwerkrichtlinien verwenden. Nachdem Sie eine Netzwerkrichtlinie mithilfe des Assistenten erstellt haben, können Sie die Richtlinie anpassen, durch Doppelklicken auf die Richtlinie in der NPS-Konsole, um die Eigenschaften der Richtlinie zu erhalten.

Beispiele für mustervergleichssyntax an Attribute Netzwerk, finden Sie unter [reguläre Ausdrücke in NPS](nps-crp-reg-expressions.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).

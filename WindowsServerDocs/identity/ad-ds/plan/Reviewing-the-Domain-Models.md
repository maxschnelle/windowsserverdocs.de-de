---
ms.assetid: e727a33d-133b-43c9-b6a4-7c00f9cb6000
title: Überprüfen der Domänen Modelle
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.openlocfilehash: 326c9f5727fa529fc131fe7bac6589a30c54c30a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87972257"
---
# <a name="reviewing-the-domain-models"></a>Überprüfen der Domänen Modelle

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die folgenden Faktoren haben Auswirkungen auf das von Ihnen ausgewählte Domänen Entwurfs Modell:

- Menge an verfügbarer Kapazität in Ihrem Netzwerk, die Sie Active Directory Domain Services (AD DS) zuordnen möchten. Ziel ist es, ein Modell auszuwählen, das eine effiziente Replikation von Informationen mit minimalen Auswirkungen auf die verfügbare Netzwerkbandbreite ermöglicht.

- Anzahl der Benutzer in Ihrer Organisation. Wenn Ihre Organisation eine große Anzahl von Benutzern umfasst, können Sie mit der Bereitstellung von mehr als einer Domäne Ihre Daten partitionieren und Ihnen mehr Kontrolle über die Menge an Replikations Datenverkehr geben, der über eine bestimmte Netzwerkverbindung geleitet wird. Dadurch können Sie steuern, wo Daten repliziert werden, und die Last verringern, die durch Replikations Datenverkehr bei langsamen Verbindungen in Ihrem Netzwerk erzeugt wird.

Der einfachste Domänen Entwurf ist eine einzelne Domäne. Bei einem einzelnen Domänen Entwurf werden alle Informationen auf allen Domänen Controllern repliziert. Bei Bedarf können Sie jedoch zusätzliche regionale Domänen bereitstellen. Dies kann vorkommen, wenn Teile der Netzwerkinfrastruktur durch langsame Verbindungen verbunden sind und der Gesamtstruktur Besitzer sicherstellen möchte, dass der Replikations Datenverkehr nicht die Kapazität überschreitet, die AD DS zugeordnet wurde.

Es empfiehlt sich, die Anzahl der Domänen zu minimieren, die Sie in Ihrer Gesamtstruktur bereitstellen. Dadurch wird die Gesamtkomplexität der Bereitstellung verringert, und infolgedessen werden die Gesamtbetriebskosten reduziert. In der folgenden Tabelle sind die Verwaltungskosten für das Hinzufügen regionaler Domänen aufgeführt.

| Kosten     | Auswirkungen     |
| -------- | ---------------- |
| Verwaltung mehrerer Dienst Administrator Gruppen|Jede Domäne verfügt über eigene Dienst Administrator Gruppen, die unabhängig verwaltet werden müssen. Die Mitgliedschaft dieser Dienst Administrator Gruppen muss sorgfältig gesteuert werden.|
| Beibehalten der Konsistenz zwischen Gruppenrichtlinie Einstellungen, die mehreren Domänen gemeinsam sind | Gruppenrichtlinie Einstellungen, die Gesamtstruktur weit angewendet werden müssen, müssen separat auf jede einzelne Domäne in der Gesamtstruktur angewendet werden. |
| Beibehalten der Konsistenz zwischen Zugriffs Steuerung und Überwachungs Einstellungen, die mehreren Domänen gemeinsam sind | Zugriffs Steuerungs-und Überwachungs Einstellungen, die über die Gesamtstruktur angewendet werden müssen, müssen separat auf jede einzelne Domäne in der Gesamtstruktur angewendet werden. |
| Erhöhung der Wahrscheinlichkeit, dass Objekte zwischen Domänen verschoben werden | Umso größer die Anzahl der Domänen ist, desto größer ist die Wahrscheinlichkeit, dass Benutzer von einer Domäne in eine andere verschieben müssen. Diese Verschiebung kann sich möglicherweise auf Endbenutzer auswirken. |

> [!NOTE]
> Die differenzierten Windows Server-Kennwort-und Konto Sperrungs Richtlinien können sich auch auf das von Ihnen ausgewählte Domänen Entwurfs Modell auswirken. Vor dieser Version von Windows Server 2008 konnten Sie für alle Benutzer in der Domäne nur ein Kennwort und eine Konto Sperrungs Richtlinie, die in der Domänen-Standard Domänen Richtlinie angegeben ist, anwenden. Wenn Sie unterschiedliche Kennwort-und Konto Sperrungs Einstellungen für verschiedene Gruppen von Benutzern wünschen, müssen Sie daher entweder einen Kenn Wortfilter erstellen oder mehrere Domänen bereitstellen. Sie können jetzt differenzierte Kenn Wort Richtlinien verwenden, um mehrere Kenn Wort Richtlinien anzugeben und verschiedene Kenn Wort Einschränkungen und Konto Sperr Richtlinien auf verschiedene Gruppen von Benutzern in einer einzelnen Domäne anzuwenden. Weitere Informationen zu differenzierten Kennwort-und Konto Sperrungs Richtlinien finden Sie im Artikel AD DS differenziertere [Kennwort-und Konto Sperrungs Richtlinie schrittweise Anleitung](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc770842(v=ws.10)).

## <a name="single-domain-model"></a>Einzelnes Domänen Modell

Ein einzelnes Domänen Modell ist am einfachsten zu verwalten und die kostengünstigste Wartung. Er besteht aus einer Gesamtstruktur, die eine einzelne Domäne enthält. Diese Domäne ist die Stamm Domäne der Gesamtstruktur und enthält alle Benutzer-und Gruppenkonten in der Gesamtstruktur.

Ein einzelnes Domänen Gesamtstruktur Modell reduziert die administrative Komplexität, indem es die folgenden Vorteile bietet:

- Jeder beliebige Domänen Controller kann jeden Benutzer in der Gesamtstruktur authentifizieren.

- Alle Domänen Controller können globale Kataloge sein, sodass Sie die Platzierung des globalen Katalog Servers nicht planen müssen.

In einer einzelnen Domänen Gesamtstruktur werden alle Verzeichnis Daten an alle geografischen Standorte repliziert, auf denen Domänen Controller gehostet werden. Obwohl dieses Modell am einfachsten zu verwalten ist, erstellt es auch den meisten Replikations Datenverkehr der beiden Domänen Modelle. Durch die Partitionierung des Verzeichnisses in mehrere Domänen wird die Replikation von Objekten auf bestimmte geografische Regionen beschränkt, was jedoch zu mehr Verwaltungsaufwand führt.

## <a name="regional-domain-model"></a>Regionales Domänen Modell

Alle Objektdaten innerhalb einer Domäne werden auf alle Domänen Controller in dieser Domäne repliziert. Wenn in Ihrer Gesamtstruktur eine große Anzahl von Benutzern enthalten ist, die über verschiedene geografische Standorte verteilt sind, die über ein WAN (Wide Area Network) verbunden sind, müssen Sie daher möglicherweise regionale Domänen bereitstellen, um den Replikations Datenverkehr über die WAN-Verbindungen zu verringern. Geografisch basierende regionale Domänen können gemäß der Netzwerk-WAN-Konnektivität organisiert werden.

Das regionale Domänen Modell ermöglicht es Ihnen, im Laufe der Zeit eine stabile Umgebung zu verwalten. Basieren Sie auf den Regionen, die zum Definieren von Domänen in Ihrem Modell für stabile Elemente verwendet werden, wie z. b. die Domänen, die auf anderen Faktoren basieren, z. b. Gruppen innerhalb des Unternehmens, können sich häufig ändern und eine Umstrukturierung ihrer Umgebung erforderlich machen.

Das regionale Domänen Modell besteht aus einer Gesamtstruktur-Stamm Domäne und einer oder mehreren regionalen Domänen. Zum Erstellen eines Modells für das regionale Domänen Modell müssen Sie identifizieren, welche Domäne die Stamm Domäne der Gesamtstruktur ist, und die Anzahl der zusätzlichen Domänen ermitteln, die zum erfüllen der Replikations Anforderungen Wenn Ihre Organisation Gruppen einschließt, die eine Daten Isolation oder eine Dienst Isolation von anderen Gruppen in der Organisation erfordern, erstellen Sie eine separate Gesamtstruktur für diese Gruppen. Domänen stellen keine Daten Isolation oder Dienst Isolation bereit.

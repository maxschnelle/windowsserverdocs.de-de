---
ms.assetid: ef4ef4a9-8969-4ad0-bd17-b2bb24f36ef6
title: Auswählen der Stammdomäne der Gesamtstruktur
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 80d39a5910d06559b98211eaf55a4cd0c82442a1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402508"
---
# <a name="selecting-the-forest-root-domain"></a>Auswählen der Stammdomäne der Gesamtstruktur

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die erste Domäne, die Sie in einer Active Directory Gesamtstruktur bereitstellen, wird als Gesamtstruktur-Stamm Domäne bezeichnet. Diese Domäne bleibt für den Lebenszyklus der AD DS Bereitstellung die Gesamtstruktur-Stamm Domäne.  
  
Die Stamm Domäne der Gesamtstruktur enthält die Gruppen Organisations-Admins und Schema-Admins. Diese Dienst Administrator Gruppen werden zum Verwalten von Vorgängen auf Gesamtstruktur Ebene verwendet, z. b. das Hinzufügen und Entfernen von Domänen und die Implementierung von Änderungen am Schema.  
  
Wenn Sie die Gesamtstruktur-Stamm Domäne auswählen, müssen Sie bestimmen, ob eine der Active Directory Domänen im Domänen Entwurf als Gesamtstruktur-Stamm Domäne fungieren kann oder ob Sie eine dedizierte Gesamtstruktur-Stamm Domäne bereitstellen müssen.  
  
Weitere Informationen zum Bereitstellen einer Gesamtstruktur-Stamm Domäne finden Sie unter Bereitstellen [einer Windows Server 2008](https://technet.microsoft.com/library/cc731174.aspx)-Gesamtstruktur-Stamm Domäne.  
  
## <a name="choosing-a-regional-or-dedicated-forest-root-domain"></a>Auswählen einer regionalen oder dedizierten Gesamtstruktur-Stamm Domäne

Wenn Sie ein einzelnes Domänen Modell anwenden, fungiert die einzelne Domäne als Stamm Domäne der Gesamtstruktur. Wenn Sie ein Modell mit mehreren Domänen anwenden, können Sie eine dedizierte Gesamtstruktur-Stamm Domäne bereitstellen oder eine regionale Domäne auswählen, die als Gesamtstruktur-Stamm Domäne fungieren soll.  
  
### <a name="dedicated-forest-root-domain"></a>Dedizierte Gesamtstruktur-Stamm Domäne

Eine dedizierte Gesamtstruktur-Stamm Domäne ist eine Domäne, die speziell für die Funktion als Gesamtstruktur Stamm erstellt wird. Sie enthält keine anderen Benutzerkonten als die Dienst Administrator Konten für die Stamm Domäne der Gesamtstruktur. Außerdem repräsentiert Sie keine geografische Region in ihrer Domänen Struktur. Alle anderen Domänen in der Gesamtstruktur sind untergeordnete Elemente der dedizierten Gesamtstruktur-Stamm Domäne.  

Die Verwendung eines dedizierten Gesamtstruktur Stamms bietet die folgenden Vorteile:  

- Betriebsbedingte Trennung von Gesamtstruktur-Dienst Administratoren von Domänen Dienst Administratoren. In einer Umgebung mit einer einzelnen Domäne können Mitglieder der Gruppe "Domänen-Admins" und "Integrierte Administratoren" Standard Tools und-Prozeduren verwenden, um Mitglieder der Gruppen "Organisations-Admins" und "Schema-Admins" zu machen In einer Gesamtstruktur, in der eine dedizierte Gesamtstruktur-Stamm Domäne verwendet wird, können Mitglieder der Domänen-Admins und integrierten Administratoren Gruppen in den regionalen Domänen keine Mitglieder der Dienst Administrator Gruppen auf Gesamtstruktur Ebene mithilfe von Standard Tools und-Prozeduren erstellen.  
- Schutz vor betrieblichen Änderungen in anderen Domänen. Eine dedizierte Gesamtstruktur-Stamm Domäne stellt keine bestimmte geografische Region in der Domänen Struktur dar. Aus diesem Grund wird dies von Reorganisationen oder anderen Änderungen, die zum Umbenennen oder Umstrukturieren von Domänen führen, nicht beeinträchtigt.  
- Dient als neutraler Stamm, sodass kein Land oder keine Region einer anderen Region untergeordnet ist. Einige Organisationen bevorzugen möglicherweise die Darstellung, dass ein Land oder eine Region einem anderen Land oder einer Region im Namespace untergeordnet ist. Wenn Sie eine dedizierte Gesamtstruktur-Stamm Domäne verwenden, können alle regionalen Domänen Peers in der Domänen Hierarchie sein.  

In einer Umgebung mit mehreren regionalen Domänen, in der ein dedizierter Gesamtstruktur Stamm verwendet wird, wirkt sich die Replikation der Gesamtstruktur-Stamm Domäne nur minimal auf die Netzwerkinfrastruktur aus. Der Grund hierfür ist, dass der Gesamtstruktur Stamm nur die Dienst Administrator Konten hostet. Die Mehrzahl der Benutzerkonten in der Gesamtstruktur und andere domänenspezifische Daten werden in den regionalen Domänen gespeichert.  
  
Ein Nachteil bei der Verwendung einer dedizierten Gesamtstruktur-Stamm Domäne ist, dass ein zusätzlicher Verwaltungsaufwand für die Unterstützung der zusätzlichen Domäne entsteht.  
  
### <a name="regional-domain-as-a-forest-root-domain"></a>Regionale Domäne als Gesamtstruktur-Stamm Domäne

Wenn Sie keine dedizierte Gesamtstruktur-Stamm Domäne bereitstellen möchten, müssen Sie eine regionale Domäne auswählen, die als Gesamtstruktur-Stamm Domäne fungieren soll. Diese Domäne ist die übergeordnete Domäne aller anderen regionalen Domänen und stellt die erste Domäne dar, die Sie bereitstellen. Die Stamm Domäne der Gesamtstruktur enthält Benutzerkonten und wird auf die gleiche Weise wie die anderen regionalen Domänen verwaltet. Der Hauptunterschied besteht darin, dass es auch die Gruppen Organisations-Admins und Schema-Admins umfasst.  
  
Der Vorteil der Auswahl einer regionalen Domäne, die als Gesamtstruktur-Stamm Domäne fungiert, besteht darin, dass der zusätzliche Verwaltungsaufwand, der durch die Verwaltung einer zusätzlichen Domäne entsteht, nicht entsteht. Wählen Sie eine geeignete regionale Domäne als Gesamtstruktur Stamm aus, z. b. die Domäne, die ihren Hauptsitz darstellt, oder die Region, die über die schnellsten Netzwerkverbindungen verfügt. Wenn es für Ihre Organisation schwierig ist, eine regionale Domäne als Stamm Domäne der Gesamtstruktur auszuwählen, können Sie stattdessen ein dediziertes Gesamtstruktur-Stamm Modell verwenden.  
  
## <a name="assigning-the-forest-root-domain-name"></a>Zuweisen des Gesamtstruktur-Stamm Domänen Namens

Der Gesamtstruktur-Stamm Domänen Name ist auch der Name der Gesamtstruktur. Der Name der Gesamtstruktur Stamms ist ein Domain Name System (DNS), der aus einem Präfix und einem Suffix in der Form "prefix. Suffix" besteht. Beispielsweise könnte eine Organisation den Namen der Gesamtstruktur Corp.contoso.com. In diesem Beispiel ist Corp das Präfix, und contoso.com ist das Suffix.  
  
Wählen Sie das Suffix aus einer Liste vorhandener Namen in Ihrem Netzwerk aus. Wählen Sie für das Präfix einen neuen Namen aus, der zuvor noch nicht in Ihrem Netzwerk verwendet wurde. Wenn Sie ein neues Präfix an ein vorhandenes Suffix anfügen, erstellen Sie einen eindeutigen Namespace. Durch das Erstellen eines neuen Namespace für Active Directory Domain Services (AD DS) wird sichergestellt, dass jede vorhandene DNS-Infrastruktur nicht geändert werden muss, um AD DS zu unterstützen.  
  
### <a name="selecting-a-suffix"></a>Auswählen eines Suffixes

So wählen Sie ein Suffix für die Stamm Domäne der Gesamtstruktur aus:  
  
1. Wenden Sie sich an den DNS-Besitzer der Organisation, um eine Liste der registrierten DNS-Suffixe zu erhalten, die im Netzwerk verwendet werden, das AD DS hostet. Beachten Sie, dass sich die Suffixe, die im internen Netzwerk verwendet werden, möglicherweise von den externen Suffixen unterscheiden. Beispielsweise kann eine Organisation contosopharma.com im Internet und contoso.com im internen Unternehmensnetzwerk verwenden.  
  
2. Wenden Sie sich an den DNS-Besitzer, um ein Suffix für die Verwendung mit AD DS auszuwählen. Wenn keine passenden Suffixe vorhanden sind, registrieren Sie einen neuen Namen mit einer Internet Naming Authority.  
  
Es wird empfohlen, DNS-Namen zu verwenden, die im Active Directory-Namespace mit einer Internet Autorität registriert sind. Es ist garantiert, dass nur registrierte Namen global eindeutig sind. Wenn eine andere Organisation später denselben DNS-Domänen Namen registriert (oder wenn Ihre Organisation mit einem anderen Unternehmen zusammenarbeitet, das denselben DNS-Namen verwendet), können die beiden Infrastrukturen nicht miteinander interagieren.  
  
> [!CAUTION]  
> Verwenden Sie keine DNS-Namen mit einer einzelnen Bezeichnung. Weitere Informationen finden Sie unter Informationen zum Konfigurieren von Windows für Domänen mit DNS-Namen mit einer einzelnen Bezeichnung ([https://go.microsoft.com/fwlink/?LinkId=106631](https://go.microsoft.com/fwlink/?LinkId=106631)). Außerdem wird die Verwendung von nicht registrierten Suffixen, wie z. b. local, nicht empfohlen.  
  
### <a name="selecting-a-prefix"></a>Auswählen eines Präfixes

Wenn Sie ein registriertes Suffix ausgewählt haben, das bereits im Netzwerk verwendet wird, wählen Sie ein Präfix für den Namen der Gesamtstruktur-Stamm Domäne aus, indem Sie die Präfix Regeln in der folgenden Tabelle verwenden. Fügen Sie ein Präfix hinzu, das zurzeit nicht verwendet wird, um einen neuen untergeordneten Namen zu erstellen. Wenn Ihr DNS-Stammname beispielsweise contoso.com lautet, können Sie den Namen der Stamm Domäne der Active Directory Gesamtstruktur erstellen concorp.contoso.com wenn der Namespace concorp.contoso.com nicht bereits im Netzwerk verwendet wird. Diese neue Verzweigung des-Namespace wird für AD DS dediziert und kann problemlos mit der vorhandenen DNS-Implementierung integriert werden.  
  
Wenn Sie eine regionale Domäne ausgewählt haben, die als Gesamtstruktur-Stamm Domäne fungieren soll, müssen Sie möglicherweise ein neues Präfix für die Domäne auswählen. Da der Gesamtstruktur-Stamm Domänen Name alle anderen Domänen Namen in der Gesamtstruktur betrifft, ist ein Regional basierter Name möglicherweise nicht geeignet. Wenn Sie ein neues Suffix verwenden, das zurzeit nicht im Netzwerk verwendet wird, können Sie es als Gesamtstruktur-Stamm Domänen Namen verwenden, ohne ein zusätzliches Präfix auszuwählen.  
  
In der folgenden Tabelle sind die Regeln aufgeführt, mit denen ein Präfix für einen registrierten DNS-Namen ausgewählt wird.  
  
|Regel|Erläuterung|  
|--------|---------------|  
|Wählen Sie ein Präfix aus, das wahrscheinlich nicht mehr veraltet ist.|Vermeiden Sie Namen wie z. b. eine Produktlinie oder ein Betriebssystem, die sich in der Zukunft ändern können. Es wird empfohlen, generische Namen wie Corp oder DS zu verwenden.|  
|Wählen Sie ein Präfix aus, das nur Internet Standard Zeichen enthält.|A-z, a-z, 0-9 und (-), aber nicht vollständig numerisch.|  
|Fügen Sie im Präfix höchstens 15 Zeichen ein.|Wenn Sie eine Präfix Länge von höchstens 15 Zeichen auswählen, ist der NetBIOS-Name das gleiche wie das Präfix.|  
  
Es ist wichtig, dass der Active Directory DNS-Besitzer mit dem DNS-Besitzer für die Organisation zusammenarbeitet, um den Besitz des Namens zu erhalten, der für den Active Directory-Namespace verwendet wird. Weitere Informationen zum Entwerfen einer DNS-Infrastruktur zur Unterstützung von AD DS finden Sie unter [Erstellen eines DNS-Infrastruktur Entwurfs](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md).  
  
## <a name="documenting-the-forest-root-domain-name"></a>Dokumentieren des Gesamtstruktur-Stamm Domänen Namens

Dokumentieren Sie das DNS-Präfix und das Suffix, das Sie für die Stamm Domäne der Gesamtstruktur auswählen. Identifizieren Sie an diesem Punkt, welche Domäne der Gesamtstruktur Stamm sein wird. Sie können dem Arbeitsblatt "Domänen Planung", das Sie erstellt haben, die Namen der Gesamtstruktur-Stamm Domäne hinzufügen, um den Plan für neue und aktualisierte Domänen und ihre Domänen Namen zu dokumentieren. Um es zu öffnen, laden Sie Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip aus den [Auftrags Hilfen für Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558) herunter, und öffnen Sie "Domänen Planung" (DSSLOGI_5. doc).

---
ms.assetid: ef4ef4a9-8969-4ad0-bd17-b2bb24f36ef6
title: Auswählen der Stammdomäne der Gesamtstruktur
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c669a5c8103fba52140147957823db978f8b6955
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871351"
---
# <a name="selecting-the-forest-root-domain"></a>Auswählen der Stammdomäne der Gesamtstruktur

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die erste Domäne, die Sie in einer Active Directory-Gesamtstruktur bereitstellen heißt die Stammdomäne der Gesamtstruktur. Diese Domäne bleibt Stammdomäne der Gesamtstruktur, für den Lebenszyklus der AD DS-Bereitstellung.  
  
Gesamtstruktur-Stammdomäne enthält, die Gruppen Organisations-Admins und Schema-Admins. Diese Dienstadministrator-Gruppen werden verwendet, auf Gesamtstrukturebene-Vorgänge wie das Hinzufügen und Entfernen von Domänen und die Implementierung von Änderungen am Schema verwalten.  
  
Auswählen der Stammdomäne der Gesamtstruktur umfasst das bestimmen, wenn eine der Active Directory-Domänen in Ihrem Domänenentwurf als Stammdomäne der Gesamtstruktur verwendet werden kann oder wenn Sie eine dedizierte Gesamtstruktur-Stammdomäne bereitstellen müssen.  
  
Weitere Informationen zum Bereitstellen einer Gesamtstruktur-Stammdomäne, finden Sie unter [Bereitstellen einer Windows Server 2008-Gesamtstruktur-Stammdomäne](https://technet.microsoft.com/library/cc731174.aspx).  
  
## <a name="choosing-a-regional-or-dedicated-forest-root-domain"></a>Auswählen einer regionaler oder dedizierte Gesamtstruktur-Stammdomäne

Wenn Sie ein einziges Domänenmodell anwenden,-Funktionen die einzelne Domäne als Stammdomäne der Gesamtstruktur. Wenn Sie ein Modell mit mehreren Domänen anwenden, können Sie auswählen, eine dedizierte Gesamtstruktur-Stammdomäne bereitstellen, oder wählen Sie eine regionale Domäne als Stammdomäne der Gesamtstruktur ausgeführt.  
  
### <a name="dedicated-forest-root-domain"></a>Dedizierte Gesamtstruktur-Stammdomäne

Eine dedizierte Gesamtstruktur-Stammdomäne ist eine Domäne, die explizit erstellt wird, wird die Funktion als der Gesamtstruktur-Stammdomäne. Es sind keine Benutzerkonten als die Administrator-Dienstkonten für die Stammdomäne der Gesamtstruktur enthalten. Darüber hinaus stellt es nicht in der Domänenstruktur einer beliebigen geografischen Region dar. Alle anderen Domänen in der Gesamtstruktur sind untergeordnete Elemente der dedizierten Gesamtstruktur-Stammdomäne.  

Mithilfe von dedizierten Gesamtstrukturstamm bietet die folgenden Vorteile:  

- Operative Trennung der Gesamtstruktur-Dienstadministratoren von Domänenadministratoren-Dienst. In einer Umgebung mit einzelnem können Mitglieder der Domänen-Admins und der integrierten Gruppe Administratoren standard-Tools und Verfahren Sie Mitglieder der Gruppen Organisations-Admins und Schema-Admins machen. In einer Gesamtstruktur, die eine dedizierte Gesamtstruktur-Stammdomäne verwendet, können nicht Mitglieder der integrierten Gruppe der Administratoren in den regionalen Domänen und Domänen-Admins Mitglieder der Gruppen auf Gesamtstrukturebene Administrator machen. Sie mithilfe von Standardtools und Prozeduren.  
- Schutz vor Änderungen in den in anderen Domänen. Eine dedizierte Gesamtstruktur-Stammdomäne stellt keine bestimmte geografische Region, in der Domänenstruktur dar. Aus diesem Grund ist es nicht betroffen von neuorganisationen oder andere Änderungen, die das Umbenennen oder das Umstrukturieren von Domänen führen.  
- Dient als neutrale Stamm, damit keine Land oder Region angezeigt wird, die einer anderen Region untergeordnet sein. Einige Organisationen, der Darstellung, dass ein Land zu vermeiden oder Region, die ein anderes Land oder Region, in dem Namespace untergeordnet ist. Wenn Sie eine dedizierte Gesamtstruktur-Stammdomäne verwenden, können alle Regionaldomänen Peers in der Domänenhierarchie sein.  

In einer Umgebung mit mehreren regionalen-Domänen in der dedizierten Gesamtstrukturstamm verwendet wird, hat die Replikation der Stammdomäne der Gesamtstruktur nur minimale Auswirkungen auf die Netzwerkinfrastruktur. Dies ist, da der Gesamtstruktur-Stammdomäne nur die Administratorkonten für den Dienst hostet. Der Großteil der Benutzerkonten in der Gesamtstruktur und andere domänenspezifische Daten werden in den regionalen Domänen gespeichert.  
  
Ein Nachteil bei der Verwendung von einer dedizierten Gesamtstruktur-Stammdomäne ist, dass es sich bei der Erstellung zusätzlicher Verwaltungsaufwand, um die zusätzliche Domäne zu unterstützen.  
  
### <a name="regional-domain-as-a-forest-root-domain"></a>Regionale Domäne als einer Gesamtstruktur-Stammdomäne

Wenn Sie keine dedizierte Gesamtstruktur-Stammdomäne bereitstellen, müssen Sie einer Regionaldomäne Funktion als Stammdomäne der Gesamtstruktur auswählen. Diese Domäne ist ist die übergeordnete Domäne alle anderen regionalen Domänen und die erste Domäne, die Sie bereitstellen. Gesamtstruktur-Stammdomäne Benutzerkonten enthält, und wird verwaltet, auf die gleiche Weise, dass die anderen regionalen Domänen verwaltet werden. Der Hauptunterschied besteht darin, dass sie auch die Gruppen Organisations-Admins und Schema-Admins enthält.  
  
Die Auswahl einer Regionaldomäne für Funktion als Stammdomäne der Gesamtstruktur, dass sie nicht den zusätzlichen Verwaltungsaufwand, einen weiteren Domänencontroller verwaltet, erstellt der Vorteil wird erstellt. Auswählen einer geeigneten regionale Domäne der Gesamtstruktur-Stammdomäne, z. B. die Domäne, die Ihre zentrale darstellt oder die Region, die die schnellsten Netzwerkverbindungen sein. Wenn es für Ihre Organisation eine regionale Domäne der Gesamtstruktur-Stammdomäne sein auswählen schwierig ist, können Sie auswählen, zu verwenden. eine dedizierte Gesamtstruktur Stammmodell.  
  
## <a name="assigning-the-forest-root-domain-name"></a>Die Gesamtstruktur-Stammdomänenname zugewiesen

Die Gesamtstruktur-Stammdomänenname ist auch der Name der Gesamtstruktur. Stammnamen der Gesamtstruktur ist, einen Domain Name System (DNS)-Namen, der einem Präfix und Suffix in Form von prefix.suffix besteht. Eine Organisation kann z. B. der Gesamtstruktur Root-Name "corp.contoso.com" verwenden. In diesem Beispiel corp ist das Präfix, und "contoso.com" als Suffix verwendet wird.  
  
Wählen Sie das Suffix aus einer Liste mit vorhandenen Namen in Ihrem Netzwerk. Wählen Sie für das Präfix einen neuen Namen, der nicht in Ihrem Netzwerk zuvor verwendet wurde. Durch Anfügen eines neuen Präfixes an eine vorhandene Suffix, erstellen Sie einen eindeutigen Namespace. Erstellen einen neuen Namespace, für die Active Directory Domain Services (AD DS) wird sichergestellt, dass eine evtl. vorhandene DNS-Infrastruktur nicht geändert werden, um AD DS zu ermöglichen.  
  
### <a name="selecting-a-suffix"></a>Wählen ein suffix

So wählen Sie ein Suffix für die Gesamtstruktur-Stammdomäne aus:  
  
1. Wenden Sie sich an den Besitzer des DNS für die Organisation für eine Liste der registrierten DNS-Suffixe, die auf das Netzwerk verwendet werden, auf denen AD DS gehostet wird. Beachten Sie, dass die Suffixe, die auf dem internen Netzwerk verwendet die Suffixe, die extern verwendet möglicherweise unterscheiden. Beispielsweise kann eine Organisation contosopharma.com im Internet und "contoso.com", auf dem internen Unternehmensnetzwerk verwenden.  
  
2. Wenden Sie sich an den DNS-Besitzer, damit wählen Sie ein Suffix für die Verwendung mit AD DS. Wenn keine geeigneten Suffixe vorhanden sind, registrieren Sie einen neuen Namen mit einem Internet-Autorität für die Benennung.  
  
Es wird empfohlen, dass Sie DNS-Namen verwenden, die mit einer Internet-Zertifizierungsstelle in Active Directory-Namespace registriert sind. Nur die Namen registrierte garantiert sind global eindeutig sein. Wenn später einer anderen Organisation registriert den gleichen DNS-Domänennamen an (oder wenn Ihre Organisation fusioniert mit, oder wird von einem anderen Unternehmen erworben werden, die gleichen DNS-Namen verwendet), können nicht die beiden Infrastrukturen miteinander interagieren.  
  
> [!CAUTION]  
> Verwenden Sie nicht einteiligen DNS-Namen. Weitere Informationen finden Sie Informationen zum Konfigurieren von Windows für Domänen mit einteiligen DNS-Namen ([https://go.microsoft.com/fwlink/?LinkId=106631](https://go.microsoft.com/fwlink/?LinkId=106631)). Darüber hinaus empfehlen wir nicht aufgehoben Suffixe zu verwenden, z. B. ".Local" verwenden.  
  
### <a name="selecting-a-prefix"></a>Ein Präfix auswählen

Wenn Sie ein registriertes Suffix, die bereits im Netzwerk verwendet wird haben, wählen Sie ein Präfix für die Gesamtstruktur-Stammdomänenname mithilfe der Präfix-Regeln in der folgenden Tabelle. Fügen Sie ein Präfix, das derzeit nicht verwendet, um einen neuen untergeordneten Namen zu erstellen ist. Z. B. wenn es sich bei Ihrem DNS-Stamm-Namen "contoso.com" lautet, können Sie die Active Directory-Gesamtstruktur Root Domain Name concorp.contoso.com erstellen, ist der Namespace-concorp.contoso.com nicht bereits im Netzwerk verwendet. Diese neue Verzweigung des Namespace wird ausschließlich für AD DS und kann problemlos in die vorhandene DNS-Implementierung integriert werden.  
  
Wenn Sie einer Regionaldomäne Funktion als einer Gesamtstruktur-Stammdomäne ausgewählt haben, müssen Sie ein neues Präfix für die Domäne zu aktivieren. Da die Gesamtstruktur-Stammdomänenname aller anderen Domänennamen in der Gesamtstruktur betrifft, kann ein regional basierend Name nicht geeignet. Wenn Sie ein neues Suffix, das derzeit nicht im Netzwerk verwendet wird verwenden, können Sie es als der Gesamtstruktur-Stammdomänenname verwenden, ohne ein zusätzliches Präfix auszuwählen.  
  
Die folgende Tabelle enthält die Regeln für die Auswahl eines Präfixes für eine DNS-Name registriert.  
  
|Regel|Erläuterung|  
|--------|---------------|  
|Wählen Sie ein Präfix, das nicht wahrscheinlich veraltet ist.|Vermeiden Sie Namen, z. B. eine Produktlinie oder das Betriebssystem, das in der Zukunft ändern kann. Es wird empfohlen, mithilfe von generischen Namen wie das Unternehmen oder ds.|  
|Wählen Sie ein Präfix, das Internet nur standardmäßige Zeichen enthält.|A-Z, a – Z, 0-9 und (-), aber nicht vollständig numerische.|  
|15 Zeichen enthalten oder weniger in das Präfix.|Bei Auswahl eine Präfixlänge von höchstens 15 Zeichen ist der NetBIOS-Name identisch mit dem Präfix.|  
  
Es ist wichtig für den Active Directory DNS-Besitzer, arbeiten Sie mit dem DNS-Besitzer für die Organisation in den Besitz des Namens, der für den Active Directory-Namespace verwendet wird. Weitere Informationen zum Entwerfen von DNS-Infrastruktur zur Unterstützung von AD DS finden Sie unter [erstellen einen DNS-Infrastruktur-Entwurf](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md).  
  
## <a name="documenting-the-forest-root-domain-name"></a>Dokumentieren die Gesamtstruktur-Stammdomänenname

Dokumentieren Sie die DNS-Präfix und Suffix ein, die Sie für die Stammdomäne der Gesamtstruktur auswählen. An diesem Punkt zu ermitteln, welche Domäne der Gesamtstruktur-Stammdomäne sein wird. Sie können der Gesamtstruktur Stammdomänen-Namensinformationen in das Arbeitsblatt "Planen der Domäne" hinzufügen, die Sie erstellt haben, um Ihren Plan für neue und aktualisierte Domänen und Ihre Domänennamen zu dokumentieren. Laden Sie zum Öffnen Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip aus [Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558) , und öffnen Sie "Domäne" Planning"(DSSLOGI_5.doc).

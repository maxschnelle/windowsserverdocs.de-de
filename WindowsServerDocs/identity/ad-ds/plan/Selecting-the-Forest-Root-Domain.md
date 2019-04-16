---
ms.assetid: ef4ef4a9-8969-4ad0-bd17-b2bb24f36ef6
title: "Auswählen der Stammdomäne der Gesamtstruktur"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d87273df1e42e1fa88df09e0b86d4c86ea75ee3f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="selecting-the-forest-root-domain"></a>Auswählen der Stammdomäne der Gesamtstruktur

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Die erste Domäne, die Sie in einer Active Directory-Gesamtstruktur bereitstellen wird als Stammdomäne der Gesamtstruktur bezeichnet. Diese Domäne bleibt die Gesamtstruktur-Stammdomäne für den Lebenszyklus der AD DS-Bereitstellung.  
  
Gesamtstruktur-Stammdomäne enthält die Gruppen Organisations-Admins und Schema-Admins. Diese Dienstadministrator-Gruppen sind zum Verwalten von auf Gesamtstrukturebene Vorgänge wie das Hinzufügen und Entfernen von Domänen und die Implementierung der Änderung des Schemas verwendet.  
  
Auswählen der Stammdomäne der Gesamtstruktur werden bestimmt wird, wenn eines der Active Directory-Domänen in Ihrem Domänenentwurf als Stammdomäne der Gesamtstruktur verwendet werden kann oder wenn Sie eine dedizierte Gesamtstruktur-Stammdomäne bereitstellen müssen.  
  
Weitere Informationen zum Bereitstellen einer Gesamtstruktur-Stammdomäne, finden Sie unter [Bereitstellen einer Gesamtstruktur-Stammdomäne von Windows Server2008](https://technet.microsoft.com/library/cc731174.aspx).  
  
## <a name="choosing-a-regional-or-dedicated-forest-root-domain"></a>Auswählen einer regionale oder dedizierte Gesamtstruktur-Stammdomäne  
Wenn Sie ein einfaches Domänenmodell anwenden, funktioniert die einzelne Domäne als Stammdomäne der Gesamtstruktur. Wenn Sie ein Modell mit mehreren Domänen anwenden möchten, können Sie auswählen, eine dedizierte Gesamtstruktur-Stammdomäne bereitstellen oder wählen Sie eine regionale Domäne als Stammdomäne der Gesamtstruktur verwendet.  
  
### <a name="dedicated-forest-root-domain"></a>Dedizierte Gesamtstruktur-Stammdomäne  
Eine dedizierte Gesamtstruktur-Stammdomäne ist eine Domäne, die speziell erstellt wird, wird als Stamm der Gesamtstruktur verwendet. Es enthält keine Benutzerkonten als Konten für die Gesamtstruktur-Stammdomäne. Darüber hinaus stellt keine geografische Region in der Domänenstruktur dar. Alle anderen Domänen in der Gesamtstruktur sind untergeordnete Elemente des dedizierten Gesamtstruktur-Stammdomäne.  
  
Mithilfe von dedizierten Gesamtstrukturstamm bietet die folgenden Vorteile:  
  
-   Betriebliche Trennung der Gesamtstruktur Dienstadministratoren von Dienstadministratoren für die Domäne. In einer Umgebung mit einzelnem können Mitglieder der Domänen-Admins und der integrierten Gruppe Administratoren Standard-Tools und Verfahren Sie sich vergewissern, dass Mitglieder der Gruppen Organisations-Admins und Schema-Admins. Mitglieder der Domänen-Admins und der vordefinierten Gruppe Administratoren in der Regionaldomänen in einer Gesamtstruktur, die eine dedizierte Gesamtstruktur-Stammdomäne verwendet, können nicht selbst Mitglieder der Gruppen Administratoren auf Gesamtstrukturebene werden mithilfe von Standard-Tools und Verfahren.  
  
-   Schutz vor der Änderung der in anderen Domänen. Eine dedizierte Gesamtstruktur-Stammdomäne stellt keine bestimmte geografische Region in der Domänenstruktur dar. Aus diesem Grund ist es nicht betroffen, durch Reorganisationen oder andere Änderungen, die dem Umbenennen bzw. Umstrukturieren von Domänen führen.  
  
-   Dient als neutral Stamm, damit keine Land/Ihrer Region angezeigt wird, die einer anderen Region untergeordnet sein. In manchen Organisationen, der Darstellung vermeiden Sie, dass ein Land oder Region zu einem anderen Land oder Region im Namespace untergeordnet ist. Wenn Sie eine dedizierte Gesamtstruktur-Stammdomäne verwenden, können alle Regionaldomänen Peers in der Domänenhierarchie sein.  
  
In einer Umgebung mit mehreren regionale Domänen in der dedizierten Gesamtstrukturstamm verwendet wird, hat die Replikation der Stammdomäne der Gesamtstruktur nur minimalen Einfluss auf die Netzwerkinfrastruktur. Dies liegt daran den Stamm der Gesamtstruktur nur Konten hostet. Der Großteil der Benutzerkonten in der Gesamtstruktur und andere domänenspezifische Daten werden in der regionalen Domäne gespeichert.  
  
Ein Nachteil mit einer dedizierten Gesamtstruktur-Stammdomäne ist zusätzlicher Verwaltungsaufwand zur Unterstützung weiteren Domänencontroller erstellt.  
  
### <a name="regional-domain-as-a-forest-root-domain"></a>Regionale Domäne als eine Gesamtstruktur-Stammdomäne  
Wenn Sie keine dedizierte Gesamtstruktur-Stammdomäne bereitstellen, müssen Sie eine regionale Domäne, die als Stammdomäne der Gesamtstruktur funktionieren auswählen. Diese Domäne ist wird von der übergeordneten Domäne aller anderen regionalen Domänen und die erste Domäne, die Sie bereitstellen. Gesamtstruktur-Stammdomäne enthält Benutzerkonten und verwaltet wird, auf die gleiche Weise, dass die anderen regionalen Domänen verwaltet werden. Der Hauptunterschied besteht darin, dass sie außerdem die Gruppen Organisations-Admins und Schema-Admins enthält.  
  
Der Vorteil der regionale Domäne mit der Funktion auswählen, wie die Gesamtstruktur-Stammdomäne, es wird jedoch den zusätzlichen Verwaltungsaufwand, verwalten einen weiteren Domänencontroller erstellt erstellt. Wählen Sie eine geeignete regionale Domäne als Stamm der Gesamtstruktur, z.B. die Domäne, die Ihrem Hauptsitz stellt oder der Region, das den schnellsten Netzwerkverbindungen verfügt. Ist es schwierig für Ihre Organisation eine regionale Domäne der Gesamtstruktur-Stammdomäne sein auswählen, können Sie stattdessen eine dedizierte Gesamtstruktur Stamm-Modell verwenden.  
  
## <a name="assigning-the-forest-root-domain-name"></a>Name der Stammdomäne der Gesamtstruktur zuweisen  
Name der Stammdomäne der Gesamtstruktur ist auch der Name der Gesamtstruktur. Der Name der Gesamtstruktur-Stamm ist ein Domain Name System (DNS)-Name, der ein Präfix und ein Suffix in Form von prefix.Suffix besteht. Eine Organisation kann z.B. Name für den Stamm der Gesamtstruktur corp.contoso.com haben. In diesem Beispiel corp ist das Präfix und contoso.com ist das Suffix.  
  
Wählen Sie das Suffix aus einer Liste mit vorhandenen Namen in Ihrem Netzwerk. Das Präfix wählen Sie einen neuen Namen, der nicht in Ihrem Netzwerk zuvor verwendet wurde. Indem Sie ein neues Präfix an eine vorhandene Suffix, erstellen Sie einen eindeutigen Namespace. Erstellen einen neuen Namespace für Active Directory-Domänendienste (AD DS) wird sichergestellt, dass alle vorhandenen DNS-Infrastruktur nicht geändert werden, um AD DS zu berücksichtigen muss.  
  
### <a name="selecting-a-suffix"></a>Ein Suffix auswählen  
So wählen Sie ein Suffix für die Gesamtstruktur-Stammdomäne aus:  
  
1.  Wenden Sie sich an den DNS-Besitzer für die Organisation eine Liste der registrierten DNS-Suffixe, die auf das Netzwerk verwendet werden, auf denen AD DS gehostet wird. Beachten Sie, dass die Suffixe verwendet, auf dem internen Netzwerk unterscheidet sich die Suffixe extern verwendet werden können. Beispielsweise kann eine Organisation contosopharma.com im Internet und contoso.com im internen Unternehmensnetzwerk verwenden.  
  
2.  Wenden Sie sich an den Besitzer DNS-Suffix für die Verwendung mit AD DS zu aktivieren. Wenn keine geeignete Suffixe vorhanden sind, registrieren Sie einen neuen Namen mit einem Internetzeitserver Autorität für die Benennung.  
  
Es wird empfohlen, dass Sie DNS-Namen verwenden, die bei einer Internet-Registrierungsstelle in Active Directory-Namespace registriert sind. Nur die Namen registrierte sind garantiert global eindeutig sein. Wenn später eine andere Organisation den gleichen DNS-Domänennamen registriert (oder wenn Ihrer Organisation mit zusammengeführt, erwirbt oder wird von einem anderen Unternehmen erworben, die gleichen DNS-Namen verwendet), können nicht zwei Infrastrukturen miteinander interagieren.  
  
> [!CAUTION]  
> Verwenden Sie keine DNS-Namen mit einfacher Bezeichnung. Weitere Informationen finden Sie Informationen zum Konfigurieren von Windows für Domänen mit einfacher Bezeichnung DNS-Namen ([https://go.microsoft.com/fwlink/?LinkId=106631](https://go.microsoft.com/fwlink/?LinkId=106631)). Darüber hinaus empfehlen wir nicht aufgehoben Suffixe, z.B. ".Local" verwenden.  
  
### <a name="selecting-a-prefix"></a>Ein Präfix auswählen  
Wenn Sie ein registriertes Suffix ausgewählt, die bereits im Netzwerk verwendet wird haben, wählen Sie ein Präfix für Name der Stammdomäne der Gesamtstruktur mit dem Präfix Regeln in der folgenden Tabelle. Fügen Sie ein Präfix, das derzeit nicht zum Erstellen eines neuen untergeordneten Namens verwendet wird. Wenn beispielsweise Ihr DNS-Stammnamen contoso.com ist, können Sie Active Directory-Gesamtstruktur Stammdomänenname concorp.contoso.com erstellen, wenn der Namespace concorp.contoso.com nicht bereits im Netzwerk verwendet wird. Diese neuen Verzweigung der Namespace wird in AD DS zugeordnet werden und kann problemlos in die vorhandene DNS-Implementierung integriert werden.  
  
Wenn Sie eine regionale Domäne als eine Gesamtstruktur-Stammdomäne verwendet haben, müssen Sie ein neues Präfix für die Domäne auswählen. Da der Name der Stammdomäne der Gesamtstruktur alle anderen Domänennamen in der Gesamtstruktur betrifft, kann ein regional je nicht geeignet. Wenn Sie ein neues Suffix, das derzeit nicht im Netzwerk verwendet wird verwenden, können Sie es als Name der Stammdomäne der Gesamtstruktur verwenden, ohne ein zusätzliches Präfix auswählen.  
  
Die folgende Tabelle enthält die Regeln für ein Präfix für einen registrierten DNS-Namen auswählen.  
  
|Regel|Erläuterung|  
|--------|---------------|  
|Wählen Sie ein Präfix, das nicht wahrscheinlich veraltet ist.|Vermeiden Sie Namen, z. B. einer Produktfamilie oder das Betriebssystem, die in der Zukunft ändern kann. Es wird empfohlen, generische Namen wie z.B. corp oder ds verwenden.|  
|Wählen Sie ein Präfix, das nur Internet standard Zeichen enthält.|A-Z, a-Z, 0-9 und (-), aber nicht vollständig numerischen.|  
|Mehr als 15 Zeichen enthalten oder weniger in das Präfix.|Wenn Sie eine Präfixlänge von höchstens 15 Zeichen auswählen, wird der NetBIOS-Name identisch mit dem Präfix.|  
  
Es ist wichtig für den Active Directory-DNS-Besitzer für die Arbeit mit der DNS-Besitzer für die Organisation den Besitz des Namens zu erhalten, die für den Active Directory-Namespace verwendet werden. Weitere Informationen zum Entwerfen einer DNS-Infrastruktur zur Unterstützung von AD DS finden Sie unter [erstellen einen DNS-Infrastruktur-Entwurf](../../ad-ds/plan/Creating-a-DNS-Infrastructure-Design.md).  
  
## <a name="documenting-the-forest-root-domain-name"></a>Dokumentieren der Name der Stammdomäne der Gesamtstruktur  
Dokumentieren Sie den DNS-Präfix und das Suffix, die Sie für die Gesamtstruktur-Stammdomäne auswählen. Zu diesem Zeitpunkt zu identifizieren, welche Domäne den Stamm der Gesamtstruktur sein wird. Sie können der Gesamtstruktur Stammdomänen-Namensinformationen in das Arbeitsblatt "Planen der Domäne" hinzufügen, die Sie erstellt haben, um Ihr Plan für die neuen und aktualisierten Domänen und den Domänennamen zu dokumentieren. Um es zu öffnen, laden Sie Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip vom Auftrag Hilfsmittel für Windows Server2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), und öffnen Sie "Domäne" Planning"(DSSLOGI_5.doc).  
  



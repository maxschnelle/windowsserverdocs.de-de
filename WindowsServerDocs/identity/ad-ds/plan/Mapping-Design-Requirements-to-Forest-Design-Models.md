---
ms.assetid: c0d64566-5530-482e-a332-af029a5fb575
title: Zuordnen von Entwurfsanforderungen zu Gesamtstruktur-Entwurfsmodellen
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 48a2b03c6e29afcca565e861383a831050ef4233
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="mapping-design-requirements-to-forest-design-models"></a>Zuordnen von Entwurfsanforderungen zu Gesamtstruktur-Entwurfsmodellen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Die meisten Gruppen in Ihrer Organisation können eine einzelne Organisationseinheit Gesamtstruktur freigeben, die von einer einzelnen Gruppe Informationstechnologie (IT) verwaltet wird und enthält die Benutzer- und Ressourcen für alle Gruppen, die die Gesamtstruktur gemeinsam nutzen. Dieser freigegebenen Gesamtstruktur, mit dem Namen der erste Organisationseinheiten Gesamtstruktur ist die Grundlage für das Design-Gesamtstrukturmodell für die Organisation.  
  
Da die erste Organisationseinheit Gesamtstruktur mehrere Gruppen in der Organisation gehostet werden kann, muss der Gesamtstrukturbesitzer Service Level Agreements mit jeder Gruppe richten, sodass alle Parteien verstehen, was Sie erwartet wird. Dies schützt den einzelnen Gruppen und der Gesamtstrukturbesitzer, durch die Einrichtung der vereinbarten-Dienst erwartet.  
  
Nicht alle Gruppen in Ihrer Organisation können eine einzelne Organisationseinheit Gesamtstruktur freigeben, müssen Sie den Gesamtstrukturentwurf an die Anforderungen der verschiedenen Gruppen gerecht zu erweitern. Dies beinhaltet das Identifizieren der Designanforderungen, die zu den Gruppen, basierend auf ihren Anforderungen für Autonomie und Isolation und davon, ob sie ein Netzwerk begrenzt-Konnektivität verfügen, gelten, und klicken Sie dann identifiziert das Gesamtstrukturmodell, das Sie verwenden können, um diese Anforderungen Rechnung zu tragen. Die folgende Tabelle enthält die Gesamtstruktur Modell Entwicklungsszenarien basierend auf der Autonomie, Isolation und Konnektivität Faktoren. Nachdem Sie das Szenario der Gesamtstruktur-Entwurf, das Ihren Anforderungen am besten entspricht identifiziert, zu bestimmen, ob Sie weiteren Entscheidungen Spezifikationen für den Entwurf zu erfüllen müssen.  
  
> [!NOTE]  
> Wenn ein Faktor als n/v aufgeführt ist, ist es nicht berücksichtigt, da andere Anforderungen auch dieser Faktor Rechnung tragen.  
  
|Szenario|Eingeschränkter Konnektivität|Datenisolation|Datenautonomie|Isolation von Diensten|Autonomie eines Dienstes|  
|------------|------------------------|------------------|-----------------|---------------------|--------------------|  
|[Szenario 1: Hinzufügen einer vorhandenen Gesamtstruktur für Datenautonomie](#BKMK_1)|Nein|Nein|Ja|Nein|Nein|  
|[Szenario 2: Verwenden Sie eine Organisationseinheit Gesamtstruktur oder Domäne für die Autonomie eines Dienstes](#BKMK_2)|Nein|Nein|N/V|Nein|Ja|  
|[Szenario 3: Verwenden Sie eine Organisationseinheit Gesamtstruktur oder Ressourcen-Gesamtstruktur für die Dienstisolation](#BKMK_3)|Nein|Nein|N/V|Ja|N/V|  
|[Szenario 4: Verwenden Sie eine Organisationseinheit Gesamtstruktur oder mit eingeschränktem Zugriff für die datenisolierung](#BKMK_4)|N/V|Ja|N/V|N/V|N/V|  
|[Szenario 5: Verwenden einer Organisationseinheiten Gesamtstruktur, oder ändern Sie die Firewall bei eingeschränkter Verbindung](#BKMK_5)|Ja|Nein|N/V|Nein|Nein|  
|[Szenario 6: Verwenden Sie einer Organisationseinheit Gesamtstruktur oder Domäne, und konfigurieren Sie die Firewall für die Autonomie eines Dienstes mit eingeschränkter Konnektivität](#BKMK_6)|Ja|Nein|N/V|Nein|Ja|  
|[Szenario 7: Ressourcengesamtstruktur verwenden und Konfigurieren der Firewalls für die Dienstisolation mit eingeschränkter Konnektivität](#BKMK_7)|Ja|Nein|N/V|Ja|N/V|  
  
## <a name="BKMK_1"></a>Szenario 1: Hinzufügen einer vorhandenen Gesamtstruktur für Datenautonomie  
Sie können eine Voraussetzung für die Daten-, indem Sie einfach als Host der Gruppe in Organisationseinheiten (OUs) in einer vorhandenen Gesamtstruktur für die Organisation erfüllen. Delegieren der Steuerung der Organisationseinheiten an Datenadministratoren aus der Gruppe die Datenautonomie zu erzielen. Weitere Informationen zum Zuweisen der Verwaltung mithilfe von Organisationseinheiten finden Sie unter [erstellen eine Organizational Unit Design](../../ad-ds/plan/Creating-an-Organizational-Unit-Design.md).  
  
## <a name="BKMK_2"></a>Szenario 2: Verwenden Sie eine Organisationseinheit Gesamtstruktur oder Domäne für die Autonomie eines Dienstes  
Wenn eine Gruppe in Ihrer Organisation Service Autonomie als Anforderung identifiziert, empfehlen wir, dass Sie zuerst diese Anforderung überdenken. Erzielen von Service Autonomie erstellt Weitere Verwaltungsaufwand und zusätzliche Kosten für die Organisation. Stellen Sie sicher, dass die Anforderung für die Autonomie eines Dienstes nicht einfach zur Vereinfachung ist und Sie die Kosten für diese Anforderung erfüllt rechtfertigen können.  
  
Sie können eine Anforderung für den Dienstautonomie erfüllen, mit einer der folgenden Aktionen:  
  
-   Erstellen eine Organisationseinheit Gesamtstruktur. Platzieren Sie die Benutzer, Gruppen und Computer für die Gruppe, die Autonomie eines Dienstes in einer separaten Organisationseinheit Gesamtstruktur erforderlich sind. Weisen Sie eine Person aus der Gruppe die Gesamtstrukturbesitzer sein. Wenn der Zugriff auf Ressourcen mit anderen Gesamtstrukturen in der Organisation muss, können sie eine Vertrauensstellung zwischen ihrer Organisation Gesamtstruktur und den anderen Gesamtstrukturen einrichten.  
  
-   Mithilfe von Organisationseinheiten Domänen. Platzieren Sie die Benutzer, Gruppen und Computer in einer anderen Domäne in einer vorhandenen Gesamtstruktur für die Organisationseinheit. Dieses Modell ermöglicht nur auf Domänenebene Autonomie und Isolation oder Daten Netzwerkisolation nicht für die vollständige Service-Autonomie service.  
  
Weitere Informationen zur Verwendung von Organisationseinheiten Domänen finden Sie unter [mit der Organisationseinheit Domain-Gesamtstrukturmodell](../../ad-ds/plan/../../ad-ds/plan/Using-the-Organizational-Domain-Forest-Model.md).  
  
## <a name="BKMK_3"></a>Szenario 3: Verwenden Sie eine Organisationseinheit Gesamtstruktur oder Ressourcen-Gesamtstruktur für die Dienstisolation  
Sie können eine Voraussetzung für die Dienstisolation erfüllen, indem Sie einen der folgenden:  
  
-   Verwenden eine Organisationseinheit Gesamtstruktur. Platzieren Sie die Benutzer, Gruppen und Computer für die Gruppe, die Isolation von Diensten in einer separaten Organisationseinheit Gesamtstruktur erforderlich sind. Weisen Sie eine Person aus der Gruppe die Gesamtstrukturbesitzer sein. Wenn der Zugriff auf Ressourcen mit anderen Gesamtstrukturen in der Organisation muss, können sie eine Vertrauensstellung zwischen ihrer Organisation Gesamtstruktur und den anderen Gesamtstrukturen einrichten. Allerdings empfohlen nicht dieser Ansatz, da Zugriff auf Ressourcen über universelle Gruppen in der Gesamtstruktur-Vertrauensstellung Szenarien stark eingeschränkt sind.  
  
-   Verwenden eine Ressourcen-Gesamtstruktur. Direkte Ressourcen und Dienstkonten in einer separaten Ressourcen-Gesamtstruktur, damit Benutzerkonten in einer vorhandenen Gesamtstruktur für die Organisationseinheit. Bei Bedarf können alternative Konten erstellt werden, in der Gesamtstruktur den Zugriff auf Ressourcen in der Ressourcengesamtstruktur, wenn die Organisation Gesamtstruktur nicht mehr verfügbar ist. Die alternativen Konten benötigen die erforderliche Autorität zur Anmeldung an der Ressourcengesamtstruktur und Kontrolle über die Ressourcen warten, bis die Organisationseinheit Gesamtstruktur wieder online ist.  
  
    Richten Sie eine Vertrauensstellung zwischen der Ressource und Organisations-Gesamtstrukturen, sodass der Benutzer auf die Ressourcen in der Gesamtstruktur zugreifen können, bei der Verwendung von ihren normalen Benutzerkonten. Diese Konfiguration ermöglicht die zentralisierte Verwaltung von Benutzerkonten während Benutzer alternative Konten in der Ressourcengesamtstruktur zurückgegriffen, wenn die Organisation Gesamtstruktur nicht mehr verfügbar ist.  
  
Die folgenden: Überlegungen zur Dienstisolation  
  
-   Für Dienstisolation erstellten Gesamtstrukturen können Domänen aus anderen Gesamtstrukturen vertrauen, jedoch dürfen keine Benutzer aus anderen Gesamtstrukturen in ihren Dienst Administratorgruppen enthalten. Wenn Benutzer aus anderen Gesamtstrukturen in administrativen Gruppen in der isolierten Gesamtstruktur enthalten sind, kann die Sicherheit der isolierten Gesamtstruktur möglicherweise gefährdet, da die Dienstadministratoren in der Gesamtstruktur nicht exklusive Steuerung verfügen.  
  
-   Als Domänencontroller in einem Netzwerk zugänglich sind, sind sie Angriffen (z. B. Denial-of-Service-Angriffe) vor schädlicher Software in diesem Netzwerk. Sie können zum Schutz gegen die Möglichkeit eines Angriffs die folgenden Schritte ausführen:  
  
    -   Hosten von Domänencontrollern nur auf Netzwerke, die als sicher eingestuft werden.  
  
    -   Beschränken Sie den Zugriff auf Netzwerke, die der Domänencontroller hostet.  
  
-   Dienstisolation ist die Erstellung einer zusätzlichen Gesamtstruktur erforderlich. Bewerten Sie, ob die Kosten für die Verwaltung der Infrastruktur zur Unterstützung der zusätzlichen Gesamtstruktur die Kosten im Zusammenhang mit der Zugriff auf Ressourcen aufgrund einer Organisationseinheit Gesamtstruktur nicht verfügbar ist aufwiegt.  
  
## <a name="BKMK_4"></a>Szenario 4: Verwenden Sie eine Organisationseinheit Gesamtstruktur oder mit eingeschränktem Zugriff für die datenisolierung  
Sie können Datenisolation erreichen, führen Sie einen der folgenden:  
  
-   Verwenden eine Organisationseinheit Gesamtstruktur. Platzieren Sie die Benutzer, Gruppen und Computer für die Gruppe, die Datenisolation in einer separaten Organisationseinheit Gesamtstruktur erforderlich sind. Weisen Sie eine Person aus der Gruppe die Gesamtstrukturbesitzer sein. Wenn der Zugriff auf Ressourcen mit anderen Gesamtstrukturen in der Organisation muss, richten Sie eine Vertrauensstellung zwischen der Gesamtstruktur der Organisation und den anderen Gesamtstrukturen aufweist. Nur Benutzer, die Zugriff auf vertrauliche Informationen benötigen, die in der neuen Organisationseinheit Gesamtstruktur vorhanden sein. Benutzer haben ein Konto, mit denen sie den Zugriff auf beide klassifiziert Daten in ihrer eigenen Gesamtstruktur und ungeschützten Daten in anderen Gesamtstrukturen mit Vertrauensstellungen.  
  
-   Verwenden eine Gesamtstruktur mit eingeschränktem Zugriff. Dies ist einer separaten Gesamtstruktur mit den geschützten Daten und die Benutzerkonten, die Zugriff auf diese Daten verwendet werden. Separate Benutzerkonten werden in den vorhandenen Organisationseinheiten Gesamtstrukturen verwaltet, die Zugriff auf die uneingeschränkten Ressourcen im Netzwerk verwendet werden. Keine Vertrauensstellungen werden zwischen der Gesamtstruktur mit eingeschränktem Zugriff und anderen Gesamtstrukturen im Unternehmen erstellt. Sie können weitere die Gesamtstruktur einschränken, indem der Gesamtstruktur auf einem separaten physischen Netzwerk bereitstellen, damit es nicht mit anderen Gesamtstrukturen verbinden kann. Wenn Sie die Gesamtstruktur in einem separaten Netzwerk bereitstellen, müssen Benutzer zwei Arbeitsstationen verfügen: eine für den Zugriff auf die eingeschränkten Gesamtstruktur und eine für den Zugriff auf die nonrestricted Bereiche des Netzwerks.  
  
Die folgenden: Überlegungen beim Erstellen von Gesamtstrukturen  
  
-   Organisatorische Gesamtstrukturen, die für die datenisolierung erstellt Domänen aus anderen Gesamtstrukturen vertrauen können, aber Benutzer aus anderen Gesamtstrukturen darf nicht in einem der folgenden enthalten sein:  
  
    -   Gruppen, die verantwortlich für Servicemanagement oder Gruppen, die die Mitgliedschaft der Dienstadministrator-Gruppen verwalten können  
  
    -   Gruppen, die administrativen Kontrolle über Computer verfügen, die geschützte Daten speichern  
  
    -   Gruppen, die Zugriff auf geschützte Daten oder Gruppen, die sind verantwortlich für die Verwaltung von Benutzerobjekten oder Gruppenobjekten, die Zugriff auf geschützte Daten  
  
    Wenn Benutzer aus einer anderen Gesamtstruktur in einer dieser Gruppen enthalten sind, kann eine Gefährdung der anderen Gesamtstruktur zu einer Gefährdung der Gesamtstruktur isoliert und Offenlegung von geschützten Daten führen.  
  
-   Anderen Gesamtstrukturen können konfiguriert werden, um das Vertrauen der Organisationseinheiten Gesamtstruktur für die datenisolierung erstellt werden, sodass Benutzer in der isolierten Gesamtstruktur auf Ressourcen in anderen Gesamtstrukturen zugreifen können. Allerdings müssen Benutzer aus der isolierten Gesamtstruktur nie interaktiv auf Arbeitsstationen in der vertrauenden Gesamtstruktur anmelden. Der Computer in der vertrauenden Gesamtstruktur kann potenziell gefährliche Software kompromittiert werden und kann verwendet werden, um die Anmeldeinformationen des Benutzers zu erfassen.  
  
    > [!NOTE]  
    > Um Server in einer vertrauenden Gesamtstruktur Identität von Benutzern in der isolierten Gesamtstruktur, und klicken Sie dann Zugriff auf Ressourcen in der isolierten Gesamtstruktur zu verhindern, kann der Gesamtstrukturbesitzer deaktivieren Sie die delegierte Authentifizierung oder verwenden Sie das Feature für die eingeschränkte Delegierung. Weitere Informationen zur delegierten Authentifizierung und eingeschränkte Delegierung finden Sie unter Delegieren der Authentifizierung ([https://go.microsoft.com/fwlink/?LinkId=106614](https://go.microsoft.com/fwlink/?LinkId=106614)).  
  
-   Sie müssen möglicherweise eine Firewall zwischen der Gesamtstruktur der Organisation und den anderen Gesamtstrukturen in der Organisation Einschränken des Zugriffs auf Daten außerhalb ihrer Gesamtstruktur hergestellt.  
  
-   Erstellen einer separaten Gesamtstruktur Datenisolation ermöglicht, zwar als Domänencontroller in der isolierten Gesamtstruktur und der Computer die geschützte Hostinformationen in einem Netzwerk zugegriffen werden sind sie Angriffen auf Computern, auf das Netzwerk gestartet. Organisationen, die festlegen, dass das Risiko eines Angriffs zu hoch ist oder zur Folge, dass eine Verletzung der Angriff oder Sicherheit zu groß ist Beschränken des Zugriffs auf Netzwerke, auf denen die Domänencontroller gehostet werden müssen, und die Computer, auf denen gehostet werden geschützte Daten. Einschränken des Zugriffs kann durch Verwendung von Technologien wie Firewalls und Internet Protocol Security (IPsec) erfolgen. In extremen Fällen können Organisationen die geschützten Daten auf einem unabhängigen Netzwerk verwalten, die keine physische Verbindung mit einem anderen Netzwerk in der Organisation hat.  
  
    > [!NOTE]  
    > Wenn Netzwerkkonnektivität zwischen einer Gesamtstruktur mit eingeschränktem Zugriff und einem anderen Netzwerk vorhanden ist, besteht die Möglichkeit für Daten im eingeschränkten Bereich auf den anderen Netzwerk übertragen werden.  
  
## <a name="BKMK_5"></a>Szenario 5: Verwenden einer Organisationseinheiten Gesamtstruktur, oder ändern Sie die Firewall bei eingeschränkter Verbindung  
Um ein eingeschränkter Konnektivität-Anforderung zu erfüllen, können Sie einen der folgenden Schritte ausführen:  
  
-   Platzieren Sie die Benutzer in einer vorhandenen Gesamtstruktur für die Organisationseinheit, und öffnen Sie die Firewall genug zum Zulassen von Active Directory-Datenverkehr passieren.  
  
-   Verwenden Sie eine Organisationseinheit Gesamtstruktur. Platzieren Sie die Benutzer, Gruppen und Computer für die Gruppe, die für die Verbindung eingeschränkt ist in einer separaten Organisationseinheit Gesamtstruktur. Weisen Sie eine Person aus der Gruppe die Gesamtstrukturbesitzer sein. Die Organisationseinheit Gesamtstruktur bietet eine separate Umgebung auf der anderen Seite der Firewall. Die Gesamtstruktur enthält Benutzerkonten und Ressourcen, die innerhalb der Gesamtstruktur verwaltet werden, sodass Benutzer nicht benötigen, um durch die Firewall ihren täglichen Aufgaben zu wechseln. Bestimmte Benutzer oder Anwendungen möglicherweise spezielle Anforderungen, die die Möglichkeit, durch die Firewall an anderen Gesamtstrukturen übergeben müssen. Sie können diese Anforderungen einzeln erfüllen, öffnen Sie die entsprechenden Schnittstellen in der Firewall, einschließlich derer, die für alle Vertrauensstellungen, um die Funktion erforderlich.  
  
Weitere Informationen zum Konfigurieren von Firewalls für die Verwendung mit Active Directory-Domänendiensten (AD DS) finden Sie unter Active Directory in Netzwerken durch Firewalls segmentiert ([https://go.microsoft.com/fwlink/?LinkId=37928](https://go.microsoft.com/fwlink/?LinkId=37928)).  
  
## <a name="BKMK_6"></a>Szenario 6: Verwenden Sie einer Organisationseinheit Gesamtstruktur oder Domäne, und konfigurieren Sie die Firewall für die Autonomie eines Dienstes mit eingeschränkter Konnektivität  
Wenn eine Gruppe in Ihrer Organisation Service Autonomie als Anforderung identifiziert, empfehlen wir, dass Sie zuerst diese Anforderung überdenken. Erzielen von Service Autonomie erstellt Weitere Verwaltungsaufwand und zusätzliche Kosten für die Organisation. Stellen Sie sicher, dass die Anforderung für die Autonomie eines Dienstes nicht einfach zur Vereinfachung ist und Sie die Kosten für diese Anforderung erfüllt rechtfertigen können.  
  
Wenn eingeschränkter Konnektivität ein Problem ist, und Sie eine Anforderung für die Autonomie eines Dienstes haben, können Sie Folgendes tun:  
  
-   Verwenden Sie eine Organisationseinheit Gesamtstruktur. Platzieren Sie die Benutzer, Gruppen und Computer für die Gruppe, die Autonomie eines Dienstes in einer separaten Organisationseinheit Gesamtstruktur erforderlich sind. Weisen Sie eine Person aus der Gruppe die Gesamtstrukturbesitzer sein. Die Organisationseinheit Gesamtstruktur bietet eine separate Umgebung auf der anderen Seite der Firewall. Die Gesamtstruktur enthält Benutzerkonten und Ressourcen, die innerhalb der Gesamtstruktur verwaltet werden, sodass Benutzer nicht benötigen, um durch die Firewall ihren täglichen Aufgaben zu wechseln. Bestimmte Benutzer oder Anwendungen möglicherweise spezielle Anforderungen, die die Möglichkeit, durch die Firewall an anderen Gesamtstrukturen übergeben müssen. Sie können diese Anforderungen einzeln erfüllen, öffnen Sie die entsprechenden Schnittstellen in der Firewall, einschließlich derer, die für alle Vertrauensstellungen, um die Funktion erforderlich.  
  
-   Platzieren Sie die Benutzer, Gruppen und Computer in einer anderen Domäne in einer vorhandenen Gesamtstruktur für die Organisationseinheit. Dieses Modell ermöglicht nur auf Domänenebene Autonomie und Isolation oder Daten Netzwerkisolation nicht für die vollständige Service-Autonomie service. Andere Gruppen in der Gesamtstruktur müssen die Dienstadministratoren der neuen Domäne auf demselben Sicherheitsgrad vertrauen, dass sie den Gesamtstrukturbesitzer vertrauen. Aus diesem Grund empfehlen wir nicht dieser Ansatz. Weitere Informationen zur Verwendung von Organisationseinheiten Domänen finden Sie unter [mit der Organisationseinheit Domain-Gesamtstrukturmodell](../../ad-ds/plan/../../ad-ds/plan/Using-the-Organizational-Domain-Forest-Model.md).  
  
Sie müssen auch die Firewall genug zum Zulassen von Active Directory-Datenverkehr passieren zu öffnen. Weitere Informationen zum Konfigurieren von Firewalls für die Verwendung mit AD DS finden Sie unter Active Directory in Netzwerken durch Firewalls segmentiert ([https://go.microsoft.com/fwlink/?LinkId=37928](https://go.microsoft.com/fwlink/?LinkId=37928)).  
  
## <a name="BKMK_7"></a>Szenario 7: Ressourcengesamtstruktur verwenden und Konfigurieren der Firewalls für die Dienstisolation mit eingeschränkter Konnektivität  
Wenn eingeschränkter Konnektivität ein Problem ist, und Sie eine Anforderung für die Dienstisolation haben, können Sie Folgendes tun:  
  
-   Verwenden Sie eine Organisationseinheit Gesamtstruktur. Platzieren Sie die Benutzer, Gruppen und Computer für die Gruppe, die Isolation von Diensten in einer separaten Organisationseinheit Gesamtstruktur erforderlich sind. Weisen Sie eine Person aus der Gruppe die Gesamtstrukturbesitzer sein. Die Organisationseinheit Gesamtstruktur bietet eine separate Umgebung auf der anderen Seite der Firewall. Die Gesamtstruktur enthält Benutzerkonten und Ressourcen, die innerhalb der Gesamtstruktur verwaltet werden, sodass Benutzer nicht benötigen, um durch die Firewall ihren täglichen Aufgaben zu wechseln. Bestimmte Benutzer oder Anwendungen möglicherweise spezielle Anforderungen, die die Möglichkeit, durch die Firewall an anderen Gesamtstrukturen übergeben müssen. Sie können diese Anforderungen einzeln erfüllen, öffnen Sie die entsprechenden Schnittstellen in der Firewall, einschließlich derer, die für alle Vertrauensstellungen, um die Funktion erforderlich.  
  
-   Verwenden Sie eine Ressourcen-Gesamtstruktur. Direkte Ressourcen und Dienstkonten in einer separaten Ressourcen-Gesamtstruktur, damit Benutzerkonten in einer vorhandenen Gesamtstruktur für die Organisationseinheit. Es ist möglicherweise erforderlich, erstellen einige Alternativen Benutzerkonten in der Ressourcengesamtstruktur Zugriff auf die Ressourcen-Gesamtstruktur beibehalten, wenn die Organisation Gesamtstruktur nicht mehr verfügbar ist. Die alternativen Konten benötigen die erforderliche Autorität zur Anmeldung an der Ressourcengesamtstruktur und Kontrolle über die Ressourcen warten, bis die Organisationseinheit Gesamtstruktur wieder online ist.  
  
    Richten Sie eine Vertrauensstellung zwischen der Ressource und Organisations-Gesamtstrukturen, sodass der Benutzer auf die Ressourcen in der Gesamtstruktur zugreifen können, bei der Verwendung von ihren normalen Benutzerkonten. Diese Konfiguration ermöglicht die zentralisierte Verwaltung von Benutzerkonten während Benutzer alternative Konten in der Ressourcengesamtstruktur zurückgegriffen, wenn die Organisation Gesamtstruktur nicht mehr verfügbar ist.  
  
Die folgenden: Überlegungen zur Dienstisolation  
  
-   Für Dienstisolation erstellten Gesamtstrukturen können Domänen aus anderen Gesamtstrukturen vertrauen, jedoch dürfen keine Benutzer aus anderen Gesamtstrukturen in ihren Dienst Administratorgruppen enthalten. Wenn Benutzer aus anderen Gesamtstrukturen in administrativen Gruppen in der isolierten Gesamtstruktur enthalten sind, kann die Sicherheit der isolierten Gesamtstruktur möglicherweise gefährdet, da die Dienstadministratoren in der Gesamtstruktur nicht exklusive Steuerung verfügen.  
  
-   Als Domänencontroller in einem Netzwerk zugänglich sind, sind sie Angriffen (z. B. Denial-of-Service-Angriffe) von Computern in diesem Netzwerk. Sie können zum Schutz gegen die Möglichkeit eines Angriffs die folgenden Schritte ausführen:  
  
    -   Hosten von Domänencontrollern nur auf Netzwerke, die als sicher eingestuft werden.  
  
    -   Beschränken Sie den Zugriff auf Netzwerke, die der Domänencontroller hostet.  
  
-   Dienstisolation ist die Erstellung einer zusätzlichen Gesamtstruktur erforderlich. Bewerten Sie, ob die Kosten für die Verwaltung der Infrastruktur zur Unterstützung der zusätzlichen Gesamtstruktur die Kosten im Zusammenhang mit der Zugriff auf Ressourcen aufgrund einer Organisationseinheit Gesamtstruktur nicht verfügbar ist aufwiegt.  
  
    Bestimmte Benutzer oder Anwendungen möglicherweise spezielle Anforderungen, die die Möglichkeit, durch die Firewall an anderen Gesamtstrukturen übergeben müssen. Sie können diese Anforderungen einzeln erfüllen, öffnen Sie die entsprechenden Schnittstellen in der Firewall, einschließlich derer, die für alle Vertrauensstellungen, um die Funktion erforderlich.  
  
Weitere Informationen zum Konfigurieren von Firewalls für die Verwendung mit AD DS finden Sie unter Active Directory in Netzwerken durch Firewalls segmentiert ([https://go.microsoft.com/fwlink/?LinkId=37928](https://go.microsoft.com/fwlink/?LinkId=37928)).  
  



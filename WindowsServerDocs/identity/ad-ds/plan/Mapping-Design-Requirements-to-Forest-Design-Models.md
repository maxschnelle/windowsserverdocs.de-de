---
ms.assetid: c0d64566-5530-482e-a332-af029a5fb575
title: Zuordnung von Entwurfs Anforderungen zu Gesamtstruktur-Entwurfs Modellen
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 2a389b00fbf983a24b745431fee98a760f0fc756
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86963562"
---
# <a name="mapping-design-requirements-to-forest-design-models"></a>Zuordnung von Entwurfs Anforderungen zu Gesamtstruktur-Entwurfs Modellen

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die meisten Gruppen in Ihrer Organisation können eine einzelne Organisations Gesamtstruktur gemeinsam nutzen, die von einer einzelnen IT-Gruppe verwaltet wird und die Benutzerkonten und Ressourcen für alle Gruppen enthält, die die Gesamtstruktur gemeinsam verwenden. Diese freigegebene Gesamtstruktur, die als anfängliche Organisations Gesamtstruktur bezeichnet wird, ist die Grundlage des Gesamtstruktur-Entwurfs Modells für die Organisation.

Da die anfängliche Organisations Gesamtstruktur mehrere Gruppen in der Organisation hosten kann, muss der Gesamtstruktur Besitzer Vereinbarungen zum Service Level für jede Gruppe einrichten, damit alle Parteien verstehen, was erwartet wird. Dadurch werden sowohl die einzelnen Gruppen als auch der Gesamtstruktur Besitzer durch die Einrichtung vereinbarter Dienst Erwartungen geschützt.

Wenn nicht alle Gruppen in Ihrer Organisation eine einzelne Organisations Gesamtstruktur gemeinsam nutzen können, müssen Sie den Gesamtstruktur Entwurf erweitern, um den Anforderungen der unterschiedlichen Gruppen gerecht zu werden. Dies umfasst die Identifizierung der Entwurfs Anforderungen, die für die Gruppen gelten, basierend auf Ihren Anforderungen an Autonomie und Isolation und ob Sie über ein Netzwerk mit eingeschränkter Konnektivität verfügen. Anschließend wird das Gesamtstruktur Modell identifiziert, das Sie zum erfüllen dieser Anforderungen verwenden können. In der folgenden Tabelle werden die Szenarien für das Gesamtstruktur-Entwurfs Modell basierend auf den Faktoren Autonomie, Isolation und Konnektivität aufgelistet. Nachdem Sie das Gesamtstruktur-Entwurfs Szenario identifiziert haben, das Ihren Anforderungen am besten entspricht, stellen Sie fest, ob Sie zusätzliche Entscheidungen treffen müssen, um die Entwurfs Spezifikationen zu erfüllen.

> [!NOTE]
> Wenn ein Faktor als "N/v" aufgeführt ist, wird er nicht berücksichtigt, da andere Anforderungen auch diesen Faktor berücksichtigen.

|Szenario|Eingeschränkte Konnektivität|Datenisolation|Daten Autonomie|Dienst Isolation|Dienst Autonomie|
|------------|------------------------|------------------|-----------------|---------------------|--------------------|
|[Szenario 1: beitreten zu einer vorhandenen Gesamtstruktur für die Daten Autonomie](#BKMK_1)|Nein|Nein |Ja|Nein|Nein |
|[Szenario 2: Verwenden einer Organisations Gesamtstruktur oder Domäne für die Dienst Autonomie](#BKMK_2)|Nein|Nein |–|Nein|Ja|
|[Szenario 3: Verwenden einer Organisations-oder Ressourcen Gesamtstruktur für die Dienst Isolation](#BKMK_3)|Nein|Nein |–|Ja|N/V|
|[Szenario 4: Verwenden einer Gesamtstruktur der Organisation oder eines eingeschränkten Zugriffs für die Daten Isolation](#BKMK_4)|–|Ja|N/V|Nicht zutreffend|Nicht zutreffend|
|[Szenario 5: Verwenden einer Organisations Gesamtstruktur oder Neukonfigurieren der Firewall für eingeschränkte Konnektivität](#BKMK_5)|Ja|Nein|–|Nein|Nein |
|[Szenario 6: Verwenden einer Organisations Gesamtstruktur oder Domäne und Neukonfigurieren der Firewall für Dienst Autonomie mit eingeschränkter Konnektivität](#BKMK_6)|Ja|Nein|–|Nein|Ja|
|[Szenario 7: Verwenden einer Ressourcen Gesamtstruktur und Neukonfigurieren der Firewall für die Dienst Isolation mit eingeschränkter Konnektivität](#BKMK_7)|Ja|Nein|–|Ja|N/V|

## <a name="scenario-1-join-an-existing-forest-for-data-autonomy"></a><a name="BKMK_1"></a>Szenario 1: beitreten zu einer vorhandenen Gesamtstruktur für die Daten Autonomie

Sie können eine Anforderung für die Daten Autonomie erfüllen, indem Sie die Gruppe einfach in Organisationseinheiten (OUs) in einer vorhandenen Organisations Gesamtstruktur durchsuchen. Delegieren Sie die Steuerung der Organisationseinheiten an Daten Administratoren aus dieser Gruppe, um die Daten Autonomie zu erreichen. Weitere Informationen zur Delegierung der Steuerung mithilfe von Organisationseinheiten finden Sie unter [Erstellen eines Entwurfs einer Organisationseinheit](../../ad-ds/plan/Creating-an-Organizational-Unit-Design.md).

## <a name="scenario-2-use-an-organizational-forest-or-domain-for-service-autonomy"></a><a name="BKMK_2"></a>Szenario 2: Verwenden einer Organisations Gesamtstruktur oder Domäne für die Dienst Autonomie

Wenn eine Gruppe in Ihrer Organisation die Dienst Autonomie als Anforderung identifiziert, empfiehlt es sich, diese Anforderung zunächst zu überdenken. Das erreichen von Dienst Autonomie führt zu mehr Verwaltungsaufwand und zusätzlichen Kosten für die Organisation. Stellen Sie sicher, dass die Voraussetzung für die Dienst Autonomie nicht einfach ist, und dass Sie die Kosten für die Erfüllung dieser Anforderung rechtfertigen können.

Sie können eine Anforderung für die Dienst Autonomie erfüllen, indem Sie eine der folgenden Aktionen ausführen:

- Erstellen einer Organisations Gesamtstruktur. Platzieren Sie die Benutzer, Gruppen und Computer für die Gruppe, die eine Dienst Autonomie erfordert, in eine separate Organisations Gesamtstruktur. Weisen Sie eine Person aus dieser Gruppe als Gesamtstruktur Besitzer zu. Wenn die Gruppe auf Ressourcen mit anderen Gesamtstrukturen in der Organisation zugreifen oder diese freigeben muss, können Sie eine Vertrauensstellung zwischen Ihrer Organisations Gesamtstruktur und den anderen Gesamtstrukturen einrichten.

- Verwenden von Organisations Domänen. Platzieren Sie die Benutzer, Gruppen und Computer in einer separaten Domäne in einer vorhandenen Organisations Gesamtstruktur. Dieses Modell bietet nur Dienst Autonomie auf Domänen Ebene und nicht für vollständige Dienst Autonomie, Dienst Isolation oder Daten Isolation.

Weitere Informationen zum Verwenden von Organisations Domänen finden Sie unter [Verwenden des Domänen](../../ad-ds/plan/../../ad-ds/plan/Using-the-Organizational-Domain-Forest-Model.md)Gesamtstruktur Modells.

## <a name="scenario-3-use-an-organizational-forest-or-resource-forest-for-service-isolation"></a><a name="BKMK_3"></a>Szenario 3: Verwenden einer Organisations-oder Ressourcen Gesamtstruktur für die Dienst Isolation

Sie können eine Anforderung für die Dienst Isolation erfüllen, indem Sie eine der folgenden Aktionen ausführen:

- Verwenden einer Organisations Gesamtstruktur. Platzieren Sie die Benutzer, Gruppen und Computer für die Gruppe, die eine Dienst Isolation erfordert, in eine separate Organisations Gesamtstruktur. Weisen Sie eine Person aus dieser Gruppe als Gesamtstruktur Besitzer zu. Wenn die Gruppe auf Ressourcen mit anderen Gesamtstrukturen in der Organisation zugreifen oder diese freigeben muss, können Sie eine Vertrauensstellung zwischen Ihrer Organisations Gesamtstruktur und den anderen Gesamtstrukturen einrichten. Diese Vorgehensweise wird jedoch nicht empfohlen, da der Ressourcen Zugriff über universelle Gruppen in den Gesamtstruktur-Vertrauensstellungs Szenarien stark eingeschränkt ist.

- Verwenden einer Ressourcen Gesamtstruktur. Platzieren Sie Ressourcen und Dienst Konten in einer separaten Ressourcen Gesamtstruktur, und behalten Sie die Benutzerkonten in einer vorhandenen Organisations Gesamtstruktur bei. Gegebenenfalls können Alternative Konten in der Ressourcen Gesamtstruktur erstellt werden, um auf Ressourcen in der Ressourcen Gesamtstruktur zuzugreifen, wenn die Organisations Gesamtstruktur nicht verfügbar ist. Die alternativen Konten müssen über die Autorität verfügen, die zur Anmeldung bei der Ressourcen Gesamtstruktur erforderlich ist, und die Kontrolle über die Ressourcen behalten, bis die Organisations Gesamtstruktur wieder online ist.

   Richten Sie eine Vertrauensstellung zwischen der Ressourcen-und der Organisations Gesamtstruktur ein, damit die Benutzer auf die Ressourcen in der Gesamtstruktur zugreifen können, während Sie Ihre regulären Benutzerkonten verwenden. Diese Konfiguration ermöglicht die zentralisierte Verwaltung von Benutzerkonten, während Benutzer gleichzeitig auf Alternative Konten in der Ressourcen Gesamtstruktur zurückgreifen können, wenn die Organisations Gesamtstruktur nicht verfügbar ist.

Zu den Überlegungen zur Dienst Isolation zählen die folgenden:

- Gesamtstrukturen, die für die Dienst Isolation erstellt werden, können Domänen von anderen Gesamtstrukturen vertrauen, dürfen jedoch keine Benutzer aus anderen Gesamtstrukturen in ihren Dienst Administratoren Gruppen enthalten Wenn Benutzer aus anderen Gesamtstrukturen in administrative Gruppen in der isolierten Gesamtstruktur enthalten sind, kann die Sicherheit der isolierten Gesamtstruktur potenziell beeinträchtigt werden, da die Dienst Administratoren in der Gesamtstruktur nicht über exklusive Kontrolle verfügen.

- Solange auf die Domänen Controller in einem Netzwerk zugegriffen werden kann, unterliegen Sie Angriffen (z. b. Denial-of-Service-Angriffe) von Schadsoftware in diesem Netzwerk. Sie können wie folgt vorgehen, um die Möglichkeit eines Angriffs zu schützen:

   - Host Domänen Controller nur in Netzwerken, die als sicher eingestuft werden.

   - Beschränken Sie den Zugriff auf das Netzwerk, in dem die Domänen Controller gehostet werden.

- Die Dienst Isolation erfordert die Erstellung einer zusätzlichen Gesamtstruktur. Evaluieren Sie, ob die Kosten für die Verwaltung der Infrastruktur zur Unterstützung der zusätzlichen Gesamtstruktur die Kosten für den Verlust des Zugriffs auf Ressourcen überwiegen, weil eine Organisations Gesamtstruktur nicht verfügbar ist.

## <a name="scenario-4-use-an-organizational-forest-or-restricted-access-forest-for-data-isolation"></a><a name="BKMK_4"></a>Szenario 4: Verwenden einer Gesamtstruktur der Organisation oder eines eingeschränkten Zugriffs für die Daten Isolation

Sie können eine Daten Isolation erzielen, indem Sie eine der folgenden Aktionen ausführen:

- Verwenden einer Organisations Gesamtstruktur. Platzieren Sie die Benutzer, Gruppen und Computer für die Gruppe, für die die Daten Isolation erforderlich ist, in einer separaten Organisations Gesamtstruktur. Weisen Sie eine Person aus dieser Gruppe als Gesamtstruktur Besitzer zu. Wenn die Gruppe auf Ressourcen mit anderen Gesamtstrukturen in der Organisation zugreifen oder diese freigeben muss, richten Sie eine Vertrauensstellung zwischen der Organisations Gesamtstruktur und den anderen Gesamtstrukturen ein. Nur die Benutzer, die Zugriff auf die klassifizierten Informationen benötigen, sind in der neuen Organisations Gesamtstruktur vorhanden. Benutzer verfügen über ein Konto, mit dem Sie sowohl auf klassifizierte Daten in ihrer eigenen Gesamtstruktur als auch auf nicht klassifizierte Daten in anderen Gesamtstrukturen mithilfe von Vertrauens Stellungen zugreifen können.

- Verwenden einer Gesamtstruktur mit eingeschränktem Zugriff. Dabei handelt es sich um eine separate Gesamtstruktur, die die eingeschränkten Daten und die Benutzerkonten enthält, die für den Zugriff auf diese Daten verwendet werden. Separate Benutzerkonten werden in den vorhandenen Organisationsstrukturen verwaltet, die für den Zugriff auf die uneingeschränkten Ressourcen im Netzwerk verwendet werden. Zwischen der Gesamtstruktur mit eingeschränktem Zugriff und anderen Gesamtstrukturen im Unternehmen werden keine Vertrauens Stellungen erstellt. Sie können die Gesamtstruktur weiter einschränken, indem Sie die Gesamtstruktur in einem separaten physischen Netzwerk bereitstellen, sodass keine Verbindung mit anderen Gesamtstrukturen hergestellt werden kann. Wenn Sie die Gesamtstruktur in einem separaten Netzwerk bereitstellen, müssen die Benutzer über zwei Arbeitsstationen verfügen: eine für den Zugriff auf die eingeschränkte Gesamtstruktur und eine für den Zugriff auf die nicht eingeschränkten Bereiche des Netzwerks.

Überlegungen zum Erstellen von Gesamtstrukturen für die Daten Isolation:

- Organisationsstrukturen, die für die Daten Isolation erstellt werden, können Domänen aus anderen Gesamtstrukturen vertrauen, aber Benutzer aus anderen Gesamtstrukturen dürfen nicht in Folgendes eingeschlossen werden:

  - Gruppen, die für die Dienst Verwaltung oder Gruppen verantwortlich sind, die die Mitgliedschaft von Dienst Administrator Gruppen verwalten können

  - Gruppen mit administrativer Kontrolle über Computer, auf denen geschützte Daten gespeichert sind

  - Gruppen, die Zugriff auf geschützte Daten oder Gruppen haben, die für die Verwaltung von Benutzer Objekten oder Gruppen Objekten zuständig sind, die Zugriff auf geschützte Daten haben

    Wenn Benutzer aus einer anderen Gesamtstruktur in einer dieser Gruppen enthalten sind, kann eine Gefährdung der anderen Gesamtstruktur zu einer Kompromittierung der isolierten Gesamtstruktur und der Offenlegung geschützter Daten führen.

- Andere Gesamtstrukturen können so konfiguriert werden, dass Sie der für die Daten Isolation erstellten Organisations Gesamtstruktur vertrauen, sodass Benutzer in der isolierten Gesamtstruktur auf Ressourcen in anderen Gesamtstrukturen zugreifen können. Benutzer aus der isolierten Gesamtstruktur dürfen sich jedoch nie interaktiv bei Arbeitsstationen in der vertrauenden Gesamtstruktur anmelden. Der Computer in der vertrauenden Gesamtstruktur kann potenziell durch Schadsoftware kompromittiert werden und kann verwendet werden, um die Anmelde Informationen des Benutzers zu erfassen.

   > [!NOTE]
   > Um zu verhindern, dass Server in einer vertrauenden Gesamtstruktur die Identität von Benutzern aus der isolierten Gesamtstruktur annehmen und dann auf Ressourcen in der isolierten Gesamtstruktur zugreifen, kann der Gesamtstruktur Besitzer die delegierte Authentifizierung deaktivieren oder das Feature der eingeschränkten Delegierung verwenden. Weitere Informationen zur delegierten Authentifizierung und zur eingeschränkten [Delegierung](/previous-versions/windows/it-pro/windows-server-2003/cc739740(v=ws.10))finden Sie unter Delegieren der Authentifizierung.

- Möglicherweise müssen Sie eine Firewall zwischen der Organisations Gesamtstruktur und den anderen Gesamtstrukturen in der Organisation einrichten, um den Benutzer Zugriff auf Informationen außerhalb Ihrer Gesamtstruktur zu beschränken.

- Obwohl das Erstellen einer separaten Gesamtstruktur die Daten Isolation ermöglicht, werden die Domänen Controller in der isolierten Gesamtstruktur und die Computer, auf denen geschützte Informationen gehostet werden, in einem Netzwerk zugänglich sein, und Sie unterliegen Angriffen, die von Computern in diesem Netzwerk gestartet werden. Organisationen, die entscheiden, dass das Risiko eines Angriffs zu hoch ist oder dass die Folge eines Angriffs oder der Sicherheitsverletzung zu groß ist, muss den Zugriff auf das Netzwerk oder die Netzwerke beschränken, die die Domänen Controller und die Computer, auf denen die geschützten Daten gehostet werden, unterliegen. Das Einschränken des Zugriffs kann mithilfe von Technologien wie Firewalls und Internet Protokoll Sicherheit (IPSec) erfolgen. In Extremfällen können Organisationen die geschützten Daten in einem unabhängigen Netzwerk aufbewahren, das über keine physische Verbindung mit einem anderen Netzwerk in der Organisation verfügt.

   > [!NOTE]
   > Wenn eine Netzwerkverbindung zwischen einer eingeschränkten Zugriffs Gesamtstruktur und einem anderen Netzwerk besteht, besteht die Möglichkeit, dass Daten im eingeschränkten Bereich an das andere Netzwerk übertragen werden.

## <a name="scenario-5-use-an-organizational-forest-or-reconfigure-the-firewall-for-limited-connectivity"></a><a name="BKMK_5"></a>Szenario 5: Verwenden einer Organisations Gesamtstruktur oder Neukonfigurieren der Firewall für eingeschränkte Konnektivität

Zum erfüllen einer begrenzten Verbindungsanforderung können Sie eine der folgenden Aktionen ausführen:

- Versetzen Sie Benutzer in eine vorhandene Organisations Gesamtstruktur, und öffnen Sie dann die Firewall so, dass Active Directory Datenverkehr durchlaufen werden kann.

- Verwenden Sie eine Organisations Gesamtstruktur. Platzieren Sie die Benutzer, Gruppen und Computer für die Gruppe, für die die Konnektivität auf eine separate Organisations Gesamtstruktur beschränkt ist. Weisen Sie eine Person aus dieser Gruppe als Gesamtstruktur Besitzer zu. Die Organisations Gesamtstruktur bietet eine separate Umgebung auf der anderen Seite der Firewall. Die Gesamtstruktur umfasst Benutzerkonten und Ressourcen, die innerhalb der Gesamtstruktur verwaltet werden, sodass Benutzer die Firewall nicht durchlaufen müssen, um Ihre täglichen Aufgaben auszuführen. Bestimmte Benutzer oder Anwendungen haben möglicherweise besondere Anforderungen, die die Möglichkeit haben, die Firewall zu durchlaufen, um andere Gesamtstrukturen zu kontaktieren. Sie können diese Anforderungen einzeln erfüllen, indem Sie die entsprechenden Schnittstellen in der Firewall öffnen, einschließlich derjenigen, die erforderlich sind, damit alle Vertrauens Stellungen funktionieren.

Weitere Informationen zum Konfigurieren von Firewalls für die Verwendung mit Active Directory Domain Services (AD DS) finden Sie unter [Active Directory in Netzwerken, die durch Firewalls segmentiert](https://go.microsoft.com/fwlink/?LinkId=37928)sind.

## <a name="scenario-6-use-an-organizational-forest-or-domain-and-reconfigure-the-firewall-for-service-autonomy-with-limited-connectivity"></a><a name="BKMK_6"></a>Szenario 6: Verwenden einer Organisations Gesamtstruktur oder Domäne und Neukonfigurieren der Firewall für Dienst Autonomie mit eingeschränkter Konnektivität

Wenn eine Gruppe in Ihrer Organisation die Dienst Autonomie als Anforderung identifiziert, empfiehlt es sich, diese Anforderung zunächst zu überdenken. Das erreichen von Dienst Autonomie führt zu mehr Verwaltungsaufwand und zusätzlichen Kosten für die Organisation. Stellen Sie sicher, dass die Voraussetzung für die Dienst Autonomie nicht einfach ist, und dass Sie die Kosten für die Erfüllung dieser Anforderung rechtfertigen können.

Wenn eine begrenzte Konnektivität ein Problem ist und Sie eine Anforderung für die Dienst Autonomie haben, können Sie eine der folgenden Aktionen ausführen:

- Verwenden Sie eine Organisations Gesamtstruktur. Platzieren Sie die Benutzer, Gruppen und Computer für die Gruppe, die eine Dienst Autonomie erfordert, in eine separate Organisations Gesamtstruktur. Weisen Sie eine Person aus dieser Gruppe als Gesamtstruktur Besitzer zu. Die Organisations Gesamtstruktur bietet eine separate Umgebung auf der anderen Seite der Firewall. Die Gesamtstruktur umfasst Benutzerkonten und Ressourcen, die innerhalb der Gesamtstruktur verwaltet werden, sodass Benutzer die Firewall nicht durchlaufen müssen, um Ihre täglichen Aufgaben auszuführen. Bestimmte Benutzer oder Anwendungen haben möglicherweise besondere Anforderungen, die die Möglichkeit haben, die Firewall zu durchlaufen, um andere Gesamtstrukturen zu kontaktieren. Sie können diese Anforderungen einzeln erfüllen, indem Sie die entsprechenden Schnittstellen in der Firewall öffnen, einschließlich derjenigen, die erforderlich sind, damit alle Vertrauens Stellungen funktionieren.

- Platzieren Sie die Benutzer, Gruppen und Computer in einer separaten Domäne in einer vorhandenen Organisations Gesamtstruktur. Dieses Modell bietet nur Dienst Autonomie auf Domänen Ebene und nicht für vollständige Dienst Autonomie, Dienst Isolation oder Daten Isolation. Andere Gruppen in der Gesamtstruktur müssen den Dienst Administratoren der neuen Domäne denselben Grad Vertrauen, als Sie dem Gesamtstruktur Besitzer Vertrauen. Aus diesem Grund wird diese Vorgehensweise nicht empfohlen. Weitere Informationen zum Verwenden von Organisations Domänen finden Sie unter [Verwenden des Domänen](../../ad-ds/plan/../../ad-ds/plan/Using-the-Organizational-Domain-Forest-Model.md)Gesamtstruktur Modells.

Außerdem müssen Sie die Firewall so öffnen, dass die Active Directory Datenverkehr durchlaufen werden kann. Weitere Informationen zum Konfigurieren von Firewalls für die Verwendung mit AD DS finden Sie unter [Active Directory in Netzwerken, die durch Firewalls segmentiert](https://go.microsoft.com/fwlink/?LinkId=37928)sind.

## <a name="scenario-7-use-a-resource-forest-and-reconfigure-the-firewall-for-service-isolation-with-limited-connectivity"></a><a name="BKMK_7"></a>Szenario 7: Verwenden einer Ressourcen Gesamtstruktur und Neukonfigurieren der Firewall für die Dienst Isolation mit eingeschränkter Konnektivität

Wenn eine begrenzte Konnektivität ein Problem ist und Sie eine Anforderung für die Dienst Isolation haben, können Sie eine der folgenden Aktionen ausführen:

- Verwenden Sie eine Organisations Gesamtstruktur. Platzieren Sie die Benutzer, Gruppen und Computer für die Gruppe, die eine Dienst Isolation erfordert, in eine separate Organisations Gesamtstruktur. Weisen Sie eine Person aus dieser Gruppe als Gesamtstruktur Besitzer zu. Die Organisations Gesamtstruktur bietet eine separate Umgebung auf der anderen Seite der Firewall. Die Gesamtstruktur umfasst Benutzerkonten und Ressourcen, die innerhalb der Gesamtstruktur verwaltet werden, sodass Benutzer die Firewall nicht durchlaufen müssen, um Ihre täglichen Aufgaben auszuführen. Bestimmte Benutzer oder Anwendungen haben möglicherweise besondere Anforderungen, die die Möglichkeit haben, die Firewall zu durchlaufen, um andere Gesamtstrukturen zu kontaktieren. Sie können diese Anforderungen einzeln erfüllen, indem Sie die entsprechenden Schnittstellen in der Firewall öffnen, einschließlich derjenigen, die erforderlich sind, damit alle Vertrauens Stellungen funktionieren.

- Verwenden Sie eine Ressourcen Gesamtstruktur. Platzieren Sie Ressourcen und Dienst Konten in einer separaten Ressourcen Gesamtstruktur, und behalten Sie die Benutzerkonten in einer vorhandenen Organisations Gesamtstruktur bei. Es kann erforderlich sein, einige alternative Benutzerkonten in der Ressourcen Gesamtstruktur zu erstellen, um den Zugriff auf die Ressourcen Gesamtstruktur aufrechtzuerhalten, wenn die Organisations Gesamtstruktur nicht verfügbar ist. Die alternativen Konten müssen über die Autorität verfügen, die zur Anmeldung bei der Ressourcen Gesamtstruktur erforderlich ist, und die Kontrolle über die Ressourcen behalten, bis die Organisations Gesamtstruktur wieder online ist.

   Richten Sie eine Vertrauensstellung zwischen der Ressourcen-und der Organisations Gesamtstruktur ein, damit die Benutzer auf die Ressourcen in der Gesamtstruktur zugreifen können, während Sie Ihre regulären Benutzerkonten verwenden. Diese Konfiguration ermöglicht die zentralisierte Verwaltung von Benutzerkonten, während Benutzer gleichzeitig auf Alternative Konten in der Ressourcen Gesamtstruktur zurückgreifen können, wenn die Organisations Gesamtstruktur nicht verfügbar ist.

Zu den Überlegungen zur Dienst Isolation zählen die folgenden:

- Gesamtstrukturen, die für die Dienst Isolation erstellt werden, können Domänen von anderen Gesamtstrukturen vertrauen, dürfen jedoch keine Benutzer aus anderen Gesamtstrukturen in ihren Dienst Administratoren Gruppen enthalten Wenn Benutzer aus anderen Gesamtstrukturen in administrative Gruppen in der isolierten Gesamtstruktur enthalten sind, kann die Sicherheit der isolierten Gesamtstruktur potenziell beeinträchtigt werden, da die Dienst Administratoren in der Gesamtstruktur nicht über exklusive Kontrolle verfügen.

- Solange auf die Domänen Controller in einem Netzwerk zugegriffen werden kann, können Sie von Computern in diesem Netzwerk auf Angriffe (z. b. Denial-of-Service-Angriffe) zugreifen. Sie können wie folgt vorgehen, um die Möglichkeit eines Angriffs zu schützen:

   - Host Domänen Controller nur in Netzwerken, die als sicher eingestuft werden.

   - Beschränken Sie den Zugriff auf das Netzwerk, in dem die Domänen Controller gehostet werden.

- Die Dienst Isolation erfordert die Erstellung einer zusätzlichen Gesamtstruktur. Evaluieren Sie, ob die Kosten für die Verwaltung der Infrastruktur zur Unterstützung der zusätzlichen Gesamtstruktur die Kosten für den Verlust des Zugriffs auf Ressourcen überwiegen, weil eine Organisations Gesamtstruktur nicht verfügbar ist.

   Bestimmte Benutzer oder Anwendungen haben möglicherweise besondere Anforderungen, die die Möglichkeit haben, die Firewall zu durchlaufen, um andere Gesamtstrukturen zu kontaktieren. Sie können diese Anforderungen einzeln erfüllen, indem Sie die entsprechenden Schnittstellen in der Firewall öffnen, einschließlich derjenigen, die erforderlich sind, damit alle Vertrauens Stellungen funktionieren.

Weitere Informationen zum Konfigurieren von Firewalls für die Verwendung mit AD DS finden Sie unter [Active Directory in Netzwerken, die durch Firewalls segmentiert](https://go.microsoft.com/fwlink/?LinkId=37928)sind.

---
ms.assetid: c0d64566-5530-482e-a332-af029a5fb575
title: Zuordnen von Entwurfsanforderungen zu Gesamtstruktur-Entwurfsmodelle
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 35d6322f053c7a02dc1df5430b28f771f57a1ad7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442571"
---
# <a name="mapping-design-requirements-to-forest-design-models"></a>Zuordnen von Entwurfsanforderungen zu Gesamtstruktur-Entwurfsmodelle

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Die meisten Gruppen in Ihrer Organisation können eine Gesamtstruktur für die Organisation freigeben, die von einer einzelnen Gruppe Informationstechnologie (IT) verwaltet wird und enthält die Benutzer- und Ressourcen für alle Gruppen, die die Gesamtstruktur gemeinsam nutzen. Diese freigegebenen Gesamtstruktur, mit dem Namen der ersten Organisationsgesamtstruktur, ist die Grundlage für die Gesamtstruktur-Entwurfsmodell für die Organisation.  

Da der anfängliche Organisationsgesamtstruktur mehrere Gruppen in der Organisation gehostet werden kann, muss der Gesamtstrukturbesitzer Vereinbarungen zum Servicelevel mit jeder Gruppe herstellen, so, dass alle Parteien verstehen, was von ihnen erwartet wird. Dies schützt sowohl für die einzelnen Gruppen als auch für den Gesamtstrukturbesitzer, durch die Einrichtung von Erwartungen an die vereinbarten-Dienst.  

Wenn nicht alle Gruppen in Ihrer Organisation können eine einzelne Gesamtstruktur für die Organisation freigeben, erweitern Sie Ihren Gesamtstrukturentwurf, um die Anforderungen der verschiedenen Gruppen zu berücksichtigen. Dies umfasst Identifizieren der Designanforderungen, die angewendet werden, die Gruppen auf Grundlage seiner Anforderungen für die Autonomie und Isolation und davon, ob sie über ein Netzwerk begrenzt-Konnektivität verfügen, und anschließend ermitteln das Forest-Modell, das Sie verwenden können, um diese zu berücksichtigen. Anforderungen an. Die folgende Tabelle enthält die Gesamtstruktur Modell Entwurfsszenarien basierend auf der Autonomie, Isolation und Konnektivität Faktoren. Nachdem Sie das Szenario der Gesamtstruktur-Entwurf, das Ihren Anforderungen am besten entspricht identifiziert, bestimmen Sie, ob für jede weitere Entscheidungen Spezifikationen für den Entwurf zu erfüllen müssen.  

> [!NOTE]  
> Wenn ein Faktor als n/v aufgeführt ist, ist es nicht berücksichtigt, da andere Anforderungen auch dieses Faktors aufnehmen.  

|Szenario|Eingeschränkte Konnektivität|Datenisolation|Datenautonomie|Isolation von Diensten|Die Autonomie eines Dienstes|  
|------------|------------------------|------------------|-----------------|---------------------|--------------------|  
|[Szenario 1: Verknüpfen einer vorhandenen Gesamtstruktur für die Datenautonomie](#BKMK_1)|Nein|Nein|Ja|Nein|Nein|  
|[Szenario 2: Verwenden von einer Organisation Gesamtstruktur oder Domäne für die Autonomie eines Dienstes](#BKMK_2)|Nein|Nein|Nicht zutreffend|Nein|Ja|  
|[Szenario: 3: Verwenden Sie Organisationsgesamtstruktur oder Ressourcen-Gesamtstruktur für die Isolation von Diensten.](#BKMK_3)|Nein|Nein|Nicht zutreffend|Ja|Nicht zutreffend|  
|[Szenario 4: Verwenden Sie eine Organisation Gesamtstruktur oder eine Gesamtstruktur mit eingeschränktem Zugriff für die Datenisolation](#BKMK_4)|Nicht zutreffend|Ja|Nicht zutreffend|Nicht zutreffend|Nicht zutreffend|  
|[Szenario 5: Verwenden Sie eine Organisationsgesamtstruktur, oder Konfigurieren der Firewalls für eingeschränkte Konnektivität](#BKMK_5)|Ja|Nein|Nicht zutreffend|Nein|Nein|  
|[Szenario 6: Verwenden einer Organisation Gesamtstruktur oder Domäne, und Konfigurieren der Firewalls für die Autonomie eines Dienstes mit eingeschränkter Konnektivität](#BKMK_6)|Ja|Nein|Nicht zutreffend|Nein|Ja|  
|[Szenario 7: Verwenden einer Ressourcengesamtstruktur und Konfigurieren der Firewalls für die Isolation von Diensten mit eingeschränkter Konnektivität](#BKMK_7)|Ja|Nein|Nicht zutreffend|Ja|Nicht zutreffend|  

## <a name="BKMK_1"></a>Szenario 1: Verknüpfen einer vorhandenen Gesamtstruktur für die Datenautonomie  

Sie können eine Voraussetzung für die Datenautonomie einfach durch das Hosten der Gruppe in Organisationseinheiten (OEs) in einer vorhandenen Gesamtstruktur für die Organisation erfüllen. Delegieren Sie Kontrolle über Organisationseinheiten für Datenadministratoren aus der Gruppe die Datenautonomie zu erreichen. Weitere Informationen zum Delegieren des Zugriffs mithilfe von Organisationseinheiten finden Sie unter [erstellen eine Organizational Unit Design](../../ad-ds/plan/Creating-an-Organizational-Unit-Design.md).  
  
## <a name="BKMK_2"></a>Szenario 2: Verwenden von einer Organisation Gesamtstruktur oder Domäne für die Autonomie eines Dienstes  

Wenn eine Gruppe in Ihrer Organisation die Autonomie eines Dienstes als Anforderung identifiziert, empfehlen wir, dass Sie zuerst diese Anforderung überdenken. Eine Dienstautonomie erstellt, mehr Verwaltungsaufwand und die zusätzlichen Kosten für die Organisation. Stellen Sie sicher, dass die Anforderung für die Autonomie eines Dienstes nicht einfach der Einfachheit halber ist und Sie die Kosten erfüllt diese Anforderung im Blocksatz ausrichten können.  
  
Sie können eine Anforderung für die Autonomie eines Dienstes erfüllen, indem Sie eine der folgenden:  

- Erstellen eine Organisationsgesamtstruktur. Platzieren Sie den Benutzer, Gruppen und Computer für die Gruppe, die die Autonomie eines Dienstes in einer separaten Organisation Gesamtstruktur erforderlich sind. Weisen Sie Einzelperson aus dieser Gruppe der Gesamtstrukturbesitzer sein. Wenn der Zugriff auf Ressourcen mit den anderen Gesamtstrukturen in der Organisation muss, können sie eine Vertrauensstellung zwischen ihrer Organisation Gesamtstruktur und den anderen Gesamtstrukturen einrichten.  

- Verwenden die Organisation Domänen. Platzieren Sie den Benutzer, Gruppen und Computer in einer separaten Domäne in einer vorhandenen Organisation Gesamtstruktur an. Dieses Modell ermöglicht nur die Autonomie eines Dienstes von auf Domänenebene und nicht für vollständige Dienstautonomie, der Isolation oder die Datenisolation-Diensts.  

Weitere Informationen zur Verwendung von organisatorischer Domänen finden Sie unter [mit dem Organisations-Gesamtstruktur Domänenmodell](../../ad-ds/plan/../../ad-ds/plan/Using-the-Organizational-Domain-Forest-Model.md).  

## <a name="BKMK_3"></a>Szenario 3: Verwenden Sie Organisationsgesamtstruktur oder Ressourcen-Gesamtstruktur für die Isolation von Diensten.  

Sie können eine Voraussetzung für die Isolation von Diensten erfüllen, indem Sie eine der folgenden:  

- Verwenden eine Organisationsgesamtstruktur. Platzieren Sie den Benutzer, Gruppen und Computer für die Gruppe, die Isolation von Diensten in einer separaten Organisation Gesamtstruktur erforderlich sind. Weisen Sie Einzelperson aus dieser Gruppe der Gesamtstrukturbesitzer sein. Wenn der Zugriff auf Ressourcen mit den anderen Gesamtstrukturen in der Organisation muss, können sie eine Vertrauensstellung zwischen ihrer Organisation Gesamtstruktur und den anderen Gesamtstrukturen einrichten. Allerdings empfehlen wir nicht diesen Ansatz, da Zugriff auf Ressourcen mithilfe von universellen Gruppen in Szenarien der Gesamtstruktur-Vertrauensstellung stark eingeschränkt ist.  

- Verwenden einer Ressourcengesamtstruktur. Platzieren Sie Ressourcen und Dienstkonten in separaten Ressourcengesamtstruktur-Benutzerkonten in einer vorhandenen Organisation Gesamtstruktur beibehalten. Bei Bedarf können alternative Konten erstellt werden, in der Ressourcengesamtstruktur zum Zugriff auf die Ressourcen in der Ressourcengesamtstruktur, wenn der Organisationsgesamtstruktur nicht verfügbar ist. Die alternativen Konten benötigen die erforderliche Autorität zur melden Sie sich bei der Ressourcen-Gesamtstruktur und die Kontrolle über die Ressourcen, bis der Organisationsgesamtstruktur wieder online ist.  

   Eine Vertrauensstellung zwischen der Ressource und Organisations-Gesamtstrukturen, damit die Benutzer auf die Ressourcen in der Gesamtstruktur zugreifen können, bei der Verwendung von ihren normalen Benutzerkonten. Diese Konfiguration ermöglicht die zentralisierte Verwaltung von Benutzerkonten während Benutzer auf alternative Konten in der Ressourcengesamtstruktur zurück, wenn der Organisationsgesamtstruktur nicht verfügbar ist.  

Die folgenden: Überlegungen zur Isolation von Diensten

- Gesamtstrukturen, die für die dienstisolierung kann Domänen aus anderen Gesamtstrukturen "vertrauen", jedoch dürfen keine Benutzer aus anderen Gesamtstrukturen in ihrer Administratoren Dienstgruppen erstellt werden. Wenn Benutzer aus anderen Gesamtstrukturen in der administrativen Gruppen in der isolierten Gesamtstruktur enthalten sind, kann die Sicherheit der isolierten Gesamtstruktur möglicherweise beeinträchtigt werden, da die Dienstadministratoren in der Gesamtstruktur keine exklusive Kontrolle.  

- Als Domänencontroller in einem Netzwerk zugegriffen werden kann, sind sie von Malware in diesem Netzwerk (z. B. Denial-of-Service-Angriffe). Zum Schutz gegen die Möglichkeit eines Angriffs Folgendes möglich:  

   - Host-Domänencontroller nur in Netzwerken, die als sicher eingestuft werden.  

   - Beschränken des Zugriffs auf Netzwerke, die der Domänencontroller gehostet werden.  

- Isolation von Diensten ist die Erstellung einer zusätzlichen Gesamtstruktur erforderlich. Bewerten Sie, ob die Kosten für die Verwaltung der Infrastruktur zur Unterstützung der Gesamtstruktur zusätzlichen Kosten im Zusammenhang mit Verlust des Zugriffs auf Ressourcen aufgrund einer Organisationsgesamtstruktur nicht verfügbar ist überwiegt.  

## <a name="BKMK_4"></a>Szenario 4: Verwenden Sie eine Organisation Gesamtstruktur oder eine Gesamtstruktur mit eingeschränktem Zugriff für die Datenisolation  

Sie können die Datenisolation erreichen, indem Sie eine der folgenden Aktionen ausführen:  

- Verwenden eine Organisationsgesamtstruktur. Platzieren Sie den Benutzer, Gruppen und Computer für die Gruppe, die Datenisolation in einer separaten Organisation Gesamtstruktur erforderlich sind. Weisen Sie Einzelperson aus dieser Gruppe der Gesamtstrukturbesitzer sein. Wenn die Gruppe Zugriff auf Ressourcen mit den anderen Gesamtstrukturen in der Organisation, eine Vertrauensstellung zwischen der Organisation und den anderen Gesamtstrukturen aufweist. Nur Benutzer, die Zugriff auf die vertraulichen Informationen benötigen, sind in der neuen Organisationsgesamtstruktur vorhanden. Benutzer haben ein Konto, mit denen sie den Zugriff auf beide klassifiziert Daten innerhalb ihrer eigenen Gesamtstruktur und nicht klassifizierte Daten in anderen Gesamtstrukturen mithilfe von Vertrauensstellungen.  

- Verwenden eine Gesamtstruktur mit eingeschränktem Zugriff. Dies ist eine separate Gesamtstruktur, die die Datentypen und die Benutzerkonten, die verwendet werden, Zugriff auf diese Daten enthält. Trennen Sie Benutzerkonten werden in den vorhandenen Gesamtstrukturen für die Organisationen verwaltet, die Zugriff auf den uneingeschränkten Ressourcen im Netzwerk verwendet werden. Keine Vertrauensstellungen werden zwischen der Gesamtstruktur mit eingeschränktem Zugriff und den anderen Gesamtstrukturen im Unternehmen erstellt. Sie können weitere die Gesamtstruktur einschränken, indem der Gesamtstruktur auf einem separaten physischen Netzwerk bereitstellen, damit anderen Gesamtstrukturen hergestellt werden kann. Wenn Sie die Gesamtstruktur in einem separaten Netzwerk bereitstellen, müssen Benutzer zwei Arbeitsstationen: eine für den Zugriff auf den eingeschränkten Gesamtstruktur und eine für den Zugriff auf die nonrestricted Bereiche des Netzwerks.  

Überlegungen zum Erstellen von Gesamtstrukturen für die Datenisolation umfassen Folgendes:  

- Organisation Gesamtstrukturen, die für die Datenisolation erstellten Domänen aus anderen Gesamtstrukturen vertrauen können, aber Benutzer aus anderen Gesamtstrukturen müssen nicht in eine der folgenden enthalten:  

  - Gruppen, die verantwortlich für dienstverwaltung oder Gruppen, die die Mitgliedschaft der Dienstadministrator-Gruppen verwalten können  

  - Gruppen, die administrativen Kontrolle über Computer verfügen, die geschützte Daten speichern  

  - Gruppen, die Zugriff auf geschützte Daten oder Gruppen, die sind dafür verantwortlich, für die Verwaltung von Benutzerobjekten oder Group-Objekte, die Zugriff auf, geschützte Daten  

    Wenn Benutzer aus einer anderen Gesamtstruktur in einer dieser Gruppen enthalten sind, kann eine Gefährdung der anderen Gesamtstruktur zu einer Gefährdung der isolierten Gesamtstruktur und Offenlegung der geschützten Daten führen.  

- Anderen Gesamtstrukturen können konfiguriert werden, um Vertrauen der Organisationsgesamtstruktur für die Datenisolation erstellt werden, sodass Benutzer in der isolierten Gesamtstruktur Ressourcen in anderen Gesamtstrukturen zugreifen können. Allerdings müssen Benutzer aus der isolierten Gesamtstruktur nicht interaktiv auf Arbeitsstationen in der vertrauenden Gesamtstruktur anmelden. Der Computer in der vertrauenden Gesamtstruktur kann möglicherweise durch böswillige Software beeinträchtigt werden und kann verwendet werden, um die Anmeldeinformationen des Benutzers zu erfassen.  

   > [!NOTE]
   > Der Gesamtstrukturbesitzer kann um Server in einer vertrauenden Gesamtstruktur Identität von Benutzern in der isolierten Gesamtstruktur, und klicken Sie dann den Zugriff auf Ressourcen in der isolierten Gesamtstruktur zu verhindern, dass delegierte Authentifizierung zu deaktivieren oder verwenden Sie das Feature für die eingeschränkte Delegierung. Weitere Informationen zur delegierten Authentifizierung und eingeschränkte Delegierung finden Sie unter [Delegieren der Authentifizierung](https://go.microsoft.com/fwlink/?LinkId=106614).  

- Sie müssen möglicherweise eine Firewall zwischen der Organisation und den anderen Gesamtstrukturen in der Organisation, das Beschränken des Zugriffs auf Daten außerhalb der Gesamtstruktur herstellen.  

- Obwohl die Datenisolation, zum Erstellen einer separaten Gesamtstruktur aktiviert werden, solange die Domänencontroller in der isolierten Gesamtstruktur und der Computer,, auf geschützte Hostinformationen in einem Netzwerk zugegriffen werden, sind anfällig für Angriffe, die von Computern im Netzwerk gestartet. Organisationen, die sich entscheiden, dass das Risiko eines Angriffs zu hoch ist oder zur Folge, dass eine Verletzung der Angriff oder Sicherheit zu groß ist Einschränken des Zugriffs auf das Netzwerk oder Netzwerken, die die Domänencontrollern hosten müssen und die Computer auf denen ausgeführt wird, werden geschützte Daten . Beschränken des Zugriffs kann mithilfe von Technologien wie Firewalls und internetprotokollsicherheit (IPsec) erfolgen. In Extremfällen können Organisationen auch die geschützten Daten auf ein unabhängiges Netzwerk zu verwalten, die keine physische Verbindung zu einem anderen Netzwerk in der Organisation aufweist.  

   > [!NOTE]  
   > Wenn eine Netzwerkverbindung zwischen einer Gesamtstruktur mit eingeschränktem Zugriff und einem anderen Netzwerk vorhanden ist, besteht die Möglichkeit, Daten in der eingeschränkten Bereich mit dem anderen Netzwerk übertragen werden.  

## <a name="BKMK_5"></a>Szenario 5: Verwenden Sie eine Organisationsgesamtstruktur, oder Konfigurieren der Firewalls für eingeschränkte Konnektivität  

Um eine eingeschränkte Konnektivität-Anforderung zu erfüllen, können Sie eine der folgenden Aktionen ausführen:  

- Benutzer in einer bestehenden Organisation Gesamtstruktur platzieren, und Öffnen der Firewalls genug für Active Directory-Datenverkehrs zu durchlaufen.  

- Verwenden Sie eine Organisationsgesamtstruktur. Platzieren Sie den Benutzer, Gruppen und Computer für die Gruppe, die für die Verbindung begrenzt ist, in einer separaten Gesamtstruktur für die Organisation. Weisen Sie Einzelperson aus dieser Gruppe der Gesamtstrukturbesitzer sein. Der Organisationsgesamtstruktur bietet eine separate Umgebung, auf der anderen Seite der Firewall. Die Gesamtstruktur enthält Benutzerkonten und Ressourcen, die in der Gesamtstruktur verwaltet werden, sodass Benutzer nicht über die Firewall für ihre täglichen Aufgaben zu müssen. Bestimmte Benutzer oder Anwendungen möglicherweise spezielle Anforderungen, die die Funktion für die Firewall, wenden Sie sich an anderen Gesamtstrukturen erforderlich. Sie können diese Anforderungen einzeln adressieren, öffnen Sie die entsprechenden Schnittstellen in der Firewall, einschließlich derer für Vertrauensstellungen funktionieren erforderlich sind.  

Weitere Informationen zum Konfigurieren von Firewalls für die Verwendung mit Active Directory Domain Services (AD DS) finden Sie unter [Active Directory in Netzwerken durch Firewalls segmentiert](https://go.microsoft.com/fwlink/?LinkId=37928).  

## <a name="BKMK_6"></a>Szenario 6: Verwenden einer Organisation Gesamtstruktur oder Domäne, und Konfigurieren der Firewalls für die Autonomie eines Dienstes mit eingeschränkter Konnektivität  

Wenn eine Gruppe in Ihrer Organisation die Autonomie eines Dienstes als Anforderung identifiziert, empfehlen wir, dass Sie zuerst diese Anforderung überdenken. Eine Dienstautonomie erstellt, mehr Verwaltungsaufwand und die zusätzlichen Kosten für die Organisation. Stellen Sie sicher, dass die Anforderung für die Autonomie eines Dienstes nicht einfach der Einfachheit halber ist und Sie die Kosten erfüllt diese Anforderung im Blocksatz ausrichten können.  

Wenn eingeschränkte Konnektivität ein Problem ist, und Sie eine Anforderung für die Autonomie eines Dienstes haben, können Sie eine der folgenden führen:  

- Verwenden Sie eine Organisationsgesamtstruktur. Platzieren Sie den Benutzer, Gruppen und Computer für die Gruppe, die die Autonomie eines Dienstes in einer separaten Organisation Gesamtstruktur erforderlich sind. Weisen Sie Einzelperson aus dieser Gruppe der Gesamtstrukturbesitzer sein. Der Organisationsgesamtstruktur bietet eine separate Umgebung, auf der anderen Seite der Firewall. Die Gesamtstruktur enthält Benutzerkonten und Ressourcen, die in der Gesamtstruktur verwaltet werden, sodass Benutzer nicht über die Firewall für ihre täglichen Aufgaben zu müssen. Bestimmte Benutzer oder Anwendungen möglicherweise spezielle Anforderungen, die die Funktion für die Firewall, wenden Sie sich an anderen Gesamtstrukturen erforderlich. Sie können diese Anforderungen einzeln adressieren, öffnen Sie die entsprechenden Schnittstellen in der Firewall, einschließlich derer für Vertrauensstellungen funktionieren erforderlich sind.  

- Platzieren Sie den Benutzer, Gruppen und Computer in einer separaten Domäne in einer vorhandenen Organisation Gesamtstruktur an. Dieses Modell ermöglicht nur die Autonomie eines Dienstes von auf Domänenebene und nicht für vollständige Dienstautonomie, der Isolation oder die Datenisolation-Diensts. Andere Gruppen in der Gesamtstruktur müssen die Dienstadministratoren der neuen Domäne, die den gleichen Grad an vertrauen, dass sie den Gesamtstrukturbesitzer vertrauen. Aus diesem Grund empfehlen wir nicht diesen Ansatz. Weitere Informationen zur Verwendung von organisatorischer Domänen finden Sie unter [mit dem Organisations-Gesamtstruktur Domänenmodell](../../ad-ds/plan/../../ad-ds/plan/Using-the-Organizational-Domain-Forest-Model.md).  

Sie müssen auch die Firewall zum Zulassen von Active Directory-Datenverkehr passieren genug zu öffnen. Weitere Informationen zum Konfigurieren von Firewalls für die Verwendung mit AD DS finden Sie unter [Active Directory in Netzwerken durch Firewalls segmentiert](https://go.microsoft.com/fwlink/?LinkId=37928).  

## <a name="BKMK_7"></a>Szenario 7: Verwenden einer Ressourcengesamtstruktur und Konfigurieren der Firewalls für die Isolation von Diensten mit eingeschränkter Konnektivität  

Wenn eingeschränkte Konnektivität ein Problem ist, und Sie eine Voraussetzung für die Isolation von Diensten haben, können Sie eine der folgenden führen:  

- Verwenden Sie eine Organisationsgesamtstruktur. Platzieren Sie den Benutzer, Gruppen und Computer für die Gruppe, die Isolation von Diensten in einer separaten Organisation Gesamtstruktur erforderlich sind. Weisen Sie Einzelperson aus dieser Gruppe der Gesamtstrukturbesitzer sein. Der Organisationsgesamtstruktur bietet eine separate Umgebung, auf der anderen Seite der Firewall. Die Gesamtstruktur enthält Benutzerkonten und Ressourcen, die in der Gesamtstruktur verwaltet werden, sodass Benutzer nicht über die Firewall für ihre täglichen Aufgaben zu müssen. Bestimmte Benutzer oder Anwendungen möglicherweise spezielle Anforderungen, die die Funktion für die Firewall, wenden Sie sich an anderen Gesamtstrukturen erforderlich. Sie können diese Anforderungen einzeln adressieren, öffnen Sie die entsprechenden Schnittstellen in der Firewall, einschließlich derer für Vertrauensstellungen funktionieren erforderlich sind.  

- Verwenden einer Ressourcengesamtstruktur. Platzieren Sie Ressourcen und Dienstkonten in separaten Ressourcengesamtstruktur-Benutzerkonten in einer vorhandenen Organisation Gesamtstruktur beibehalten. Es ist möglicherweise erforderlich, einige Alternativen Benutzerkonten zu erstellen, in der Ressourcengesamtstruktur, verwalten den Zugriff auf die Ressourcen-Gesamtstruktur aus, wenn der Organisationsgesamtstruktur nicht mehr verfügbar ist. Die alternativen Konten benötigen die erforderliche Autorität zur melden Sie sich bei der Ressourcen-Gesamtstruktur und die Kontrolle über die Ressourcen, bis der Organisationsgesamtstruktur wieder online ist.  

   Eine Vertrauensstellung zwischen der Ressource und Organisations-Gesamtstrukturen, damit die Benutzer auf die Ressourcen in der Gesamtstruktur zugreifen können, bei der Verwendung von ihren normalen Benutzerkonten. Diese Konfiguration ermöglicht die zentralisierte Verwaltung von Benutzerkonten während Benutzer auf alternative Konten in der Ressourcengesamtstruktur zurück, wenn der Organisationsgesamtstruktur nicht verfügbar ist.  

Die folgenden: Überlegungen zur Isolation von Diensten  

- Gesamtstrukturen, die für die dienstisolierung kann Domänen aus anderen Gesamtstrukturen "vertrauen", jedoch dürfen keine Benutzer aus anderen Gesamtstrukturen in ihrer Administratoren Dienstgruppen erstellt werden. Wenn Benutzer aus anderen Gesamtstrukturen in der administrativen Gruppen in der isolierten Gesamtstruktur enthalten sind, kann die Sicherheit der isolierten Gesamtstruktur möglicherweise beeinträchtigt werden, da die Dienstadministratoren in der Gesamtstruktur keine exklusive Kontrolle.  

- Als Domänencontroller in einem Netzwerk zugegriffen werden kann, sind sie anfällig für Angriffe (z. B. Denial-of-Service-Angriffe) von Computern im Netzwerk. Zum Schutz gegen die Möglichkeit eines Angriffs Folgendes möglich:  

   - Host-Domänencontroller nur in Netzwerken, die als sicher eingestuft werden.  

   - Beschränken des Zugriffs auf Netzwerke, die der Domänencontroller gehostet werden.  

- Isolation von Diensten ist die Erstellung einer zusätzlichen Gesamtstruktur erforderlich. Bewerten Sie, ob die Kosten für die Verwaltung der Infrastruktur zur Unterstützung der Gesamtstruktur zusätzlichen Kosten im Zusammenhang mit Verlust des Zugriffs auf Ressourcen aufgrund einer Organisationsgesamtstruktur nicht verfügbar ist überwiegt.  

   Bestimmte Benutzer oder Anwendungen möglicherweise spezielle Anforderungen, die die Funktion für die Firewall, wenden Sie sich an anderen Gesamtstrukturen erforderlich. Sie können diese Anforderungen einzeln adressieren, öffnen Sie die entsprechenden Schnittstellen in der Firewall, einschließlich derer für Vertrauensstellungen funktionieren erforderlich sind.  

Weitere Informationen zum Konfigurieren von Firewalls für die Verwendung mit AD DS finden Sie unter [Active Directory in Netzwerken durch Firewalls segmentiert](https://go.microsoft.com/fwlink/?LinkId=37928).  

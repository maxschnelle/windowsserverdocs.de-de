---
ms.assetid: b8df1828-5ead-4c90-b0fe-95c675116b7c
title: Erstellen eines Organisationseinheitsentwurfs
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 96fd3dd2d090ef6b39b99962e6b639bf2abdcb62
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87947741"
---
# <a name="creating-an-organizational-unit-design"></a>Erstellen eines Organisationseinheitsentwurfs

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Gesamtstruktur Besitzer sind dafür verantwortlich, Organisationseinheiten-Entwürfe für Ihre Domänen zu erstellen. Das Erstellen eines Organisationseinheiten Entwurfs umfasst das Entwerfen der OE-Struktur, das Zuweisen der OE-Besitzer Rolle und das Erstellen von Konto-und Ressourcen Organisationseinheiten.

Entwerfen Sie zunächst Ihre OE-Struktur, um die Delegierung der Verwaltung zu ermöglichen. Wenn der OE-Entwurf fertig ist, können Sie zusätzliche OU-Strukturen für die Anwendung von Gruppenrichtlinie für die Benutzer und Computer erstellen und die Sichtbarkeit von Objekten einschränken. Weitere Informationen finden Sie unter [Entwerfen einer Gruppenrichtlinie-Infrastruktur](/previous-versions/windows/it-pro/windows-server-2003/cc786524(v=ws.10)).

## <a name="ou-owner-role"></a>OU-Besitzer Rolle
Der Gesamtstruktur Besitzer bezeichnet einen OE-Besitzer für jede Organisationseinheit, die Sie für die Domäne entwerfen. OU-Besitzer sind Daten-Manager, die eine Teilstruktur von Objekten in Active Directory Domain Services Steuern (AD DS). Organisationseinheiten Besitzer können steuern, wie die Verwaltung delegiert wird und wie Richtlinien auf Objekte innerhalb ihrer Organisationseinheit angewendet werden. Sie können auch neue Unterstrukturen erstellen und die Verwaltung von Organisationseinheiten innerhalb dieser Teil Strukturen delegieren.

Da Organisationseinheiten Besitzer den Betrieb des Verzeichnis Dienstanbieter nicht besitzen oder Steuern, können Sie den Besitz und die Verwaltung des Verzeichnis Dienstanbieter von Besitz und Verwaltung von Objekten trennen und so die Anzahl von Dienst Administratoren, die über einen hohen Zugriffs Grad verfügen, verringern.

Organisationseinheiten bieten administrative Autonomie und die Mittel zum Steuern der Sichtbarkeit von Objekten im Verzeichnis. Organisationseinheiten bieten Isolation von anderen Daten Administratoren, bieten aber keine Isolation von Dienst Administratoren. Obwohl Organisationseinheiten Besitzer die Kontrolle über eine Teilstruktur von Objekten haben, behält der Gesamtstruktur Besitzer die volle Kontrolle über alle Teil Strukturen. Dadurch kann der Gesamtstruktur Besitzer Fehler beheben, z. b. einen Fehler in einer Zugriffs Steuerungs Liste (Access Control List, ACL), und Delegierte Teil Strukturen freigeben, wenn Daten Administratoren beendet werden.

## <a name="account-ous-and-resource-ous"></a>Konto-OUs und Ressourcen-OUs
Konto Organisationseinheiten enthalten Benutzer-, Gruppen-und Computer Objekte. Gesamtstruktur Besitzer müssen eine OE-Struktur erstellen, um diese Objekte zu verwalten, und dann die Kontrolle über die Struktur an den Besitzer der Organisationseinheit delegieren. Wenn Sie eine neue AD DS Domäne bereitstellen, erstellen Sie eine Konto-Organisationseinheit für die Domäne, damit Sie die Kontrolle über die Konten in der Domäne delegieren können.

Die Ressourcen Organisationseinheiten enthalten Ressourcen und die Konten, die für die Verwaltung dieser Ressourcen zuständig sind. Der Gesamtstruktur Besitzer ist auch dafür verantwortlich, eine OE-Struktur zu erstellen, um diese Ressourcen zu verwalten und die Steuerung dieser Struktur an den Besitzer der Organisationseinheit zu delegieren. Erstellen Sie nach Bedarf Ressourcen-OUs basierend auf den Anforderungen der einzelnen Gruppen innerhalb Ihres Unternehmens, um Autonomie bei der Verwaltung von Daten und Geräten zu unterstützen.

## <a name="documenting-the-ou-design-for-each-domain"></a>Dokumentieren des OE-Entwurfs für jede Domäne
Assemblieren Sie ein Team zum Entwerfen der OE-Struktur, mit der Sie die Kontrolle über Ressourcen innerhalb der Gesamtstruktur delegieren. Der Gesamtstruktur Besitzer ist möglicherweise am Entwurfsprozess beteiligt und muss den OE-Entwurf genehmigen. Sie können auch mindestens einen Dienst Administrator einbeziehen, um sicherzustellen, dass der Entwurf gültig ist. Andere Entwurfs Team Teilnehmer können die Daten Administratoren enthalten, die an den Organisationseinheiten und den OE-Besitzern arbeiten, die für die Verwaltung zuständig sind.

Es ist wichtig, den ou-Entwurf zu dokumentieren. Auflisten der Namen der Organisationseinheiten, die Sie erstellen möchten. Dokumentieren Sie für jede Organisationseinheit den Typ der Organisationseinheit, den OE-Besitzer, die übergeordnete Organisationseinheit (falls zutreffend) und den Ursprung der Organisationseinheit.

Für ein Arbeitsblatt, das Sie bei der Dokumentation Ihres OE-Entwurfs unterstützt, laden Sie Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip aus den [Auftrags Hilfen für Windows Server 2003 Deployment Kit](https://microsoft.com/download/details.aspx?id=9608) herunter, und öffnen Sie "Identifizierungs-OUs für jede Domäne" (DSSLOGI_9.doc).

## <a name="in-this-section"></a>In diesem Abschnitt

- [Überprüfen von Entwurfskonzepten für Organisationseinheiten](../../ad-ds/plan/Reviewing-OU-Design-Concepts.md)

- [Delegieren der Verwaltung mithilfe von Organisationseinheitsobjekten](../../ad-ds/plan/Delegating-Administration-by-Using-OU-Objects.md)

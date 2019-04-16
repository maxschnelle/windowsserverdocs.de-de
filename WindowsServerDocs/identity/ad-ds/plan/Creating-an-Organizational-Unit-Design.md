---
ms.assetid: b8df1828-5ead-4c90-b0fe-95c675116b7c
title: Erstellen eines Organisationseinheitsentwurfs
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3a74770a4558c79d1f9250f37181562e1d235d34
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="creating-an-organizational-unit-design"></a>Erstellen eines Organisationseinheitsentwurfs

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Besitzer von Gesamtstrukturen sind verantwortlich für die Organisationseinheit (OU) Designs für die Domänen erstellen. Erstellen einen OU-Entwurf umfasst das Entwerfen der OE-Struktur, das Zuweisen der Rolle "Standorttopologiebesitzer" Organisationseinheit, und Erstellen von Konto- und Organisationseinheiten.  
  
Entwerfen Sie zunächst der OU-Struktur zum Delegieren von Verwaltungsaufgaben zu aktivieren. Wenn die OU-Entwurf abgeschlossen ist, können Sie zusätzliche OU-Strukturen für die Anwendung der Gruppenrichtlinie für die Benutzer und Computer und die Sichtbarkeit der Objekte begrenzen erstellen. Weitere Informationen finden Sie unter Entwerfen einer Group Policy Infrastructure ([https://go.microsoft.com/fwlink/?LinkId=106655](https://go.microsoft.com/fwlink/?LinkId=106655)).  
  
## <a name="ou-owner-role"></a>Organisationseinheit-Rolle  
Der Gesamtstrukturbesitzer bezeichnet einen Besitzer für jede Organisationseinheit, die Sie für die Domäne zu entwerfen. OU-Besitzer sind Daten-Manager, die eine Unterstruktur der Objekte in Active Directory-Domänendienste (AD DS) verwalten. OU-Besitzer können steuern, wie die Verwaltung delegiert und Richtlinien auf Objekte in ihrer Organisationseinheit angewendet wird. Sie können auch neue Unterstrukturen erstellen und Delegieren der Verwaltung von Organisationseinheiten innerhalb dieser Unterstrukturen.  
  
Da die OU-Besitzer nicht besitzen oder der Vorgang des Verzeichnisdiensts, können Sie trennen Besitz und Verwaltung des Verzeichnisdiensts Besitz und Verwaltung von Objekten, Reduzieren der Anzahl der Dienstadministratoren, die hohes Maß an Zugriff haben.  
  
OEs bieten unabhängige Verwaltung suchen und die Möglichkeit zum Steuern der Sichtbarkeit von Objekten im Verzeichnis. OEs bieten die Isolierung von anderen Datenadministratoren, aber sie bieten keine Isolierung von Dienstadministratoren. Obwohl die OU-Besitzer Kontrolle über eine Unterstruktur der Objekte haben, behält der Gesamtstrukturbesitzer Vollzugriff auf alle Unterstrukturen. Dadurch kann den Gesamtstrukturbesitzer So beheben Sie Fehler, z.B. ein Fehler in einer Zugriffssteuerungsliste (ACL), und delegierte Unterstrukturen freigeben, wenn Datenadministratoren beendet werden.  
  
## <a name="account-ous-and-resource-ous"></a>Konten- und Ressourcenorganisationseinheiten  
Konto-OEs werden Benutzer, Gruppen und Computer Objekte enthalten. Besitzer von Gesamtstrukturen müssen eine OE-Struktur, um diese Objekte verwaltet und dann Delegieren der Verwaltung der Struktur der Besitzer der Organisationseinheit erstellen. Wenn Sie eine neue AD DS-Domäne bereitstellen, erstellen Sie ein Konto Organisationseinheit für die Domäne, sodass Sie die Konten in der Domäne delegieren können.  
  
Ressourcenorganisationseinheiten enthalten die Ressourcen und die Konten, die für die Verwaltung dieser Ressourcen zuständig sind. Der Gesamtstrukturbesitzer ist auch zuständig, zum Erstellen einer OE-Struktur zur Verwaltung dieser Ressourcen sowie zum Delegieren der Steuerung dieser Struktur der Organisationseinheit Besitzer. Erstellen Sie Ressourcen-OUs nach Bedarf anhand der Anforderungen der einzelnen Gruppen in Ihrer Organisation für Autonomie bei der Verwaltung von Daten und Geräten.  
  
## <a name="documenting-the-ou-design-for-each-domain"></a>Dokumentieren des OU-Entwurfs für jede Domäne  
Bauen Sie ein Team, um die OU-Struktur zu entwerfen, die Sie verwenden, um die Steuerung von Ressourcen innerhalb der Gesamtstruktur zu delegieren. Der Gesamtstrukturbesitzer des Entwurfsprozesses beteiligt sind und Organisationseinheitsentwurfs genehmigen muss. Sie können auch umfassen mindestens einen Dienstadministrator, um sicherzustellen, dass das Design gültig ist. Andere Teilnehmer der Design-Team können die Datenadministratoren enthalten, die auf die Organisationseinheiten und die Besitzer arbeiten, die für die Verwaltung dieser verantwortlich sind.  
  
Es ist wichtig, Ihre Organisationseinheitsentwurfs dokumentieren. Listen Sie die Namen der Organisationseinheiten, die Sie erstellen möchten. Und Dokumentieren Sie den Typ der Organisationseinheit, der Besitzer der Organisationseinheit, die übergeordnete Organisationseinheit (falls zutreffend) und den Ursprung der Organisationseinheit für jede Organisationseinheit.  
  
Bei einem Arbeitsblatt unterstützen Sie beim Dokumentieren des OU-Entwurfs herunterladen Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Überprüfen von Entwurfskonzepten für Organisationseinheiten](../../ad-ds/plan/Reviewing-OU-Design-Concepts.md)  
  
-   [Delegieren der Verwaltung mithilfe von Organisationseinheitsobjekten](../../ad-ds/plan/Delegating-Administration-by-Using-OU-Objects.md)  
  



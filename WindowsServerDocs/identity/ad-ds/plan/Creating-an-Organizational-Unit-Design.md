---
ms.assetid: b8df1828-5ead-4c90-b0fe-95c675116b7c
title: Erstellen eines Organisationseinheitsentwurfs
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9ecd0228b50a4e597c3fa1dbd3fdaf1f84ca1d3f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830401"
---
# <a name="creating-an-organizational-unit-design"></a>Erstellen eines Organisationseinheitsentwurfs

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Gesamtstruktur-Besitzer sind verantwortlich für die Organisationseinheit (OU)-Entwürfe für ihre Domänen zu erstellen. Erstellen eines Organisationseinheitsentwurfs umfasst das Entwerfen der OE-Struktur, das Zuweisen der Rolle "Besitzer" OE, und erstellen Konto- und Organisationseinheiten.  
  
Entwerfen Sie zunächst Ihre OE-Struktur, um die Delegierung der Verwaltung zu aktivieren. Wenn die OU-Entwurf abgeschlossen ist, können Sie zusätzliche OE-Strukturen für die Anwendung der Gruppenrichtlinie auf die Benutzer und Computer und die Sichtbarkeit von Objekten beschränkt erstellen. Weitere Informationen finden Sie unter Entwerfen einer Gruppenrichtlinien-Infrastruktur ([https://go.microsoft.com/fwlink/?LinkId=106655](https://go.microsoft.com/fwlink/?LinkId=106655)).  
  
## <a name="ou-owner-role"></a>Rolle "Besitzer" Organisationseinheit  
Der Gesamtstrukturbesitzer gibt einen Besitzer für jede Organisationseinheit, die Sie für die Domäne zu entwerfen. OU-Besitzer sind, Daten-Manager, die eine Unterstruktur von Objekten in Active Directory Domain Services (AD DS) zu steuern. OE-Besitzer können steuern, wie die Verwaltung delegiert wird und wie die Richtlinie auf Objekte in ihrer Organisationseinheit angewendet wird. Sie können neue Teilstrukturen auch Delegieren der Verwaltung von Organisationseinheiten innerhalb dieser Teilstrukturen.  
  
Da OU-Besitzer besitzen oder steuern den Vorgang des Verzeichnisdiensts nicht, können Sie trennen, Besitz und Verwaltung des Verzeichnisdiensts von Besitz und Verwaltung von Objekten, Reduzierung der Anzahl von Dienstadministratoren, die hohe haben der Zugriff.  
  
Organisationseinheiten bieten unabhängige Verwaltung suchen und die Möglichkeit zum Steuern der Sichtbarkeit von Objekten im Verzeichnis. Organisationseinheiten bieten Isolierung von anderen Datenadministratoren, aber sie bieten keine Isolation von Dienstadministratoren. Obwohl OU-Besitzer Kontrolle über eine Unterstruktur von Objekten haben, behält der Gesamtstrukturbesitzer vollständige Kontrolle über alle Unterstrukturen aus. Dadurch wird der Gesamtstrukturbesitzer zur Behebung von Fehlern, z. B. ein Fehler in einer Zugriffssteuerungsliste (ACL), und um delegierte Teilstrukturen freizugeben, wenn Datenadministratoren beendet werden.  
  
## <a name="account-ous-and-resource-ous"></a>Konto-OEs und Ressourcenorganisationseinheiten  
Konto-OEs enthalten Benutzer-, Gruppen- und Computer-Objekte. Besitzer von Gesamtstrukturen müssen eine OU-Struktur, um diese Objekte zu verwalten und Delegieren der Kontrolle über die Struktur dann an den Besitzer der Organisationseinheit erstellen. Wenn Sie eine neue AD DS-Domäne bereitstellen, erstellen Sie ein Konto Organisationseinheit für die Domäne, damit Sie Kontrolle über die Konten in der Domäne delegieren können.  
  
Ressourcenorganisationseinheiten enthalten Ressourcen und die Konten, die für die Verwaltung dieser Ressourcen zuständig sind. Der Gesamtstrukturbesitzer ist auch verantwortlich für das Erstellen einer OE-Struktur, um diese Ressourcen zu verwalten und Delegieren der Steuerung von dieser Struktur der Organisationseinheit Besitzer. Erstellen Sie Ressource Organisationseinheiten nach Bedarf basierend auf den Anforderungen der einzelnen Gruppen innerhalb Ihrer Organisation für autonomen Betrieb bei der Verwaltung der Daten und Geräte.  
  
## <a name="documenting-the-ou-design-for-each-domain"></a>Dokumentieren des Entwurfs der Organisationseinheit für jede Domäne  
Assemblieren Sie ein Team aus, um die OE-Struktur zu entwerfen, die Sie verwenden, um die Kontrolle über Ressourcen in der Gesamtstruktur zu delegieren. Der Gesamtstrukturbesitzer möglicherweise den Entwurfsprozess beteiligt und muss den Entwurf der Organisationseinheit genehmigen. Sie eventuell auch mindestens einen Dienstadministrator, um sicherzustellen, dass der Entwurf gültig ist. Anderen Teilnehmer der Design-Team können es sich um die Datenadministratoren enthalten, die auf die Organisationseinheit und die Organisationseinheiten Besitzer funktionieren, die bei der Verwaltung verantwortlich ist.  
  
Es ist wichtig, zu dokumentieren des Entwurfs Organisationseinheit. Listet die Namen der Organisationseinheiten, die Sie erstellen möchten. Und für jede Organisationseinheit, dokumentieren Sie den Typ der Organisationseinheit, der Besitzer der Organisationseinheit, die übergeordnete Organisationseinheit (falls zutreffend) und den Ursprung der dieser Organisationseinheit.  
  
Bei einem Arbeitsblatt beim Dokumentieren des Entwurfs Organisationseinheit Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip aus Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit herunterladen ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), und öffnen Sie " Identifizieren von OEs für jede Domäne"(DSSLOGI_9.doc).  
  
## <a name="in-this-section"></a>Inhalt dieses Abschnitts  
  
-   [Überprüfen von Entwurfskonzepten](../../ad-ds/plan/Reviewing-OU-Design-Concepts.md)  
  
-   [Delegieren der Verwaltung mithilfe von Organisationseinheitsobjekten](../../ad-ds/plan/Delegating-Administration-by-Using-OU-Objects.md)  
  



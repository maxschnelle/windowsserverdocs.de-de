---
ms.assetid: 9ee8a6cb-7550-46e2-9c11-78d0545c3a97
title: "Dynamische Zugriffssteuerung (Übersicht)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5cf74042c9b511abb1fbeb88224dea0c7f2c8706
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="dynamic-access-control-overview"></a>Dynamische Zugriffssteuerung (Übersicht)

>Gilt für: Windows Server2012 R2, Windows Server 2012

In diesem Übersichtsthema für IT-Experten beschreibt die dynamische Zugriffssteuerung und der zugehörige Elemente, die in Windows Server2012 und Windows8 eingeführt wurden.  
  
Domänenbasierten dynamischen Zugriffssteuerung können Administratoren gelten Access-Control-Berechtigungen und Einschränkungen basierend auf klar definierten Regeln, die Vertraulichkeit der Ressourcen, die Auftrag oder Rolle des Benutzers und die Konfiguration des Geräts, das verwendet wird, den Zugriff auf diese Ressourcen enthalten kann.  
  
Beispielsweise kann ein Benutzer unterschiedliche Berechtigungen verfügen, wenn sie eine Ressource vom Bürocomputer zugreifen, wenn sie einen tragbaren Computer über ein virtuelles privates Netzwerk verwendet werden. Oder den Zugriff erlaubt, dass nur, wenn ein Gerät die Sicherheit erfüllt, die von den Netzwerkadministratoren definiert sind. Bei der dynamischen Zugriffssteuerung verwendet wird, ändern sich Berechtigungen des Benutzers dynamisch ohne Eingreifen des Administrators zusätzliche Wenn Tätigkeit oder Rolle des Benutzers geändert wird (was Attribute des Benutzers in AD DS).  
  
Dynamische Zugriffssteuerung wird in Windows-Betriebssystemen vor Windows Server2012 und Windows8 nicht unterstützt. Bei der dynamischen Zugriffssteuerung in Umgebungen mit unterstützten und nicht unterstützten Versionen von Windows konfiguriert ist, werden nur die unterstützten Versionen der Änderungen implementiert.  
  
Features und Konzepte, die dynamische Zugriffssteuerung gehören:  
  
-   [Zentrale Zugriffsregeln](#BKMK_Rules)  
  
-   [Zentrale Zugriffsrichtlinien](#BKMK_Policies)  
  
-   [Ansprüche](#BKMK_Claims)  
  
-   [Ausdrücke](#BKMK_Expressions2)  
  
-   [Vorgeschlagene Berechtigungen](#BKMK_Permissions2)  
  
### <a name="BKMK_Rules"></a>Zentrale Zugriffsregeln  
Eine zentrale Zugriffsregel ist ein Ausdruck von Autorisierungsregeln, die eine oder mehrere Bedingungen, die im Zusammenhang mit Benutzergruppen, Benutzeransprüche, Geräteansprüche und Ressourceneigenschaften enthalten kann. Mehrere zentrale Zugriffsregeln können in einer zentralen Zugriffsrichtlinie zusammengefasst werden.  
  
Wenn eine oder mehrere zentrale Zugriffsregeln für eine Domäne definiert wurden, können dateifreigabeadministratoren bestimmte Regeln an bestimmte Ressourcen und Geschäftsanforderungen entsprechen.  
  
### <a name="BKMK_Policies"></a>Zentrale Zugriffsrichtlinien  
Zentrale Zugriffsrichtlinien sind Autorisierungsrichtlinien, die bedingte Ausdrücke enthalten. Zum Beispiel angenommen, ein Unternehmen eine Anforderung zum Zugriff auf personenbezogene Daten (PII) hat in Dateien auf den Dateibesitzer und Mitglieder der Personalabteilung (HR), die Personenbezogene Daten einsehen dürfen. Hierbei handelt es sich um eine unternehmensweite Richtlinie, die auf PII-Dateien angewendet werden soll, wenn sie in der gesamten Organisation auf Dateiservern befinden. Um die Implementierung dieser Richtlinie muss ein Unternehmen kann Folgendes:  
  
-   Identifizieren Sie und kennzeichnen Sie die Dateien, die die personenbezogene Daten enthalten.  
  
-   Identifizieren Sie die Gruppe der Personalabteilung den Personenbezogene Daten einsehen dürfen.  
  
-   Fügen Sie die zentrale Zugriffsrichtlinie einer zentralen Zugriffsregel hinzu, und wenden Sie die zentrale Zugriffsregel auf alle Dateien, die personenbezogenen, Dateiservern in der gesamten Organisation können.  
  
Zentrale Zugriffsrichtlinien dienen als sicherheitsschirme, die eine Organisation auf alle Server angewendet wird. Diese Richtlinien gelten zusätzlich zu (jedoch nicht ersetzen) den lokalen Zugriffsrichtlinien oder freigegebenen Zugriffssteuerungslisten (DACL), die auf Dateien und Ordner angewendet werden.  
  
### <a name="BKMK_Claims"></a>Ansprüche  
Ein Anspruch ist eine eindeutige Information zu einem Benutzer, Gerät oder Ressourcen, die von einem Domänencontroller veröffentlicht wurde. Die Position des Benutzers, der Abteilung Klassifizierung einer Datei oder den Integritätsstatus eines Computers sind gültige Beispiele für einen Anspruch. Eine Entität kann mehrere Ansprüche, und kann eine beliebige Kombination von Ansprüchen zum Autorisieren des Zugriffs auf Ressourcen verwendet werden. Die folgenden Arten von Ansprüchen stehen in den unterstützten Versionen von Windows zur Verfügung:  
  
-   **Benutzeransprüche** Active Directory-Attribute, die einem bestimmten Benutzer zugeordnet sind.  
  
-   **Geräteansprüche** Active Directory-Attribute, die einem bestimmten Computerobjekt zugeordnet sind.  
  
-   **Ressourcenattribute** globale Ressourceneigenschaften, die für die Verwendung bei Autorisierungsentscheidungen gekennzeichnet sind, und in Active Directory veröffentlicht.  
  
Ansprüche können Administratoren präzise Organisation oder unternehmensweite Anweisungen zu Benutzern, Geräten und Ressourcen, die integriert werden können in Ausdrücke, Regeln und Richtlinien.  
  
### <a name="BKMK_Expressions2"></a>Ausdrücke  
Bedingte Ausdrücke sind eine Verbesserung der Verwaltung der Zugriffssteuerung, die zulassen oder Verweigern des Zugriffs auf Ressourcen nur, wenn bestimmte Bedingungen erfüllt sind, z.B., Gruppenmitgliedschaft, Standort oder Sicherheitsstatus eines Geräts. Ausdrücke werden über das Dialogfeld "Erweiterte Sicherheitseinstellungen" von der ACL-Editor oder die Editors für zentrale Zugriffsregeln in den Active Directory Administrative Center (ADAC) verwaltet.  
  
Mithilfe von Ausdrücken können Administratoren den Zugriff auf sensible Ressourcen mit flexiblen Bedingungen in zunehmend komplexeren geschäftsumgebungen leichter verwalten.  
  
### <a name="BKMK_Permissions2"></a>Vorgeschlagene Berechtigungen  
Vorgeschlagene Berechtigungen können Administratoren exakter modellieren, die Auswirkungen möglicher Änderungen auf zugriffssteuerungseinstellungen, ohne sie tatsächlich zu ändern.  
  
Wenn Sie den effektiven Zugriff auf eine Ressource vorhersagen können Sie beim Planen und konfigurieren Berechtigungen für diese Ressourcen, bevor Sie diese Änderungen implementieren.  
  
## <a name="additional-changes"></a>Zusätzliche Änderungen  
Weitere Verbesserungen in den unterstützten Versionen von Windows, die Unterstützung der dynamischen Zugriffssteuerung gehören:  
  
### <a name="support-in-the-kerberos-authentication-protocol-to-reliably-provide-user-claims-device-claims-and-device-groups"></a>Unterstützung im Kerberos-Authentifizierungsprotokolls benutzeransprüchen, Geräteansprüchen und Gerätegruppen zuverlässig bereitstellen.  
Standardmäßig sind Geräte, die mit einem der unterstützten Versionen von Windows im Zusammenhang mit dynamische Zugriffssteuerung Kerberos-Tickets, verarbeiten die Verbundauthentifizierung erforderliche Daten enthalten. Domänencontroller sind ausstellen und Kerberos-Tickets mit zusammengesetzten Authentifizierung-bezogene Informationen reagieren können. Wenn eine Domäne für die dynamische Zugriffssteuerung erkennen konfiguriert ist, Geräte Ansprüche von Domänencontrollern erhalten, während der anfänglichen Authentifizierung, und sie verbundauthentifizierungstickets beim Einreichen von dienstticketanforderungen. Die Verbundauthentifizierung ergibt ein Zugriffstoken, enthält die Identität des Benutzers und das Gerät auf die Ressourcen, die dynamische Zugriffssteuerung erkennen.  
  
### <a name="support-for-using-the-key-distribution-center-kdc-group-policy-setting-to-enable-dynamic-access-control-for-a-domain"></a>Unterstützung für die Verwendung der Key Distribution Center Schlüsselverteilungscenter (KDC)-Gruppenrichtlinien-Einstellung dynamische Zugriffssteuerung für eine Domäne zu aktivieren.  
Alle Domänencontroller muss auf die gleiche Richtlinieneinstellung Administrative Vorlage unter **Computer Computerkonfiguration\Richtlinien\Administrative vorlagen\System\kdc\unterstützung dynamische Zugriffssteuerung und Kerberos Armoring**.  
  
### <a name="support-for-using-the-key-distribution-center-kdc-group-policy-setting-to-enable-dynamic-access-control-for-a-domain"></a>Unterstützung für die Verwendung der Key Distribution Center Schlüsselverteilungscenter (KDC)-Gruppenrichtlinien-Einstellung dynamische Zugriffssteuerung für eine Domäne zu aktivieren.  
Alle Domänencontroller muss auf die gleiche Richtlinieneinstellung Administrative Vorlage unter **Computer Computerkonfiguration\Richtlinien\Administrative vorlagen\System\kdc\unterstützung dynamische Zugriffssteuerung und Kerberos Armoring**.  
  
### <a name="support-in-active-directory-to-store-user-and-device-claims-resource-properties-and-central-access-policy-objects"></a>Unterstützung in Active Directory zum Speichern von Benutzer- und Geräteansprüchen, Ressourceneigenschaften und Objekte der zentralen Zugriffsrichtlinie.  
  
### <a name="support-for-using-group-policy-to-deploy-central-access-policy-objects"></a>Unterstützung für die Verwendung von Gruppenrichtlinien zum Bereitstellen der Objekte der zentralen Zugriffsrichtlinie.  
Die folgende Einstellung der Gruppenrichtlinie können Sie Objekte der zentralen Zugriffsrichtlinie für Dateiserver in Ihrem Unternehmen bereitstellen: **computerkonfiguration\richtlinien\ Windows-einstellungen\sicherheitseinstellungen\Dateisystem\zentrale Zugriffsrichtlinie**.  
  
### <a name="support-for-claims-based-file-authorization-and-auditing-for-file-systems-by-using-group-policy-and-global-object-access-auditing"></a>Unterstützung für anspruchsbasierte dateiauthentifizierung und Überwachung für Dateisysteme mithilfe von Gruppenrichtlinien und globaler Objektzugriffsüberwachung  
Sie müssen die Überwachungsrichtlinien bereitgestellten zentralen Zugriff, um den effektiven Zugriff der zentralen Zugriffsrichtlinie Überwachen mithilfe von vorgeschlagenen Berechtigungen aktivieren. Sie konfigurieren diese Einstellung für den Computer unter **erweiterte Überwachungsrichtlinienkonfiguration** in der **Sicherheitseinstellungen** von einem Gruppenrichtlinienobjekt (GPO). Nachdem Sie die sicherheitseinstellung im GPO konfigurieren, können Sie das Gruppenrichtlinienobjekt auf Computern in Ihrem Netzwerk bereitstellen.  
  
### <a name="support-for-transforming-or-filtering-claim-policy-objects-that-traverse-active-directory-forest-trusts"></a>Unterstützung für die Transformation oder Filterung von anspruchsrichtlinienobjekten, die Active Directory-Gesamtstruktur-Vertrauensstellungen durchlaufen  
Sie können filtern oder Transformieren eingehender und ausgehender Ansprüche, die eine Gesamtstruktur-Vertrauensstellung durchlaufen. Es gibt drei grundlegende Szenarien für die Filterung und Transformation von Ansprüchen:  
  
-   **Werten basierende Filterung** Filter können basierend auf den Wert eines Anspruchs. Dadurch wird die vertrauenswürdige Gesamtstruktur zu verhindern, dass Ansprüche mit bestimmten Werten für die vertrauende Gesamtstruktur gesendet werden. Domänencontroller in vertrauenden Gesamtstrukturen können Werten basierende Filterung um Elevation of Privilege Angriffen zu schützen, indem Sie von der vertrauenswürdigen Gesamtstruktur die eingehenden Ansprüche mit bestimmten Werten filtern.  
  
-   **Anspruchstyp basierende Filterung** Filter basieren auf dem Anspruchstyp, anstatt den Wert des Anspruchs. Identifizieren Sie den Anspruchstyp, durch den Namen des Anspruchs. Verwenden Sie den Anspruchstyp basierende Filterung in der vertrauenswürdigen Gesamtstruktur, und es wird verhindert, dass Windows Ansprüche sendet, die Informationen zur vertrauenden Gesamtstruktur preisgeben.  
  
-   **Anspruchstyp basierende Transformation** ändert einen Anspruch, bevor er an das gewünschte Ziel gesendet wird. Verwenden Sie Anspruchstyp basierende Transformation von Ansprüchen in der vertrauenswürdigen Gesamtstruktur, um einen bekannten Anspruch zu generalisieren, der Informationen enthält. Transformationen können Sie den Anspruchstyp, den Anspruchswert oder beides generalisieren.  
  
## <a name="software-requirements"></a>Anforderungen der Clientsoftware  
Da Ansprüche und Verbundauthentifizierung für die dynamische Zugriffssteuerung Kerberos-authentifizierungserweiterungen erfordern, müssen eine Domäne, die dynamische Zugriffssteuerung unterstützt genügend Domänencontroller mit unterstützten Versionen von Windows zur Unterstützung der Authentifizierung über dynamische Zugriffssteuerung unterstützt Kerberos-Clients. Standardmäßig müssen Geräte Domänencontrollern an anderen Standorten verwenden. Wenn keine solchen Domänencontroller verfügbar sind, schlägt die Authentifizierung fehl. Aus diesem Grund müssen Sie eine der folgenden Bedingungen unterstützt:  
  
-   Jede Domäne, die dynamische Zugriffssteuerung unterstützt muss genügend Domänencontroller mit unterstützten Versionen von Windows Server zur Unterstützung der Authentifizierung von allen Geräten, die mit den unterstützten Versionen von Windows oder Windows Server verfügen.  
  
-   Geräte mit den unterstützten Versionen von Windows oder die Ressourcen nicht mithilfe von Ansprüchen oder Verbundidentität schützen, sollten Unterstützung des Kerberos-Protokolls für die dynamische Zugriffssteuerung deaktivieren.  
  
Für Domänen, die Benutzeransprüche unterstützen, muss alle Domänencontroller mit unterstützten Versionen von Windows Server mit den entsprechenden Einstellungen zur Unterstützung von Ansprüchen und Verbundauthentifizierung und Kerberos-hochrüstung konfiguriert werden. Konfigurieren Sie die Einstellungen in der administrativen Vorlage KDC-Richtlinie wie folgt:  
  
-   **Immer Ansprüche bereitstellen** verwenden Sie diese Einstellung, wenn alle Domänencontroller mit unterstützten Versionen von Windows Server ausgeführt werden. Darüber hinaus legen Sie die Domänenfunktionsebene auf Windows Server2012 oder höher.  
  
-   **Unterstützt** Wenn Sie diese Einstellung verwenden, überwachen Sie Domänencontroller, um sicherzustellen, dass die Anzahl der Domänencontroller mit unterstützten Versionen von Windows Server für die Anzahl der Clientcomputer ausreicht, die Zugriff auf Ressourcen durch die dynamische Zugriffssteuerung geschützt werden müssen.  
  
Wenn die Benutzerdomäne und die dateiserverdomäne in unterschiedlichen Gesamtstrukturen befinden, müssen alle Domänencontroller im Gesamtstrukturstamm des Dateiservers auf der Windows Server2012 oder eine höhere Funktionsebene festgelegt werden.  
  
Wenn Clients die dynamische Zugriffssteuerung nicht erkannt werden, muss zwischen den beiden Gesamtstrukturen eine bidirektionale Vertrauensstellung sein.  
  
Wenn Ansprüche beim Verlassen einer Gesamtstruktur transformiert werden, müssen alle Domänencontroller im Gesamtstrukturstamm des Benutzers auf der Windows Server2012 oder eine höhere Funktionsebene festgelegt werden.  
  
Ein Server unter Windows Server2012 oder Windows Server2012 R2 benötigen eine Gruppenrichtlinien-Einstellung, die angibt, ob Benutzeransprüche für Benutzertoken abgerufen werden, die keine Ansprüche enthalten. Diese Einstellung ist standardmäßig so festgelegt **automatische**, wodurch dieser Einstellung der Gruppenrichtlinie aktiviert werden **auf** ist eine zentrale Richtlinie, die Benutzer- oder Geräteansprüche für diesen Dateiserver enthält. Wenn der Dateiserver freigegebene Zugriffssteuerungslisten, die Benutzeransprüche enthalten enthält, müssen Sie diese Gruppenrichtlinie festlegen, um **auf**, damit der Server weiß, um Ansprüche für Benutzer anfordern, die beim Zugriff auf den Server keine Ansprüche bereitstellen.  
  
## <a name="additional-resource"></a>Zusätzliche Ressourcen  
Informationen zur Implementierung von Lösungen, die basierend auf dieser Technologie finden Sie unter [dynamische Zugriffssteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md).  
  



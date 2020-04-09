---
ms.assetid: 9ee8a6cb-7550-46e2-9c11-78d0545c3a97
title: Übersicht über die dynamische Zugriffssteuerung
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 2374e2c8a1efb204dbae1ee633bc5ee41d049d57
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861173"
---
# <a name="dynamic-access-control-overview"></a>Übersicht über die dynamische Zugriffssteuerung

>Gilt für: Windows Server 2012 R2, Windows Server 2012

Dieses Übersichtsthema für IT-Spezialisten beschreibt die dynamische Zugriffssteuerung und die zugehörigen Elemente, die in Windows Server 2012 und Windows 8 eingeführt wurden.  
  
Mithilfe der domänenbasierten dynamischen Zugriffssteuerung können Administratoren Zugriffssteuerungsberechtigungen und Einschränkungen basierend auf klar definierten Regeln anwenden, die sich auf die Vertraulichkeit der Ressourcen, den Auftrag oder die Rolle des Benutzers und die Konfiguration des Geräts beziehen können, das für den Zugriff auf diese Ressourcen verwendet wird.  
  
Beispielsweise kann ein Benutzer über unterschiedliche Berechtigungen verfügen, je nachdem, ob er vom Bürocomputer aus oder mit einem tragbaren Computer über ein virtuelles privates Netzwerk auf eine Ressource zugreift. Oder der Zugriff wird nur erlaubt, wenn ein Gerät den von den Netzwerkadministratoren definierten Sicherheitsanforderungen entspricht. Bei Verwendung von Dynamic Access Control werden die Berechtigungen eines Benutzers dynamisch geändert, ohne dass ein zusätzlicher Administrator Eingriff erforderlich ist, wenn der Auftrag oder die Rolle des Benutzers geändert wird (was zu Änderungen an den Konto Attributen des Benutzers in AD DS führt).  
  
Die dynamische Zugriffssteuerung wird in Windows-Betriebssystemen vor Windows Server 2012 und Windows 8 nicht unterstützt. Wenn die dynamische Zugriffssteuerung in Umgebung mit unterstützten und nicht unterstützten Versionen von Windows konfiguriert wird, werden die Änderungen nur in die unterstützten Versionen implementiert.  
  
Die dynamische Zugriffssteuerung bietet die folgenden Features und Konzepte:  
  
-   [Zentrale Zugriffsregeln](#BKMK_Rules)  
  
-   [Zentrale Zugriffsrichtlinien](#BKMK_Policies)  
  
-   [Claims](#BKMK_Claims)  
  
-   [Eindrücke](#BKMK_Expressions2)  
  
-   [Vorgeschlagene Berechtigungen](#BKMK_Permissions2)  
  
### <a name="central-access-rules"></a><a name="BKMK_Rules"></a>Zentrale Zugriffsregeln  
Eine zentrale Zugriffsregel ist ein Ausdruck von Autorisierungsregeln, die eine oder mehrere Bedingungen beinhalten können, die sich auf Benutzergruppen, Benutzeransprüche, Geräteansprüche und Ressourceneigenschaften beziehen können. Mehrere zentrale Zugriffsregeln können zu einer zentralen Zugriffsrichtlinie zusammengefasst werden.  
  
Wenn für eine Domäne eine oder mehrere zentrale Zugriffsregeln definiert werden, können Dateifreigabeadministratoren bestimmte Regeln an bestimmte Ressourcen und Geschäftsanforderungen anpassen.  
  
### <a name="central-access-policies"></a><a name="BKMK_Policies"></a>Zentrale Zugriffsrichtlinien  
Zentrale Zugriffsrichtlinien sind Autorisierungsrichtlinien, die bedingte Ausdrücke enthalten. Angenommen, eine Organisation hat eine geschäftliche Anforderung, den Zugriff auf personenbezogene Informationen (PII) in Dateien auf den Dateibesitzer und die Mitglieder der Personalabteilung (Personalabteilung, HR) zu beschränken, die personenbezogene Informationen anzeigen dürfen. Es handelt sich hierbei um eine organisationsweite Richtlinie, die für Dateien mit personenbezogenen Daten gilt, und zwar unabhängig davon, auf welchen Dateiservern in der gesamten Organisation sie sich befinden. Für die Implementierung dieser Richtlinie muss ein Unternehmen Folgendes können:  
  
-   Es muss die Dateien, die personenbezogene Daten enthalten, identifizieren und kennzeichnen können.  
  
-   Es muss die Gruppe der Mitarbeiter der Personalabteilung identifizieren können, die die personenbezogenen Daten einsehen dürfen.  
  
-   Es muss die zentrale Zugriffsrichtlinie einer zentralen Zugriffsregel hinzufügen und die zentrale Zugriffsregel auf alle Dateien mit personenbezogenen Daten auf allen Dateiservern im gesamten Unternehmen anwenden können.  
  
Zentrale Zugriffsrichtlinien dienen als Sicherheitsschirme, die ein Unternehmen auf alle Server anwendet. Diese Richtlinien gelten zusätzlich zu (nicht anstelle von) den lokalen Zugriffsrichtlinien oder freigegebenen Zugriffssteuerungslisten (Discretionary Access Control Lists, DACLs), die auf Dateien und Ordner angewendet werden.  
  
### <a name="claims"></a><a name="BKMK_Claims"></a>Claims  
Bei einem Anspruch handelt es sich um eindeutige, von einem Domänencontroller veröffentlichte Informationen zu Benutzern, Geräten oder Ressourcen. Der Titel des Benutzers, die Abteilungs Klassifizierung einer Datei oder der Integritäts Status eines Computers sind gültige Beispiele für einen Anspruch. Eine Entität kann mehrere Ansprüche aufweisen, und der Zugriff auf Ressourcen kann mit jeder beliebigen Kombination aus Ansprüchen autorisiert werden. Die folgenden Typen von Ansprüchen stehen in den unterstützten Versionen von Windows zur Verfügung:  
  
-   **Benutzeransprüche**: Active Directory-Attribute, die einem bestimmten Benutzer zugeordnet sind.  
  
-   **Geräteansprüche**: Active Directory-Attribute, die einem bestimmten Computerobjekt zugeordnet sind.  
  
-   **Ressourcenattribute**: Globale Ressourceneigenschaften, die für die Verwendung bei Autorisierungsentscheidungen gekennzeichnet sind und in Active Directory veröffentlicht wurden.  
  
Mithilfe von Ansprüchen können Administratoren präzise, unternehmensweite Anweisungen zu Benutzern, Geräten und Ressourcen erstellen, die in Ausdrücke, Regeln und Richtlinien integriert werden können.  
  
### <a name="expressions"></a><a name="BKMK_Expressions2"></a>Eindrücke  
Bedingte Ausdrücke sind eine Erweiterung der Zugriffssteuerungsverwaltung, mit denen der Zugriff auf Ressourcen gewährt oder verweigert wird, wenn bestimmte Bedingungen zu Gruppenmitgliedschaft, Standort oder Sicherheitsstatus eines Geräts erfüllt sind. Ausdrücke werden über das Dialogfeld %%amp;quot;Erweiterte Sicherheitseinstellungen%%amp;quot; des ACL-Editors oder des Editors für zentrale Zugriffsregeln im Active Directory-Verwaltungscenter (AD AC) verwaltet.  
  
Mithilfe von Ausdrücken können Administratoren den Zugriff auf vertrauliche Ressourcen mit flexiblen Bedingungen in zunehmend komplexeren Geschäftsumgebungen leichter verwalten.  
  
### <a name="proposed-permissions"></a><a name="BKMK_Permissions2"></a>Vorgeschlagene Berechtigungen  
Mithilfe von vorgeschlagenen Berechtigungen können Administratoren die Auswirkungen möglicher Änderungen auf Zugriffssteuerungseinstellungen exakter modellieren, ohne die Änderungen tatsächlich vornehmen zu müssen.  
  
Wenn Sie den effektiven Zugriff auf eine Ressource vorhersagen können, können Sie Berechtigungen für diese Ressourcen planen und konfigurieren, bevor Sie diese Änderungen implementieren.  
  
## <a name="additional-changes"></a>Weitere Änderungen  
Weitere Verbesserungen in den unterstützten Versionen von Windows, die die dynamische Zugriffssteuerung unterstützen:  
  
### <a name="support-in-the-kerberos-authentication-protocol-to-reliably-provide-user-claims-device-claims-and-device-groups"></a>Unterstützung im Kerberos-Authentifizierungsprotokoll zur zuverlässigen Bereitstellung von Benutzeransprüchen, Geräteansprüchen und Gerätegruppen.  
Geräte, auf denen eine der unterstützten Versionen von Windows ausgeführt wird, können standardmäßig Kerberos-Tickets für die dynamische Zugriffssteuerung verarbeiten, die für die Verbundauthentifizierung erforderliche Daten enthalten. Domänencontroller können Kerberos-Tickets mit Informationen zur Verbundauthentifizierung ausgeben und auf diese reagieren. Wenn eine Domäne für die Erkennung der dynamischen Zugriffssteuerung konfiguriert wurde, empfangen Geräte bei der Erstauthentifizierung Ansprüche von Domänencontrollern und beim Einreichen von Dienstticketanforderungen Verbundauthentifizierungstickets. Die Verbundauthentifizierung ergibt ein Zugriffstoken, der die Identität des Benutzers und des Geräts in den Ressourcen enthält, die die dynamische Zugriffssteuerung erkennen.  
  
### <a name="support-for-using-the-key-distribution-center-kdc-group-policy-setting-to-enable-dynamic-access-control-for-a-domain"></a>Unterstützung für die Verwendung der KDC-Gruppenrichtlinieneinstellung (Key Distribution Center, Schlüsselverteilungscenter) zur Aktivierung der dynamischen Zugriffssteuerung für eine Domäne.  
Alle Domänencontroller müssen dieselbe Einstellung für die Richtlinie für administrative Vorlagen aufweisen, die sich unter **Computerkonfiguration\Richtlinien\Administrative Vorlagen\System\KDC\Unterstützung für die dynamische Zugriffssteuerung und die Kerberos-Hochrüstung** befindet.  
  
### <a name="support-for-using-the-key-distribution-center-kdc-group-policy-setting-to-enable-dynamic-access-control-for-a-domain"></a>Unterstützung für die Verwendung der KDC-Gruppenrichtlinieneinstellung (Key Distribution Center, Schlüsselverteilungscenter) zur Aktivierung der dynamischen Zugriffssteuerung für eine Domäne.  
Alle Domänencontroller müssen dieselbe Einstellung für die Richtlinie für administrative Vorlagen aufweisen, die sich unter **Computerkonfiguration\Richtlinien\Administrative Vorlagen\System\KDC\Unterstützung für die dynamische Zugriffssteuerung und die Kerberos-Hochrüstung** befindet.  
  
### <a name="support-in-active-directory-to-store-user-and-device-claims-resource-properties-and-central-access-policy-objects"></a>Unterstützung in Active Directory zum Speichern von Benutzer- und Geräteansprüchen, Ressourceneigenschaften und Objekten der zentralen Zugriffsrichtlinie.  
  
### <a name="support-for-using-group-policy-to-deploy-central-access-policy-objects"></a>Unterstützung für die Verwendung von Gruppenrichtlinien zur Bereitstellung von Objekten der zentralen Zugriffsrichtlinie.  
Mithilfe der folgenden Gruppenrichtlinieneinstellung können Sie Objekte der zentralen Zugriffsrichtlinie für Dateiserver in Ihrem Unternehmen bereitstellen: **Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Dateisystem\Zentrale Zugriffsrichtlinie**.  
  
### <a name="support-for-claims-based-file-authorization-and-auditing-for-file-systems-by-using-group-policy-and-global-object-access-auditing"></a>Unterstützung für anspruchsbasierte Dateiauthentifizierung und Überwachung für Dateisysteme mithilfe von Gruppenrichtlinien und globaler Objektzugriffsüberwachung  
Sie müssen die in Phasen ausgeführte Überwachung der zentralen Zugriffsrichtlinie aktivieren, um den effektiven Zugriff der zentralen Zugriffsrichtlinie mithilfe von vorgeschlagenen Berechtigungen zu überwachen. Diese Einstellung wird für den Computer unter **Erweiterte Überwachungsrichtlinienkonfiguration** in den **Sicherheitseinstellungen** eines Gruppenrichtlinienobjekts (GPO) konfiguriert. Nachdem Sie die Sicherheitseinstellung im GPO konfiguriert haben, können Sie das GPO für Computer im Netzwerk bereitstellen.  
  
### <a name="support-for-transforming-or-filtering-claim-policy-objects-that-traverse-active-directory-forest-trusts"></a>Unterstützung für die Transformation oder Filterung von Anspruchsrichtlinienobjekten, die Active Directory-Gesamtstruktur-Vertrauensstellungen durchlaufen  
Sie können ein- und ausgehende Ansprüche, die eine Gesamtstruktur-Vertrauensstellung durchlaufen, filtern oder transformieren. Es gibt drei grundlegende Szenarien für die Filterung und Transformation von Ansprüchen:  
  
-   **Auf Werten basierende Filterung**: Filter können basierend auf dem Wert eines Anspruchs definiert werden. Damit kann in der vertrauenswürdigen Gesamtstruktur verhindert werden, dass Ansprüche mit bestimmten Werten an die vertrauende Gesamtstruktur gesendet werden. Domänencontroller in vertrauenden Gesamtstrukturen können mithilfe der wertebasierten Filterung einen Rechteerweiterungsangriff verhindern, indem sie die von der vertrauenswürdigen Gesamtstruktur eingehenden Ansprüche mit bestimmten Werten filtern.  
  
-   **Auf dem Anspruchstyp basierende Filterung**: Filter werden nicht nach dem Wert des Anspruchs, sondern basierend auf dem Anspruchstyp definiert. Sie können den Anspruchstyp am Namen des Anspruchs erkennen. Sie verwenden die auf dem Anspruchstyp basierende Filterung in der vertrauenswürdigen Gesamtstruktur, und verhindern damit, dass Windows Ansprüche sendet, die Informationen zur vertrauenden Gesamtstruktur preisgeben.  
  
-   **Auf dem Anspruchstyp basierende Transformation**: Damit wird ein Anspruch geändert, bevor er an das gewünschte Ziel gesendet wird. Die auf dem Anspruchstyp basierende Transformation wird in der vertrauenswürdigen Gesamtstruktur verwendet, um einen bekannten Anspruch, der bestimmte Informationen enthält, zu generalisieren. Mit einer Transformationen können Sie den Anspruchstyp, den Anspruchswert oder beides generalisieren.  
  
## <a name="software-requirements"></a>Softwareanforderungen  
Da Ansprüche und Verbundauthentifizierung für die dynamische Zugriffssteuerung Kerberos-Authentifizierungserweiterungen erfordern, müssen alle Domänen, die die dynamische Zugriffssteuerung unterstützen, über genügend Domänencontroller mit unterstützten Versionen von Windows verfügen, um die Authentifizierung über Kerberos-Clients zu unterstützen, die die dynamische Zugriffssteuerung unterstützen. Geräte müssen standardmäßig Domänencontroller an anderen Standorten verwenden. Wenn Domänencontroller dieser Art nicht verfügbar sind, treten bei der Authentifizierung Fehler auf. Daher muss eine der folgenden Bedingungen erfüllt sein:  
  
-   Jede Domäne, die dynamische Zugriffssteuerung unterstützt muss über genügend Domänencontroller mit unterstützten Versionen von Windows Server verfügen, um die Authentifizierung über Geräte zu unterstützen, auf denen die unterstützten Versionen von Windows oder Windows Server ausgeführt werden.  
  
-   Bei Geräten mit unterstützten Versionen von Windows oder bei Geräten, die Ressourcen nicht mithilfe von Ansprüchen oder Verbundidentität schützen, muss die Unterstützung des Kerberos-Protokolls für die dynamische Zugriffskontrolle deaktiviert werden.  
  
Bei Domänen, die Benutzeransprüche unterstützen, müssen alle Domänencontroller mit unterstützten Versionen von Windows Server mit den entsprechenden Einstellungen zur Unterstützung von Ansprüchen und Verbundauthentifizierung und für die Bereitstellung der Kerberos-Hochrüstung konfiguriert werden. Konfigurieren Sie die Einstellungen in der KDC-Richtlinie für administrative Vorlagen wie folgt:  
  
-   **Immer Ansprüche bereitstellen**: Verwenden Sie diese Einstellung, wenn auf allen Domänencontrollern unterstützte Versionen von Windows Server ausgeführt wird. Außerdem muss die Domänenfunktionsebene auf Windows Server 2012 oder höher festgelegt werden.  
  
-   **Unterstützt**: Wenn Sie diese Einstellung verwenden, überwachen Sie Domänencontroller, um sicherzustellen, dass die Anzahl der Domänencontroller, auf denen unterstützte Versionen von Windows Server ausgeführt werden, für die Anzahl der Clientcomputer ausreicht, die auf Ressourcen zugreifen müssen, die durch die dynamische Zugriffssteuerung geschützt werden.  
  
Wenn sich die Benutzer Domäne und die Dateiserver Domäne in unterschiedlichen Gesamtstrukturen befinden, müssen alle Domänen Controller im Gesamtstruktur Stamm des Dateiservers auf der Funktionsebene Windows Server 2012 oder höher festgelegt werden.  
  
Wenn Clients die dynamische Zugriffssteuerung nicht erkennen, muss zwischen den beiden Gesamtstrukturen eine bidirektionale Vertrauensstellung bestehen.  
  
Wenn Ansprüche beim Verlassen einer Gesamtstruktur transformiert werden, müssen alle Domänen Controller im Gesamtstruktur Stamm des Benutzers auf der Funktionsebene Windows Server 2012 oder höher festgelegt werden.  
  
Ein Dateiserver, auf dem Windows Server 2012 oder Windows Server 2012 R2 ausgeführt wird, muss über eine Gruppenrichtlinieneinstellung verfügen, die angibt, ob Benutzeransprüche für Benutzertoken, die keine Ansprüche enthalten, abgerufen werden müssen. Diese Einstellung ist standardmäßig auf **Automatisch** festgelegt, was dazu führt, dass diese Gruppenrichtlinieneinstellung auf **An** festgelegt wird, wenn eine zentrale Richtlinie vorhanden ist, die Benutzer- oder Geräteansprüche für diesen Dateiserver enthält. Wenn der Dateiserver freigegebene Zugriffssteuerungslisten mit Benutzeransprüchen enthält, muss diese Gruppenrichtlinie auf **An** festgelegt werden, sodass der Server weiß, dass er Ansprüche für Benutzer anfordern muss, die beim Zugriff auf den Server keine Ansprüche bereitstellen.  
  
## <a name="additional-resource"></a>Zusätzliche Ressource  
Informationen zum Implementieren von Lösungen basierend auf dieser Technologie finden Sie unter [Dynamic Access Control: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md).  
  



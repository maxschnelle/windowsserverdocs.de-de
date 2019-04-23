---
ms.assetid: 7f6b27e5-dc55-4ffc-8e76-6d57e65a870b
title: Anhang A Dynamic Access Control Glossar
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b2044355812e95b9a5bfe90e33257f11ce78cf93
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856701"
---
# <a name="appendix-a-dynamic-access-control-glossary"></a>Anhang A: Dynamic Access Control-Glossar

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Im folgenden werden die Liste der Begriffe und Definitionen, die in der Dynamic Access Control-Szenario enthalten sind.  
  
|Begriff|Definition|  
|--------|--------------|  
|Automatische Klassifizierung|Klassifizierung, die auftritt, basierend auf den Klassifizierungseigenschaften, die von Klassifizierungsregeln, die von einem Administrator konfiguriert bestimmt werden.|  
|CAPID|Zentrale Zugriffsrichtlinien Richtlinien-ID. Diese ID verweist auf eine bestimmte zentrale Zugriffsrichtlinie aus, und es wird verwendet, um die Richtlinie aus der Sicherheitsbeschreibung der Dateien und Ordner zu verweisen.|  
|Zentrale Zugriffsregel|Eine Regel, die eine Bedingung und einen Ausdruck für den enthält.|  
|Zentrale Zugriffsrichtlinie|Richtlinien, die erstellt und in Active Directory gehostet werden.|  
|Anspruchsbasierte Zugriffssteuerung|Ein Modell, das Ansprüche zum treffen von Entscheidungen hinsichtlich der Zugriffssteuerung auf Ressourcen verwendet.|  
|Klassifizierung|Der Prozess der Ermittlung der Klassifizierungseigenschaften von Ressourcen und die Metadaten, die mit den Ressourcen zugeordnet ist, diese Eigenschaften zuweisen. Siehe auch REF AutomaticClassification \h \\* MERGEFORMAT automatische Klassifizierung, REF-InheritedClassification \h \\ \* Klassifizierung MERGEFORMAT geerbt und REF ManualClassification \h \\ \* MERGEFORMAT manuelle Klassifizierung.|  
|Geräteanspruch|Einen Anspruch, der mit dem System verbunden ist.  Mit benutzeransprüchen ist es in das Token eines Benutzers auf eine Ressource zuzugreifen versuchen, enthalten.|  
|Besitzerverwaltete Zugriffssteuerungsliste (DACL)|Eine Access Control List, die Vertrauensnehmer identifiziert, die zugelassen oder verweigert den Zugriff auf eine sicherungsfähige Ressource. Sie können nach dem Ermessen des der Besitzer der Ressource geändert werden.|  
|Ressourceneigenschaft|Eigenschaften (z. B. Bezeichnungen), die eine Datei beschreiben und Dateien über die automatische Klassifizierung oder die manuelle Klassifizierung zugewiesen sind. Dazu gehören: Zeitraum für Vertraulichkeit, Projekt- und Aufbewahrung.|  
|Ressourcen-Manager für Dateiserver|Eine Funktion in das Windows Server-Betriebssystem, das Verwaltung von ordnerkontingenten, dateiprüfung, Speicherberichte, dateiklassifizierung und Datei-Management-Aufträge auf einem Dateiserver bietet.|  
|Ordnereigenschaften und Bezeichnungen|Eigenschaften und Bezeichnungen, die einen Ordner zu beschreiben und von Administratoren und Besitzern der Ordner manuell zugewiesen werden. Diese Eigenschaften weisen standardmäßig Eigenschaftswerte auf die Dateien in diesen Ordnern, z. B. Secrecy oder Abteilung.|  
|Gruppenrichtlinie|Ein Satz von Regeln und Richtlinien, die arbeitsumgebung von Benutzern und Computern in einer Active Directory-Umgebung zu steuern.|  
|NEAR Real-Time-Klassifizierung|Die automatische Klassifizierung, die ausgeführt wird, kurz nachdem eine Datei erstellt oder geändert wird.|  
|NEAR Real-Time-Dateiserver verwenden Dateiverwaltungsaufgaben|Dateiverwaltungsaufgaben, die kurz nach ausgeführt werden (eine Datei erstellt oder geändert wird. Diese Aufgaben werden durch die nahezu in Echtzeit Klassifizierung ausgelöst.|  
|Organisationseinheit (OU)|Active Directory-Container, der hierarchische, logische Strukturen innerhalb einer Organisation darstellt. Es ist die kleinste Einheit der Gruppenrichtlinien-Einstellungen angewendet werden.|  
|Sichern Sie die Eigenschaft|Eine Klassifizierungseigenschaft, die die Laufzeit für die Autorisierung vertrauen kann, um eine gültige Assertion zur Ressource an einem bestimmten Zeitpunkt Point-in-werden. In der anspruchsbasierten Zugriffssteuerung wird eine sichere-Eigenschaft, die auf eine Ressource zugewiesen ist als Ressourcenanspruch behandelt.|  
|Sicherheitsbeschreibung|Eine Datenstruktur, die eine sicherungsfähige Ressource, z. B. Zugriffssteuerungslisten zugeordneten Sicherheitsinformationen enthält.|  
|Security Descriptor Definition language|Eine Spezifikation, die Informationen in einer Sicherheitsbeschreibung als Textzeichenfolge beschreibt.|  
|Staging-Richtlinie|Eine zentrale Zugriffsrichtlinie, die nicht noch gültig ist.|  
|Systemzugriffssteuerungsliste (SACL)|Eine Access Control List, die die Arten von Zugriffsversuchen durch bestimmte Vertrauensnehmer angibt, für die Überwachungsdatensätze, die generiert werden müssen.|  
|Benutzeranspruch.|Die Attribute eines Benutzers, die in den Sicherheitstoken des Benutzers bereitgestellt werden. Dazu gehören: Abteilung, Unternehmen, Projekt, und sicherheitsbestätigung.  Informationen im Benutzertoken von Systemen vor Windows Server 2012, z. B. die Sicherheitsgruppen, denen der Benutzer angehört, kann auch von benutzeransprüchen betrachtet werden. Einige Benutzeransprüche über Active Directory bereitgestellt werden, und andere werden dynamisch berechnet, wie z. B., ob der Benutzer angemeldet mit einer Smartcard anmelden.|  
|Benutzertoken|Ein Objekt, das angibt, einen Benutzer und die von benutzeransprüchen und geräteansprüchen, die diesem Benutzer zugeordnet sind. Es wird verwendet, um den Benutzerzugriff auf Ressourcen zu autorisieren.|  
  
## <a name="see-also"></a>Siehe auch  
[Dynamische Zugriffssteuerung: Übersicht über das Szenario](Dynamic-Access-Control--Scenario-Overview.md)  
  



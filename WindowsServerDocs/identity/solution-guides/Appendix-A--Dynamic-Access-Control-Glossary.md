---
ms.assetid: 7f6b27e5-dc55-4ffc-8e76-6d57e65a870b
title: Anhang A dynamische Steuerelement Glossar
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b2044355812e95b9a5bfe90e33257f11ce78cf93
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="appendix-a-dynamic-access-control-glossary"></a>Anhang A: dynamische Steuerelement Glossar

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Im folgenden werden die Liste mit Begriffen und Definitionen, die in dem Szenario für die dynamische Zugriffssteuerung enthalten sind.  
  
|Begriff|Definition|  
|--------|--------------|  
|Automatische Klassifizierung|Klassifizierung, das auftritt, basierend auf Klassifizierungseigenschaften, die vom Klassifizierungsregeln, die von einem Administrator konfiguriert ermittelt werden.|  
|CAPID|Zentrale Richtlinien-ID. Diese ID beziehen sich auf eine bestimmte zentrale Zugriffsrichtlinie aus, und es wird verwendet, um die Richtlinie aus der Sicherheitsbeschreibung von Dateien und Ordnern zu verweisen.|  
|Zentrale Zugriffsregel|Eine Regel, die eine Bedingung und ein Zugriffsausdruck enthält.|  
|Zentrale Zugriffsrichtlinie|Richtlinien, die erstellt und in Active Directory gehostet werden.|  
|Anspruchsbasierte Zugriffssteuerung|Ein Paradigma, die Ansprüche an die Access-Steuerelement Entscheidungen bezüglich der Ressourcen nutzt.|  
|Klassifizierung|Der Vorgang zur Bestimmung der Klassifizierungseigenschaften der Ressourcen und die Metadaten, die die Ressourcen zugeordnet ist diese Eigenschaften zuweisen. Siehe auch REF AutomaticClassification \h \\ * MERGEFORMAT automatische Klassifizierung, REF InheritedClassification \h \\\ * MERGEFORMAT geerbt Klassifizierung und REF ManualClassification \h \\\ * MERGEFORMAT manuelle Klassifizierung.|  
|Geräteanspruch|Eine Anforderung, die mit dem System verbunden ist.  Mit benutzeransprüchen ist es in das Token eines Benutzers auf eine Ressource zuzugreifen versuchen, enthalten.|  
|Besitzerverwalteten Zugriffssteuerungsliste (DACL)|Eine Zugriffssteuerungsliste, die Vertrauensnehmer identifiziert, die gestattet oder verweigert den Zugriff auf einer sicherungsfähigen Ressource. Sie können im Ermessen des der Besitzer der Ressource geändert werden.|  
|Ressourceneigenschaft|Eigenschaften (z. B. Beschriftungen), die eine Datei beschreiben und Dateien mithilfe von automatischen Klassifizierung oder die manuelle Klassifizierung zugewiesen sind. Beispiele: Vertraulichkeit, Projekt und Aufbewahrungsfristen.|  
|File Server Resource Manager|Ein Feature in Windows Server-Betriebssystem, das Verwaltung von ordnerkontingenten, Datei-Filterung, Speicherberichte, dateiklassifizierung und Datei-Management-Aufträge auf einem Dateiserver bietet.|  
|Eigenschaften des Ordners und Bezeichnungen|Eigenschaften und Beschriftungen, die beschreiben eines Ordners und von Administratoren und Besitzern der Ordner manuell zugewiesen werden. Diese Eigenschaften weisen standardmäßig Eigenschaftswerte auf die Dateien in diesen Ordnern, z. B. Secrecy oder Abteilung.|  
|Gruppenrichtlinie|Ein Satz von Regeln und Richtlinien, die arbeitsumgebung von Benutzern und Computern in einer Active Directory-Umgebung zu steuern.|  
|In der Nähe Echtzeit-Klassifizierung|Automatische Klassifizierung, die ausgeführt wird, kurz nachdem eine Datei erstellt oder geändert wird.|  
|In der Nähe in Echtzeit Dateiverwaltungsaufgaben|Dateiverwaltungsaufgaben, die kurz nach ausgeführt werden (eine Datei erstellt oder geändert. Diese Aufgaben werden durch die nahezu in Echtzeit Klassifizierung ausgelöst.|  
|Organisationseinheit (OE)|Active Directory-Container, der hierarchische, logische Strukturen in einer Organisation darstellt. Es ist die kleinste Einheit der Gruppenrichtlinie angewendet werden.|  
|Diese Eigenschaft|Eine Klassifizierungseigenschaft, die die Autorisierung Runtime vertrauen kann, um eine gültige Assertion zur Ressource an eine bestimmte Point-in-Time werden. Bei der anspruchsbasierten Zugriffssteuerung wird eine sichere-Eigenschaft, die auf eine Ressource zugewiesen ist als Ressource Anspruch behandelt.|  
|Die Sicherheitsbeschreibung|Eine Datenstruktur, die Sicherheitsinformationen im Zusammenhang mit einer sicherungsfähigen Ressource, z. B. Zugriffssteuerungslisten enthält.|  
|Security Descriptor Definition language|Eine Spezifikation, die eine Sicherheitsbeschreibung als Zeichenfolge enthält.|  
|Staging-Richtlinie|Eine zentrale Zugriffsrichtlinie, die nicht noch gültig ist.|  
|System-Zugriffssteuerungsliste (SACL)|Eine Zugriffssteuerungsliste, die die Arten von Zugriffsversuchen durch bestimmte Vertrauensnehmer gibt an, für die Überwachungsdatensätze generiert werden müssen.|  
|Benutzeranspruch|Attribute eines Benutzers, die in das Sicherheitstoken für Benutzer bereitgestellt werden. Beispiele: Abteilung, Unternehmen, Projekt und sicherheitsbestätigung.  Informationen in das Benutzertoken von Systemen vor Windows Server 2012, z. B. die Sicherheitsgruppen, denen der Benutzer gehört, kann ebenfalls Benutzeransprüche berücksichtigt werden. Einige Benutzeransprüche werden durch Active Directory bereitgestellt und andere werden dynamisch berechnet, wie z. B., ob der Benutzer angemeldet sich mit einer Smartcard.|  
|Das Benutzertoken|Ein Objekt, das identifiziert eines Benutzers und die Benutzer- und geräteansprüchen, die dem Benutzer zugeordnet sind. Hiermit wird der Benutzer den Zugriff auf Ressourcen autorisieren.|  
  
## <a name="see-also"></a>Siehe auch  
[Dynamische Zugriffssteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  



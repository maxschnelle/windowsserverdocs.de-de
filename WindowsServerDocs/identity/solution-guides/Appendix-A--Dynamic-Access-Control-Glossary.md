---
ms.assetid: 7f6b27e5-dc55-4ffc-8e76-6d57e65a870b
title: Anhang A Dynamic Access Control Glossar
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 5508c3397039a1a70c07f1dc5f29e06bd02234a0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357610"
---
# <a name="appendix-a-dynamic-access-control-glossary"></a>Anhang A: Dynamisches Access Control Glossar

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Im folgenden finden Sie eine Liste der Begriffe und Definitionen, die im Szenario für dynamische Access Control enthalten sind.  
  
|Begriff|Definition|  
|--------|--------------|  
|Automatische Klassifizierung|Klassifizierung, die auf der Grundlage von Klassifizierungs Eigenschaften erfolgt, die durch von einem Administrator konfigurierte Klassifizierungsregeln bestimmt werden.|  
|CAPID|ID der zentralen Zugriffs Richtlinie. Diese ID verweist auf eine bestimmte zentrale Zugriffs Richtlinie und wird verwendet, um auf die Richtlinie aus der Sicherheits Beschreibung von Dateien und Ordnern zu verweisen.|  
|Zentrale Zugriffs Regel|Eine Regel, die eine Bedingung und einen Zugriffs Ausdruck enthält.|  
|Zentrale Zugriffs Richtlinie|Richtlinien, die in Active Directory erstellt und gehostet werden.|  
|Anspruchs basierte Zugriffs Steuerung|Ein Paradigma, das Ansprüche verwendet, um Zugriffs Steuerungs Entscheidungen für Ressourcen zu treffen.|  
|Klassifizierung|Der Prozess der Bestimmung der Klassifizierungs Eigenschaften von Ressourcen und Zuweisen dieser Eigenschaften zu den Metadaten, die den Ressourcen zugeordnet sind. Siehe auch Ref automaticclassification \h \\ * MERGEFORMAT Automatic Classification, Ref eritedclassification \h \\ @ no__t-2 MERGEFORMAT geerbt Classification und ref manualclassification \h \\ @ no__t-4 MERGEFORMAT Manual Ordnung.|  
|Geräteanspruch|Ein Anspruch, der dem System zugeordnet ist.  Mit Benutzer Ansprüchen ist Sie im Token eines Benutzers enthalten, der versucht, auf eine Ressource zuzugreifen.|  
|Freigegebene Zugriffs Steuerungs Liste (DACL)|Eine Zugriffs Steuerungs Liste, die Vertrauens nehmer identifiziert, denen der Zugriff auf eine Sicherungs fähige Ressource gestattet oder verweigert wird. Er kann nach Ermessen des Ressourcen Besitzers geändert werden.|  
|Ressourcen Eigenschaft|Eigenschaften (z. b. Bezeichnungen), die eine Datei beschreiben und Dateien mithilfe der automatischen Klassifizierung oder manuellen Klassifizierung zugewiesen werden. Dazu gehören: Sensitivität, Projekt und Beibehaltungs Dauer.|  
|Ressourcen-Manager für Dateiserver|Eine Funktion des Windows Server-Betriebssystems, die die Verwaltung von Ordner Kontingenten, Dateiüberprüfung, Speicher Berichten, Datei Klassifizierungs-und Datei Verwaltungs Aufträgen auf einem Datei Server ermöglicht.|  
|Ordnereigenschaften und-Bezeichnungen|Eigenschaften und Bezeichnungen, die einen Ordner beschreiben und manuell von Administratoren und Ordner Besitzern zugewiesen werden. Diese Eigenschaften weisen den Dateien innerhalb dieser Ordner Standardeigenschaftswerte zu, z. b. Geheimhaltung oder Abteilung.|  
|Gruppenrichtlinie|Eine Reihe von Regeln und Richtlinien, mit denen die Arbeitsumgebung von Benutzern und Computern in einer Active Directory Umgebung gesteuert wird.|  
|Near Real Time Classification|Automatische Klassifizierung, die kurz nach dem Erstellen oder Ändern einer Datei ausgeführt wird.|  
|Near Real-Time File Management Tasks|Datei Verwaltungsaufgaben, die kurz nach ausgeführt werden (eine Datei wird erstellt oder geändert. Diese Aufgaben werden durch die Near Real-Time-Klassifizierung ausgelöst.|  
|Organisationseinheit (OU)|Ein Active Directory Container, der hierarchische logische Strukturen innerhalb einer Organisation darstellt. Dies ist der kleinste Bereich, auf den Gruppenrichtlinie Einstellungen angewendet werden.|  
|Secure-Eigenschaft|Eine Klassifizierungs Eigenschaft, der die Autorisierungs Laufzeit Vertrauen kann, damit Sie zu einem bestimmten Zeitpunkt über die Ressource verfügt. In der Anspruchs basierten Zugriffs Steuerung wird eine sichere Eigenschaft, die einer Ressource zugewiesen ist, als Ressourcen Anspruch behandelt.|  
|Sicherheits Beschreibung|Eine Datenstruktur, die Sicherheitsinformationen enthält, die einer Sicherungs fähigen Ressource zugeordnet sind, z. b. Zugriffs Steuerungs Listen.|  
|Definitions Sprache für Sicherheits Deskriptoren|Eine Spezifikation, die die Informationen in einer Sicherheits Beschreibung als Text Zeichenfolge beschreibt.|  
|Staging-Richtlinie|Eine zentrale Zugriffs Richtlinie, die noch nicht wirksam ist.|  
|System-Zugriffs Steuerungs Liste (SACL)|Eine Zugriffs Steuerungs Liste, die die Arten von Zugriffsversuchen durch bestimmte Vertrauens nehmer angibt, für die Überwachungsdaten Sätze generiert werden müssen.|  
|Benutzer Anspruch|Attribute eines Benutzers, die im Sicherheits Token des Benutzers bereitgestellt werden. Dazu gehören: Abteilung, Unternehmen, Projekt und Sicherheit.  Informationen im Benutzer Token von Systemen vor Windows Server 2012, z. b. die Sicherheitsgruppen, denen der Benutzer gehört, können auch als Benutzer Ansprüche angesehen werden. Einige Benutzer Ansprüche werden über Active Directory bereitgestellt, und andere werden dynamisch berechnet, z. b. ob der Benutzer sich mit einer Smartcard angemeldet hat.|  
|Benutzer Token|Ein Datenobjekt, mit dem ein Benutzer und die Benutzer Ansprüche und Geräteansprüche identifiziert werden, die diesem Benutzer zugeordnet sind. Sie wird verwendet, um den Zugriff des Benutzers auf Ressourcen zu autorisieren.|  
  
## <a name="see-also"></a>Siehe auch  
[Dynamische Zugriffsteuerung: Szenarioübersicht](Dynamic-Access-Control--Scenario-Overview.md)  
  



---
description: Implement a user story
---

## Zweck
Strukturierter Workflow von einem initialen Input bis zu einer freigegebenen Umsetzungsplanung – mit klaren Feedback-Loops und Freigabe-Gates. Arbeite Schritt für Schritt. Lasse keinen Schritt aus. Starte bei Schritt 1

1. Create user story

2. Refine user story

3. Approval gate loop:
   - Frage den User explizit:
     - „User Story freigeben? (JA / Änderungen)“
   - Bei Änderungen:
     - Feedback einarbeiten
     - Zurück zu Schritt 1
   - Bei JA:
     - User Story ist final → weiter zu Phase 2
    Loop-Regel:  
    Diese Phase wird so lange wiederholt, bis die User Story final freigegeben ist.

4. Plan user story

5. Approval gate loop:  
   - Frage den User explizit:
     - „Implementierungsplan freigeben? (JA / Änderungen)“
   - Bei Änderungen:
     - Feedback einarbeiten
     - Zurück zu Schritt 4
   - Bei JA:
     - Planung ist final → OK für Implementierung
    Loop-Regel:  
    Diese Phase wird so lange wiederholt, bis der Implementierungsplan freigegeben ist.

## Ergebnis
- Final freigegebene User Story
- Final freigegebener Implementierungsplan inkl. Testplanung
- Klare Freigabe für die anschließende Implementierung
---
name: create-user-story
description: When the user ask to create a user story, this skill will be used to create a user story.
---

## Zweck
Dieser Skill erstellt entwicklungsreife, fachlich saubere User Stories nach anerkannten Best Practices (INVEST, DoR, Gherkin), geeignet für Scrum- und Kanban-Teams.

## Rolle
Du agierst als erfahrener Product Owner / Business Analyst mit starkem Domänen- und Technikverständnis.

## Verbindliche Schritte
1. Problem vor Lösung  
   - Verstehe Ziel, Nutzerrolle und fachlichen Mehrwert  
   - Triff keine stillschweigenden Annahmen  

2. User Story Format (zwingend)  
   Als <konkrete Nutzerrolle>  
   möchte ich <klar abgegrenzte Fähigkeit>  
   damit <konkreter fachlicher Nutzen>

3. Akzeptanzkriterien  
   - Immer im Gherkin-Format  
   - Fachlich, nicht technisch  
   - Vollständig testbar  

4. Qualitätskriterien (INVEST)  
   - Independent  
   - Negotiable  
   - Valuable  
   - Estimable  
   - Small  
   - Testable  

5. Scope-Disziplin  
   - Eine Story = ein fachliches Ziel  
   - Keine Sammelstories  
   - Keine UI- oder Implementierungsdetails  

## Ausgabeformat
User Story:  
Als …  
möchte ich …  
damit …

Akzeptanzkriterien:  
Given …  
When …  
Then …

Business Rules / Fachliche Hinweise:  
- …

Abhängigkeiten & Offene Fragen:  
- …

## Rückfragen-Regel
Wenn für eine saubere Story Informationen fehlen:  
- Maximal 3 präzise Rückfragen stellen  
- Keine Story auf unklaren Annahmen formulieren  
- Unvermeidbare Annahmen explizit kennzeichnen  

## Qualitätsprüfung vor Ausgabe
- Nutzen eindeutig erkennbar  
- Story ist schätzbar  
- Tester können ohne Rückfragen testen  
- Entwickler verstehen was, nicht wie  

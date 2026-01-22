---
trigger: model_decision
---

# Rule: Testing Is Mandatory

Jede Änderung am Code – unabhängig davon, ob sie aus einer User Story, einem Bugfix, einem Refactoring oder einer technischen Aufgabe entsteht – muss Tests berücksichtigen.

- Jede geplante oder vorgeschlagene Code-Änderung erfordert eine explizite Aussage zur Teststrategie.
- Funktionale Änderungen dürfen nur erfolgen, wenn passende Tests neu erstellt oder bestehende Tests angepasst werden.
- Änderungen am Verhalten bestehender Komponenten machen eine Anpassung der zugehörigen Tests zwingend erforderlich.
- Refactorings müssen durch bestehende oder ergänzte Tests abgesichert sein.
- Es dürfen keine Implementierungspläne, Architekturänderungen oder Code-Vorschläge gemacht werden, ohne die Auswirkungen auf Tests zu benennen.

Tests müssen im selben Stil und nach den gleichen Patterns implementiert werden wie die bestehenden Tests im Repository:
- Nutze dieselben Test-Frameworks, Libraries, Namenskonventionen, Fixture-/Setup-Patterns und Ordnerstrukturen.
- Orientiere dich an bestehenden Beispieltests in der betroffenen Domäne/Schicht.
- Wenn keine passenden Tests existieren, schlage die geringste konsistente Erweiterung der bestehenden Teststruktur vor (ohne neue Frameworks einzuführen), und begründe kurz warum.

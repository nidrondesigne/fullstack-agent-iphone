# Agent Local — jämförande källstudie och byggplan
Datum: 2026-11-22

## Verifierade App Store-källor
1. Jarvis5.0 — https://apps.apple.com/se/app/jarvis5-0/id6802474039 — Michael Valaris. Kamera-HUD, Apple Vision för analys av bildflöde, tryck för manuell mållåsning, syntetiskt tal. Det är en underhållningsapp, inte verifierad generell AI-agent. Proprietär kod ej tillgänglig.
2. Jarvis AI-assistent — https://apps.apple.com/se/app/jarvis-ai-assistent/id6787468112 — Himanshi Kapoor enligt butikssidan. Röstkonversationer, bestående minne, påminnelser, kalender och webbsökning. Kräver egen Google Gemini API-nyckel; är därför inte ett offline-referensexempel. Proprietär kod ej tillgänglig.
3. Chat Svenska — https://apps.apple.com/se/app/chat-svenska/id6446446867 — svenskspråkig AI-chatt, textgenerering, frågor och skrivstöd. Ingen verifierad lokal modell. Proprietär kod ej tillgänglig.

## Öppna referenser
- Jared Rhodenizers installerare: https://github.com/jaredrhod/fullstack-agent
- Minne: https://github.com/jaredrhod/ai-memory-vault
- Röst: https://github.com/jaredrhod/backtalk
- Ansikte: https://github.com/jaredrhod/ai-visualizer
- Händer: https://github.com/jaredrhod/barehands
Originalet använder Claude Code som agenthjärna och är inte en offline-iPhone-app. Projektens licenser måste respekteras vid direkt kodåteranvändning. Vår kod är en ny implementation inspirerad av funktionsuppdelningen.

## Gemensam arkitektur
1. Agentkärna: lokal språkmodell (WebLLM i PWA, senare Apple Foundation Models i native app när tillgängligt).
2. Agentverktyg: deterministisk kalkylator, lokala anteckningar, framtida uppgifter och påminnelser.
3. Minne: idag localStorage med JSON-backup; migrera till IndexedDB med versionsschema och sökning.
4. Tal in: MediaRecorder + lokal Whisper via Transformers.js; kräver första modellnedladdning och verifiering på Safari.
5. Tal ut: speechSynthesis, offline-röster ej verifierade.
6. Visuell agent: Canvas och tillståndsbuss (idle, listening, thinking, speaking).
7. Vision: camera getUserMedia och lokal HUD med manuell mållåsning; automatisk objektdetektion kräver separat lokal modell.
8. Handgester: framtida MediaPipe Hands-prototyp efter iOS-benchmark.
9. Integritet: inga ljud- eller kamerabilder skickas till vår server; tredjeparts modell- och skriptvärdar används vid nedladdning. Webbläsarlagring kan rensas av iOS.

## Verifieringskrav
- Testa alla funktioner på faktisk iPhone.
- Testa flygplansläge först efter att alla beroenden laddats ner och cachats.
- Verifiera att minnen kvarstår efter stängning och omstart.
- Kontrollera att transkribering fungerar för svenska.
- Kontrollera modellens svarskvalitet och felhantering.
- Verifiera att kamera stängs och strömmens spår stoppas.
- För native app: undersök Xcode Cloud, signering och iOS-begränsningar utan Mac.

## Status
Agent.html: minne, kalkylator, ansikte, uppläsning, experimentell Whisper, experimentell WebLLM.
Vision.html: kamera-HUD och manuell mållåsning.
Ingen automatisk objektigenkänning, inga riktiga systempåminnelser, ingen handspårning och ingen verifierad offline-AI ännu.

# Sovereign Development Rules
- **Data Classification:** All files in `/data/` and `/logic/legal_engine/` are CLASS 1 (Sovereign).
- **Prohibition:** NEVER send CLASS 1 file contents or screenshots of CLASS 1 data to any external LLM provider (Gemini/Claude).
- **Cloud Restriction:** Do not send user property photos or specific planning logic queries to the cloud. All Legal Logic (e.g., Party Wall Act 1996, Slough RESPD) must be handled by the local sovereign LLM (Ollama/Llama 3.1).
- **Tool Selection:** For any task involving "Legal Logic," "Planning Compliance," or "Structural Analysis," you MUST use the localized models and engines.
- **Privacy:** When testing the UI with property images, use the local vision model only. Do not use cloud-based browser verification for pages displaying this sensitive data.
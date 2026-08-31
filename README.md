<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:1a1a2e,100:e94560&height=120&section=header&text=Ankit%20Kumar&fontSize=42&fontColor=eaeaea&fontAlignY=65&animation=fadeIn" width="100%"/>

### Builder · AI Enthusiast · Computer Vision Nerd

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ankit-kumar-10o26/)
[![Instagram](https://img.shields.io/badge/Instagram-E4405F?style=flat-square&logo=instagram&logoColor=white)](https://www.instagram.com/_.ken_k_/)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:ankitmukesh2003@email.com)

</div>

---

## 👋 About Me

I'm a self-driven developer who builds things at the intersection of AI, computer vision, and full-stack software. I care about projects that solve real problems — not just demos. Whether it's a face-authenticated vault, a gesture-controlled mouse, or a local RAG assistant, I build to learn and ship to grow.

- 🎓 **MCA graduate (2026), Graphic Era University** — currently looking for my first full-time role
- 🎯 **Applying across two tracks:** AI/ML Engineer and Full Stack Developer
- 🔭 **Currently building:** Stacks — a full-stack RAG chatbot (React, Express, MongoDB, Qdrant, Ollama)
- 🌱 **Exploring next:** relational database design, PostgreSQL, and real-time systems (WebSockets)
- 💬 **Ask me about:** OpenCV, RAG pipelines, PyQt5, or anything computer vision
- ⚡ **Philosophy:** *"The only way to learn is to build."*

---

## 🛠️ Tech Stack

**Languages**

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)
![C](https://img.shields.io/badge/C-00599C?style=flat-square&logo=c&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)

**Full Stack**

![React](https://img.shields.io/badge/React-61DAFB?style=flat-square&logo=react&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=nodedotjs&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white)

**AI / ML / Computer Vision**

![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=flat-square&logo=opencv&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=flat-square&logo=tensorflow&logoColor=white)
![MediaPipe](https://img.shields.io/badge/MediaPipe-0097A7?style=flat-square&logo=google&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square)
![Ollama](https://img.shields.io/badge/Ollama-000000?style=flat-square)
![Qdrant](https://img.shields.io/badge/Qdrant-DC244C?style=flat-square)

**Tools & Platforms**

![Git](https://img.shields.io/badge/Git-F05032?style=flat-square&logo=git&logoColor=white)
![VS Code](https://img.shields.io/badge/VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)
![PyQt5](https://img.shields.io/badge/PyQt5-41CD52?style=flat-square&logo=qt&logoColor=white)

---

## 🚀 Featured Projects

### 🧵 Stacks — Full-Stack RAG Chatbot
> **React · Express/Node.js · Ollama (Gemma) · Qdrant · MongoDB**

A solo-built, full-stack Retrieval-Augmented Generation chatbot with real conversation persistence — not just a wrapped LLM call.

- **Pipeline:** query → embedded via Qwen3-Embedding (Ollama) → similarity search against Qdrant → retrieved chunks injected into a prompt template → Gemma (Ollama) generates the grounded answer
- **Auth:** bcrypt password hashing + express-session, with sessions persisted in MongoDB via connect-mongo (survives server restarts, unlike in-memory sessions)
- **Vector store:** Qdrant chosen over an embedded store for its dedicated server, filtering, and payload indexing — the right call for something meant to scale past a single-user toy
- Lazy conversation persistence (a chat isn't written to MongoDB until there's an actual exchange), sidebar with rename/delete, theme persistence
- Straight retrieval-then-generation — no tool calling or multi-step reasoning, so this is RAG, not an agent (see VoiceFlow below for the agentic example)

---

### 🛡️ SecureVault
> **Python · PyQt5 · face_recognition · dlib · Cryptography · SQLite**

A desktop security app combining face-recognition auth (with blink-based liveness detection) and AES file encryption.

- **Auth flow:** primary auth is live face matching via `face_recognition`/dlib, with **liveness enforced by eye-blink detection** (Eye Aspect Ratio via `scipy.spatial.distance`) so a static photo can't unlock it — falls back to a bcrypt-verified password after repeated failures
- **Key derivation chain:** vault password → PBKDF2-HMAC-SHA256 (480,000 iterations) → 256-bit key → converted to a Fernet key (AES-128-CBC + HMAC-SHA256, so tampering is detectable, not just unreadable)
- **Nothing sensitive touches disk:** only the salt persists — the derived key lives in memory with a 1-hour TTL and is zeroed on logout
- Intruder capture (unknown faces photographed + timestamped) and a full SQLite audit trail of every auth/encryption event
- Packaged as a standalone Windows `.exe` via PyInstaller

---

### 🤟 Real-Time Sign Language to Speech System
> **Python · FastAPI · React · MediaPipe · TensorFlow · LangChain · Ollama**

A real-time, full-stack pipeline that captures hand gestures via webcam and converts them into spoken English sentences.

- **Representation:** each frame is a 126-dim vector — 21 landmarks × (x,y,z) × 2 hands, zero-padded when a hand isn't visible, keeping sequence shape consistent for the model
- **Why LSTM, not a single-frame classifier:** signs unfold over time (30-frame sequences), so the model needs to learn motion, not just a static pose
- **Full-stack, not desktop:** originally a PyQt5 app; now a FastAPI backend streams inference over WebSockets (`/ws/infer`, `/ws/collect`) to a React frontend that owns the webcam via `getUserMedia` — the model, MediaPipe, and LLM logic all run server-side, untouched
- **Graceful degradation throughout:** LLM grammar correction (LangChain + Ollama/Gemma) falls back to a rule-based capitalizer if Ollama is unreachable; facial-emotion detection falls back from DeepFace to geometric heuristics if DeepFace isn't installed — the LLM is an enhancement, never a hard dependency
- Offline TTS via pyttsx3 with gTTS fallback, synthesized server-side and streamed back as audio for browser playback
- Full pipeline included: data collection → preprocessing → training → live inference
- Reported 100% test accuracy reflects a small, custom-collected dataset with limited diversity (few signers, controlled lighting) — a strong proof of pipeline correctness, not yet a claim of real-world generalization

---

### 🎙️ VoiceFlow — AI Voice Assistant
> **Python · LangChain · Ollama · pyttsx3 · SpeechRecognition**

A local, agentic voice assistant with a real tool-dispatch loop, not scripted commands.

- **Agent loop:** speech → text (Google STT) → `ChatOllama` with `bind_tools()` → the model itself decides whether the request needs a tool call and which one → the tool actually executes (opens a URL, launches an app, runs a search) → result returned to the model as a `ToolMessage` → final response spoken via TTS
- This decision step — the model choosing *whether and which* tool to invoke — is what makes this genuinely agentic, as opposed to Stacks' fixed retrieve-then-generate flow
- Supports local Ollama models (llama3.2, mistral, phi3) and cloud models; cloud requests leave the device, local ones don't — documented and left as a deliberate user choice
- Continuous or single-shot listening modes with ambient noise calibration; hot-swappable models at runtime

---

### 📄 DocMind AI — RAG Document Q&A
> **Python · LangChain · Ollama · ChromaDB · Tkinter**

A fully local RAG application — upload a document, ask questions, get source-attributed answers, no data leaves the device.

- **Same category as Stacks, different implementation:** ChromaDB (embedded, single-user) instead of Qdrant, a Tkinter desktop GUI instead of a web stack, and no multi-user accounts or persisted history — a lighter-weight tool by design, not a cut corner
- Supports PDF, DOCX, TXT, CSV, and Markdown
- Chunk size, overlap, and Top-K retrieval are all user-configurable from the UI, not hardcoded constants
- Hot-swappable Ollama chat models without re-indexing the document store

---

### 🖐️ Hand Gesture Mouse Controller
> **Python · MediaPipe · TensorFlow · PyAutoGUI**

Full mouse control via webcam hand gestures — no extra hardware required.

- MediaPipe extracts 21 hand landmarks (63 features) feeding a custom TensorFlow dense classifier across six gesture classes
- **Landmarks are normalized relative to the wrist**, making the model invariant to where your hand is in frame or how close it is to the camera
- **Gesture smoothing via a ring buffer** — a single frame's prediction is noisy, so a gesture is only confirmed once several consecutive frames agree, keeping the cursor stable
- Single-frame classification (dense network, no memory across time) — a useful contrast with the sign language project's sequence-based LSTM, since mouse gestures are static poses rather than motions

---

### 🛡️ Face Recognition Security System
> **Python · OpenCV · Tkinter**

A real-time access-control system using OpenCV's LBPH (Local Binary Patterns Histograms) algorithm — a classical, pre-deep-learning face recognition technique that encodes local texture patterns and compares histograms.

- Fast and GPU-free, but more lighting-sensitive and less accurate than the dlib-based deep embeddings used in AI SecureVault — the earlier, simpler project that led directly into building SecureVault's more robust approach
- Register multiple users with live face capture; real-time recognition with confidence scoring
- GRANTED / DENIED access log with a management dashboard for adding/removing registered faces

---

### 🧩 Crossword Puzzle Game
> **C · GTK4**

A desktop crossword game built around a **Trie (prefix tree)** for the word/hint engine — the right data structure for fast prefix-based word lookup, which is exactly what generating a crossword grid requires. Includes role-based (student/teacher) access control and a persistent word database.

---

## 📊 Currently Working Toward

- [ ] A relational-database-backed project (PostgreSQL) to round out full-stack applications
- [ ] Real-time systems using WebSockets
- [ ] Deeper hands-on experience with fine-tuning (LoRA/QLoRA)

---

## 📬 Connect

I'm always open to interesting project ideas, collaborations, or a good tech conversation.

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/ankit-kumar-10o26/)
[![Instagram](https://img.shields.io/badge/Instagram-Follow-E4405F?style=flat-square&logo=instagram&logoColor=white)](https://www.instagram.com/_.ken_k_/)
[![Email](https://img.shields.io/badge/Email-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:ankitmukesh2003@email.com)
[![Portfolio](https://img.shields.io/badge/Portfolio-Visit-1a1a2e?style=flat-square&logo=vercel)](https://portfolio-ankitk26-projects.vercel.app/)

---

<div align="center">
<img src="https://capsule-render.vercel.app/api?type=waving&color=0:e94560,100:1a1a2e&height=80&section=footer" width="100%"/>
</div>

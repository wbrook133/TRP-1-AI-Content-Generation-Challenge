## 📁 src/ai_content/

### 🔹 core/
Contains the fundamental building blocks of the system.

- **provider.py**  
  Defines the base interface for AI providers.

- **registry.py**  
  Handles registration and management of providers or pipelines.

- **job_tracker.py**  
  Manages the state, lifecycle, and tracking of generation jobs.

- **result.py**  
  Defines the structure and data model for generation results.

---

### 🔹 pipelines/
Defines workflows for generating different types of content.

- **base.py**  
  Abstract base class for all content generation pipelines.

- **music.py**  
  Pipeline responsible for music generation.

- **video.py**  
  Pipeline responsible for video generation.

- **full.py**  
  Comprehensive pipeline combining multiple modalities (e.g., text, audio, video).

---

### 🔹 providers/
Implementations for specific AI service providers.

- **google/**  
  Integration with Google AI models (e.g., Gemini, VideoFX).

- **aimlapi/**  
  Integration with external AI/ML APIs.

- **kling/**  
  Integration with Kling AI services.

---

### 🔹 integrations/
External platform and service connectors.

- **youtube.py**  
  Handles YouTube-related functionality such as uploads or searches.

- **archive.py**  
  Provides archival or long-term storage integration.

- **media.py**  
  General utilities for handling and processing media files.

---

### 🔹 cli/
Command-line interface (CLI) entry points for interacting with the system.

---

### 🔹 config/
Configuration management and environment-specific settings.

---

### 🔹 utils/
General-purpose utility functions shared across the project.

## 🧩 Provider Architecture

Providers are organized using a **Protocol-based design** combined with a **Decorator-driven Registry**.  
This approach enables flexible, decoupled provider implementations without rigid inheritance hierarchies.

---

## 1️⃣ Base Interfaces  
📍 `src/ai_content/core/provider.py`

Providers must implement **one of three Protocol interfaces**, enabling duck-typing rather than strict inheritance.

### 🎵 MusicProvider
Used for music generation.

- **Methods**
  - `generate(...)`
- **Properties**
  - `supports_vocals`
  - *(other capability flags as needed)*

---

### 🎬 VideoProvider
Used for video generation.

- **Methods**
  - `generate(...)`
- **Properties**
  - `supports_image_to_video`
  - *(other video-specific capabilities)*

---

### 🖼️ ImageProvider
Used for image generation.

- **Methods**
  - `generate(...)`
- **Properties**
  - `aspect_ratio`
  - *(other image-related settings)*

> ⚙️ This Protocol-based (duck-typing) approach provides flexibility and avoids deep inheritance chains.

---

## 2️⃣ Provider Registration  
📍 `src/ai_content/core/registry.py`

A **singleton `ProviderRegistry`** manages all registered providers.

### 🔹 Registration
Providers self-register using decorators:

```python
@ProviderRegistry.register_music("provider_name")

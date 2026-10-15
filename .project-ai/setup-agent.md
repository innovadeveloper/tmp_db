# Configuración del agente

> Proyecto: `DBProjects`  
> Stack detectado: desconocido

## 1. opencode.json

Copia este archivo en la **raíz del proyecto** y abre OpenCode ahí.
Incluye el modelo, el proveedor Ollama y Serena (MCP + LSP) en un solo bloque.

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "llamacpp/qwen3.6-35b",
  "plugin": [
    "opencode-ollama-toolcall-proxy"
  ],
  "instructions": [
    ".project-ai/notes.md"
  ],
  "provider": {
    "linux": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Ollama Linux",
      "options": {
        "baseURL": "http://178.156.133.161:9008/v1"
      },
      "models": {
        "qwen3:14b-20k": {
          "name": "Qwen3 14B 20K (Linux)",
          "limit": {
            "context": 20480,
            "output": 4096
          }
        },
        "qwen3:14b-16k": {
          "name": "Qwen3 14B 16K (Linux)",
          "limit": {
            "context": 16384,
            "output": 4096
          }
        }
      }
    },
    "mac": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "Ollama Mac",
      "options": {
        "baseURL": "http://localhost:11434/v1"
      },
      "models": {
        "qwen3-coder:30b-64k": {
          "name": "Qwen3 Coder 30B 64K (Mac)",
          "limit": {
            "context": 65536,
            "output": 8192
          }
        }
      }
    },
    "llamacpp": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "llama.cpp Linux",
      "options": {
        "baseURL": "http://192.168.0.50:8080/v1"
      },
      "models": {
        "qwen3-coder-30b": {
          "name": "Qwen3 Coder 30B MoE (Linux)",
          "limit": {
            "context": 65536,
            "output": 8192
          }
        },
        "qwen3.6-35b": {
          "name": "Qwen3.6 35B MoE (Linux)",
          "limit": {
            "context": 65536,
            "output": 8192
          }
        }
      }
    }
  },
  "lsp": true,
  "mcp": {
    "serena": {
      "command": "uvx",
      "args": [
        "serena",
        "--project-root",
        "/Users/kenny/PropertyProjects/DBProjects"
      ],
      "enabled": true
    }
  },
  "permission": {
    "edit": "ask",
    "bash": {
      "grep *": "allow",
      "find *": "allow",
      "ls *": "allow",
      "git diff*": "allow",
      "git status*": "allow",
      "*": "ask"
    }
  }
}
```

> Para usar el nodo N2 cambia `model` a `ollama/qwen2.5-coder:14b` y `url` a `http://localhost:11434`.

## 2. Prerrequisitos

### Stack genérico

Serena arrancará sin LSP específico. Para mejor soporte instala el LSP
de tu lenguaje y añade `--lsp-binary <nombre>` a los args de Serena.

## 3. Verificaciones rápidas

```bash
# N1 — http://localhost:11434
curl -s http://localhost:11434/api/tags | python3 -m json.tool | head -20

# N2 — http://localhost:11434
curl -s http://localhost:11434/api/tags | python3 -m json.tool | head -20

# Modelos cargados
curl -s http://localhost:11434/api/ps
```

Si los nodos no responden: `OLLAMA_HOST=0.0.0.0 ollama serve`.

## 4. Contexto bajo demanda

```bash
# Genera un paquete de contexto para pegar en cualquier chat:
project-ai context "cómo funciona el auth" --path /Users/kenny/PropertyProjects/DBProjects
```

## 5. Schema SQL

El proyecto tiene un esquema SQL documentado en `.project-ai/schema-map.md`.
Para documentar cada tabla y función con Ollama:

```bash
project-ai schema /Users/kenny/PropertyProjects/DBProjects --document
```

Los documentos se guardan en `.project-ai/schema/tablas/` y `.project-ai/schema/funciones/`.
Inclúyelos como contexto adicional en tu chat con OpenCode.

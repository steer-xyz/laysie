# 🌱 laisy

**Zero-friction digital garden framework powered by AI**

Transform scattered thoughts, voice notes, links, and media into a coherent, living website that grows with you. Built on GitHub Actions for fully autonomous content creation and site maintenance.

[![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-blue?logo=github-actions&logoColor=white)](https://github.com/features/actions)
[![AI Powered](https://img.shields.io/badge/AI-Powered-purple?logo=openai&logoColor=white)](https://openai.com)
[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> "Drop thoughts anywhere, laisy turns them into a coherent, living website that grows with you."

## ✨ Features

- **🎤 Voice to Blog**: Record voice notes → automatic transcription → polished blog posts
- **🔗 Smart Bookmarks**: Share links → structured content with key takeaways
- **🤖 AI Agent**: Learns your writing style and automatically cross-links content
- **📧 Email Gateway**: Send thoughts via email → instant website updates
- **🚀 Zero Setup**: Working site in 2 minutes with GitHub template
- **📱 Progressive Web App**: Capture content anywhere, sync automatically
- **🎨 Customizable**: From no-code templates to full plugin development

## 🎯 Use Cases

### For Researchers
- **Paper Ingestion**: Automatically process arXiv papers into structured notes
- **Citation Management**: Auto-generated cross-references and bibliographies
- **Literature Reviews**: AI-assisted synthesis of research themes

### For Indie Developers  
- **Project Showcases**: Auto-generated from GitHub releases and README files
- **Changelog Automation**: Convert git commits into readable release notes
- **Technical Writing**: Voice notes become polished technical blog posts

### For Visual Artists
- **Portfolio Generation**: EXIF-aware photo galleries with AI captions
- **Creative Process**: Document work-in-progress with voice and images
- **Exhibition Archives**: Structured documentation of shows and projects

### For Content Creators
- **Multi-Platform Publishing**: One source of truth for all content
- **Audience Building**: SEO-optimized posts from casual thoughts
- **Content Repurposing**: Transform videos/podcasts into multiple formats

## 🏗️ Proposed Architecture

```
Input Sources → GitHub Actions → AI Processing → Living Website
     ↓               ↓              ↓              ↓
Voice Notes     Ingest Action   Claude/Whisper   Static Site
Email/Links  →  Process Action → Content Enhancement → Auto-Deploy
PWA/CLI         Pull Requests   Style Learning     Git History
```

### Core Components

- **Ingest Layer**: Receives content from multiple sources (CLI, email, PWA)
- **Processing Engine**: AI-powered content enhancement and cross-linking
- **Agent Memory**: Learns your voice and maintains consistency over time
- **Deployment**: Automated GitHub Pages or Cloudflare Pages publishing

## 📋 Content Types

laisy automatically detects and formats different content types:

| Input | Output | Features |
|-------|--------|----------|
| 🎤 Voice Notes | Blog Posts | Whisper transcription → Claude enhancement |
| 🔗 URLs | Content Archive | Auto-extract metadata, summaries, takeaways |  
| 📊 Research Papers | Structured Notes | Citation parsing, key insights, cross-links |
| 📸 Images | Gallery Pages | EXIF metadata, AI captions, optimization |
| 💭 Quick Thoughts | Journal Entries | Style-consistent formatting and tagging |

## 🔌 Input Methods

### CLI
```bash
laisy record --mic 90s              # Voice recording
laisy link https://example.com      # Bookmark with summary
laisy note "Random thought..."       # Quick text entry
laisy upload photo.jpg              # Image with auto-caption
```

### Progressive Web App
- 📱 One-tap voice recording with live transcription
- ✍️ WYSIWYG editor with slash commands (`/youtube`, `/tag`)
- 📴 Offline support with sync when connected

## 🧠 AI Agent Learning

idea is to learn from you:

### Style Adaptation
- **Voice Analysis**: Learns from your existing content
- **Feedback Loop**: Incorporates your edits and preferences  
- **Cross-Linking**: Automatically connects related ideas
- **Historical Context**: Maintains consistency across all content

### Project Structure (something like this? idk)
```
laisy/
├── .github/workflows/     # GitHub Actions for processing
├── laisy.toml            # Configuration
├── prompts/              # AI prompt templates
├── theme/                # Hydro theme + overrides
├── content/              # Generated markdown
│   ├── inbox/           # Staging area
│   ├── vignettes/       # Blog posts
│   └── archive/         # Bookmarks & references
├── profile.yml           # Your writing style & preferences
└── assets/              # Media files
```

## 🤝 Community
twitter/disc maybe

## 🗺️ Roadmap

### v1.0 (working on it)
- ✅ Core ingestion and processing
- ✅ GitHub Actions workflow
- ✅ Basic AI enhancement
- ✅ Static site generation

### v1.1 (next up)
- 🔄 Plugin API v1
- 🔄 Advanced cross-linking
- 🔄 Multi-language support
- 🔄 Enhanced mobile PWA

### v2.0 (some day)
- 📋 Collaborative gardens
- 📋 Real-time collaboration
- 📋 Advanced analytics
- 📋 Enterprise features

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

## 🌟 Contributing

Dm me if you are interested [@steerdev](https://x.com/steerdev) for guidelines.

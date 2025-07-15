# laisy Project Context Guide

## Project Overview
laisy is a zero-friction digital garden framework that transforms scattered thoughts, links, and media into a coherent, living website. Built on GitHub Actions, it enables fully autonomous content creation and site maintenance through agentic workflows.

**Core Value Proposition**: "Drop thoughts anywhere, laisy turns them into a coherent, living website that grows with you."

## Architecture Philosophy

### Design Principles
- **Zero-Friction**: Voice notes, links, and thoughts become polished content automatically
- **Event-Driven**: GitHub Actions handle ingestion, processing, and deployment
- **Git-Native**: Full transparency with git history of all changes
- **Hackable**: From no-code template to full plugin customization
- **Learning**: Agent adapts to your voice and style over time

### Reference Architecture
```
repo/
├── .github/workflows/
│   ├── ingest.yml      # Receives payloads (issues, email, webhook)
│   ├── process.yml     # Runs Claude/Whisper/etc
│   └── deploy.yml      # Pushes to gh-pages (or Cloudflare Pages)
├── laisy.toml           # Site + agent config
├── prompts/            # Prompt packs for different personas
├── theme/              # Hydro theme with overridable partials
├── content/            # Generated and manual markdown
│   └── inbox/          # Incoming content staging area
├── profile.yml         # User preferences and style guide
└── assets/            # Media files (Git LFS or OCI store)
```

## Content Processing Workflow

### Event Flow
```
Input Source → GitHub App/CLI → Ingest Action → Process Action → Pull Request → Deploy
```

1. **Ingest Action**: Validates input, writes to `content/inbox/{timestamp}.md`
2. **Process Action**: Runs AI enrichment (Whisper, Claude Code, tagging)
3. **Pull Request**: Creates preview with processed content
4. **Deploy Action**: Merges and deploys to live site

### Input Sources

#### A. laisy CLI
```bash
laisy record --mic 90s             # voice note → transcript → blog post
laisy link https://youtu.be/xyz    # bookmark → structured content
laisy note "Thinking about RLHF…"  # raw text → formatted entry
```

#### B. Progressive Web App
- One-tap voice recording with live transcription
- WYSIWYG editor with slash commands (`/youtube <url>`, `/tag ai music`)
- Offline support with IndexedDB sync

#### C. Email Gateway
- Send to `me@laisy.page` → automatic Issue creation
- Attachments land in `assets/` directory

#### D. Browser Integration
- Bookmarklet/extension for current tab + highlights
- Share sheet integration

#### E. Chat Ops
- Slack/Discord slash commands (`/laisy note ...`)

## Product Layers (No-Code → Power-User)

### Layer 1: Baseline "Gold Path"
- **Setup**: `npx laisy-init <site-name>` → working site in 2 minutes
- **Use**: GitHub template repo + App installation

### Layer 2: Configuration
- **File**: `laisy.toml` with feature toggles
- **Examples**: `auto_crosslink = true`, `gallery.resize = 1024`

### Layer 3: Prompt Packs
- **Location**: `prompts/` directory
- **Examples**: `blogger.md`, `academic.md`, `researcher.md`

### Layer 4: Theme Overrides
- **Location**: `theme/partials/`
- **Use**: Drop custom Tailwind components

### Layer 5: Plugin API
- **Languages**: TypeScript or Python
- **Interface**: Implement `onIngest()`, `onProcess()`, `onDeploy()`
- **Examples**: Arxiv auto-fetch, semantic summarization

## Agent Learning System

### User Profile (`profile.yml`)
```yaml
name: "John Steer"
tone: "conversational yet technical"
expertise: ["ai", "engineering", "product"]
pov: "first-person"
reading_level: "technical"
cross_link_style: "contextual"
```

### Style Adaptation
- **Embeddings Index**: DuckDB + pgvector for content similarity
- **Feedback Loop**: Post-merge prompts for style validation
- **Prompt Mixer**: Base + persona + task + recent feedback
- **Historical Context**: RAG retrieval for consistent voice

### Learning Mechanisms
1. **Content Analysis**: Extract patterns from existing posts
2. **User Feedback**: Y/N + comments on generated content
3. **Style Evolution**: Gradual refinement of voice and structure
4. **Cross-Linking**: Automatic connections based on content similarity

## Content Types & Templates

### Vignettes (Blog Posts)
- **Trigger**: Voice notes, long-form thoughts
- **Structure**: Title, intro, main content, reflection
- **Location**: `content/vignettes/`

### Content Archive
- **YouTube Videos**: Title, creator, key takeaways, timestamps
- **Research Papers**: Abstract, relevance, implementation notes
- **Podcasts**: Key quotes, speaker insights, action items
- **Location**: `content/archive/`

### Project Pages
- **Trigger**: GitHub releases, shipped features
- **Content**: Auto-generated from README, tech stack tags
- **Location**: `content/projects/`

### Gallery
- **Trigger**: Photo uploads with EXIF data
- **Processing**: Optimization, AI-generated captions
- **Location**: `content/gallery/`

## Starter Kits & Community

### Researcher Kit
- Paper ingestion from Arxiv, PubMed
- Citation management and cross-referencing
- Automatic literature review generation

### Indie Developer Kit
- Changelog automation from git commits
- Release note generation
- Project showcase templates

### Visual Artist Kit
- Gallery optimization and organization
- EXIF metadata extraction
- Portfolio presentation templates

### Plugin Registry
- Simple JSON index of community plugins
- npm/PyPI packages named `@laisy/plugin-*`
- Installation via `laisy.toml` configuration

## Development Workflow

### Content Creation Process
1. **Input**: Voice, text, link, or media via any interface
2. **Validation**: Schema check and content type detection
3. **Processing**: AI enrichment with user's style and context
4. **Review**: Pull request with preview deployment
5. **Publish**: Merge triggers production deployment

### Agent Context Engineering
- **Deterministic**: Structured prompts with required fields
- **Contextual**: Historical content for style consistency
- **Adaptive**: Feedback incorporation for continuous improvement
- **Transparent**: All processing steps logged and reviewable

### Quality Assurance
- Pre-commit hooks for content validation
- Spell check and grammar verification
- Link verification and SEO optimization
- Responsive design testing

## Configuration Reference

### `laisy.toml` Structure
```toml
[site]
name = "My Digital Garden"
url = "https://garden.example.com"
theme = "hydro"

[agent]
model = "claude-3.5-sonnet"
voice_model = "whisper-large-v3"
auto_crosslink = true
auto_tag = true

[content]
auto_publish = false  # Require manual PR merge
max_voice_length = 300  # seconds

[integrations]
email_gateway = true
pwa_enabled = true
```

### Prompt Engineering
- **System Prompts**: Core behavior and constraints
- **Persona Prompts**: Writing style and voice
- **Task Prompts**: Specific content type instructions
- **Context Prompts**: Historical patterns and preferences

## Security & Privacy

### Data Handling
- **Public Repos**: Framework code, sanitized examples
- **Private Configs**: API keys, personal context
- **Content**: User controls public/private status
- **Processing**: Ephemeral environments, no data retention

### Access Control
- GitHub App permissions for repository access
- API authentication for external integrations
- Webhook validation for security
- Rate limiting and abuse prevention

## MVP Roadmap (12 Weeks)

### Weeks 1-2: Foundation
- Template repository with basic static site
- GitHub Actions for deployment
- Basic CLI for content ingestion

### Weeks 3-4: Ingestion
- Issues API integration
- Content validation and staging
- Basic prompt processing

### Weeks 5-6: AI Processing
- Whisper integration for voice transcription
- Claude Code for content enhancement
- Template-based content generation

### Weeks 7-8: Workflow
- Pull request automation
- Preview deployments
- Configuration system (`laisy.toml`)

### Weeks 9-10: User Experience
- Progressive Web App for content capture
- Enhanced CLI with multiple input modes
- Theme system with customization

### Weeks 11-12: Extensibility
- Plugin API v1
- Community starter kits
- Documentation and examples

## Trade-offs & Design Decisions

### GitHub Issues as Queue
- **Why**: No extra infrastructure, built-in UI and mobile app
- **Limitation**: API rate limits (~5,000 calls/hour)
- **Alternative**: Custom queue system for high-volume users

### Markdown + Static Sites
- **Why**: Diff-friendly, cheap hosting, easy RAG indexing
- **Limitation**: No dynamic features (comments, search)
- **Alternative**: Hybrid approach with serverless functions

### Single Repository
- **Why**: Simpler forks, unified remote, easier management
- **Limitation**: Scaling for multi-tenant SaaS
- **Alternative**: Multi-repo architecture for enterprise

## Monitoring & Observability

### Key Metrics
- Content processing success rate and latency
- User engagement with generated content
- Agent learning effectiveness
- System reliability and uptime

### Error Handling
- Graceful degradation for API failures
- Retry mechanisms with exponential backoff
- Comprehensive logging for debugging
- User notification for processing failures

### Performance Optimization
- Content caching and CDN integration
- Image optimization and lazy loading
- Minimal JavaScript for fast page loads
- Progressive enhancement for features

## Notes for Claude Code

### Execution Context
- Always validate `laisy.toml` configuration before processing
- Maintain consistency with user's established voice and style
- Use historical content for context and cross-linking opportunities
- Follow git commit message conventions for transparency

### Content Processing Guidelines
1. **Input Analysis**: Detect content type and extract metadata
2. **Template Selection**: Choose appropriate format from `prompts/`
3. **Style Application**: Apply user's voice from `profile.yml`
4. **Enhancement**: Add tags, cross-links, and SEO metadata
5. **Validation**: Check output quality and completeness

### Error Recovery
- Fallback to manual processing on AI failures
- Preserve original content in `inbox/` for reprocessing
- Clear error messages with suggested fixes
- Graceful handling of API rate limits

This document serves as the primary context for all Claude Code operations on the laisy project. It should be referenced for consistent behavior and updated as the project evolves.
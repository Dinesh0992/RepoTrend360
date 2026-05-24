# RepoTrend360 — GitHub Repository Explorer & Tech Trends Radar

A comprehensive, interactive dashboard for discovering, monitoring, and analyzing top open-source repositories across 30+ technology categories. Powered by GitHub, Hacker News, Dev.to, and built with zero backend dependencies.

## 📸 Screenshots

### Main Dashboard
![RepoTrend360 Dashboard](https://github.com/Dinesh0992/RepoTrend360/raw/main/image1.png)

### Analytics & Visualizations
![RepoTrend360 Analytics](https://github.com/Dinesh0992/RepoTrend360/raw/main/image2.png)

---

## ✨ Features

### 📚 Repository Discovery
- **30+ curated tech categories**: AI Agents, LLM, ML/MLOps, IoT, Web Dev, DevTools, Security, Blockchain, Data Engineering, Cloud Native, Robotics, Gaming, FinTech, HealthTech, Quantum, AR/VR, Climate, Education, NLP, Audio/Voice, Low-code, Banking, Insurance, Manufacturing, and more
- **Dynamic GitHub Search API** integration with category-specific queries
- **Year-aware filtering** to focus on actively maintained repositories
- **Multi-filter support**: Language, Topic, Creation Year, Growth Rate
- **Smart reclassification** using GitHub topics for accurate categorization

### 📰 News & Releases Hub
- **GitHub Releases API** with intelligent lazy-loading (max 2 selections per group)
- **Hacker News integration** via Algolia API for tech-focused stories
- **GitHub Advisories** for CVE and security alerts
- **Dev.to API** for community discussions and articles
- **Tabbed interface** to switch between company/topic groups

### 📊 Analytics & Insights
- **Trending Strip**: Real-time hot repositories with growth metrics
- **Dominating vs. Emerging Classification**: Identify established vs. rising projects
- **Overview Stats**: Total repositories, language distribution, trending count
- **Interactive Charts**: 
  - Language distribution (pie chart)
  - Stars vs. Forks (scatter plot)
  - Growth trends (line chart)
  - Category breakdown (bar chart)
- **Custom insights panel** with key metrics and recommendations

### 🎨 User Experience
- **Collapsible sidebar** with category navigation and instant search
- **Real-time search** combining local fuzzy matching + GitHub live API lookup
- **4 theme variants**: Dark (default), Light, Ocean, Solarized
- **Responsive design** with mobile-friendly toggle
- **Keyboard shortcuts** for power users (Cmd+K to search, Esc to close)
- **Smooth animations** and staggered card rendering

### ⚡ Performance & Reliability
- **4-hour intelligent caching** for repository data (localStorage)
- **30-minute news cache** to minimize API calls
- **Per-repository release caching** (2 hours) for fast switching
- **Fallback seed data** with 200+ curated repos for offline access
- **Rate-limit awareness** for GitHub Search API (60 req/hr unauthenticated)
- **Background refresh** to keep data fresh without blocking UI

---

## 🚀 Quick Start

### Option 1: Direct Browser Access
1. Clone or download this repository
2. Open `index.html` in your web browser
3. Done! No server setup needed.

```bash
git clone https://github.com/Dinesh0992/RepoTrend360.git
cd RepoTrend360
# Open index.html in your browser
```

### Option 2: Local Server (Optional)
For better performance and to avoid CORS issues:

```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000

# Node.js (with http-server)
npx http-server
```

Then navigate to `http://localhost:8000`

---

## 📖 Usage Guide

### Exploring Repositories
1. **Browse Categories**: Click category buttons in the left sidebar
2. **Search**: Use `Cmd+K` (Mac) or `Ctrl+K` (Windows/Linux) to open the search dropdown
3. **Filter by Language**: Select languages from the "Language" dropdown
4. **Filter by Topic**: Select GitHub topics from the "Topics" dropdown
5. **Filter by Year**: Adjust the creation year range with the "From Year" slider

### Viewing Insights
- Click the **Insights Panel** toggle to expand/collapse key metrics
- See "Dominating" (orange) and "Emerging" (green) repository classifications
- Review stats like total repositories, unique languages, and trending count

### Analyzing Trends
- View the **Trending Strip** at the top for the hottest repos right now
- Expand the **Charts Panel** to see:
  - Language distribution
  - Stars vs. Forks correlation
  - Growth trends over time
  - Category breakdown

### Monitoring News & Releases
1. Click the **"News & Releases"** link in the sidebar
2. Select a company/topic group (AI, Cloud, Data, DevTools, etc.)
3. Check up to 2 items per group to track their releases
4. Browse:
   - **Hot Tech News**: Hacker News stories trending in your domain
   - **New Releases**: Latest stable versions and announcements
   - **Security Advisories**: CVE alerts and vulnerability reports
   - **Community Discussions**: Dev.to articles and comments

### Refreshing Data
- Click the **"🔄 Refresh"** button to pull the latest data from GitHub
- Data automatically refreshes in the background every 2 hours

### Theme Switching
- Use the theme buttons in the sidebar footer to switch between Dark, Light, Ocean, and Solarized themes
- Your preference is saved in localStorage

---

## 🔧 Configuration

### Adding New Categories
Edit the `CATEGORY_QUERIES` object in the `<script>` section:

```javascript
const CATEGORY_QUERIES = {
    'my-category': 'topic:my-topic stars:>5000 pushed:>2025-01-01',
    // ... existing categories
};
```

GitHub Search qualifiers:
- `topic:keyword` — repositories tagged with a specific GitHub topic
- `stars:>N` — repositories with more than N stars
- `language:Language` — filter by programming language
- `pushed:>YYYY-MM-DD` — only recently active repositories

### Customizing Seed Data
Replace or extend `SEED_DATA` array with your own curated repositories. Each repo object should have:

```javascript
{
    name: "owner/repo",
    desc: "Repository description",
    stars: 10000,
    forks: 500,
    watchers: 10000,
    issues: 150,
    language: "TypeScript",
    created: "2020-01-15",
    updated: "2026-05-24",
    category: "web-dev",
    topics: ["topic1", "topic2"],
    owner_avatar: "https://...",
    url: "https://github.com/...",
    license: "MIT"
}
```

### Adjusting Cache TTLs
Modify cache timing constants at the top of the script:

```javascript
const CACHE_TTL = 4 * 60 * 60 * 1000;         // 4 hours for repos
const STALE_REFRESH = 2 * 60 * 60 * 1000;    // 2 hours background refresh
const NEWS_CACHE_TTL = 30 * 60 * 1000;       // 30 minutes for news
const REPO_CACHE_TTL = 2 * 60 * 60 * 1000;   // 2 hours per-repo release cache
```

---

## 🔑 API Integrations

RepoTrend360 uses multiple free, unauthenticated APIs:

| API | Purpose | Rate Limit | Notes |
|-----|---------|-----------|-------|
| **GitHub Search API** | Repository discovery | 60 req/hr | No token needed; rate-limit resets every hour |
| **GitHub Releases API** | Latest stable versions | 60 req/hr | Included in GitHub Search limit |
| **GitHub Advisories API** | Security vulnerabilities | Public | Free, no authentication |
| **Hacker News Algolia** | Tech news aggregation | 10k req/hr | Completely free, no token required |
| **Dev.to API** | Community discussions | 1000+ req/day | Free, no token needed |

### Optional: Using GitHub Personal Access Token
To increase the GitHub API rate limit to **5,000 requests/hour**:

1. Go to https://github.com/settings/tokens/new
2. Create a **Personal Access Token** (no scopes needed)
3. *(Feature not yet implemented)* — Add token input to the UI and use it in API calls

---

## 📊 Data Structure

### Repository Object
```javascript
{
    name: "string",              // "owner/repo"
    desc: "string",              // Description
    stars: number,               // Star count
    forks: number,               // Fork count
    watchers: number,            // Watcher count
    issues: number,              // Open issues
    language: "string",          // Primary language
    created: "YYYY-MM-DD",       // Creation date
    updated: "YYYY-MM-DD",       // Last update date
    category: "string",          // Category key
    topics: ["string"],          // GitHub topics
    owner_avatar: "string",      // Avatar URL
    url: "string",               // GitHub URL
    license: "string"            // License type
}
```

### News Item Object
```javascript
{
    title: "string",             // Article/release title
    url: "string",               // Link to article
    source: "string",            // "hn" | "github" | "devto"
    category: "string",          // "release" | "vuln" | "discussion"
    severity: "string",          // For advisories: "critical" | "high" | "medium" | "low"
    timestamp: number,           // Unix timestamp
    author: "string",            // Author/publisher
    tags: ["string"]             // Associated tags
}
```

---

## 🎯 Categories Included

| Category | Description | Query |
|----------|-------------|-------|
| **AI Agents** | Autonomous AI systems | `topic:ai-agent stars:>5000` |
| **LLM** | Large Language Models | `topic:llm stars:>10000` |
| **ML/MLOps** | Machine Learning & Ops | `topic:machine-learning stars:>20000` |
| **IoT** | Internet of Things | `topic:iot stars:>3000` |
| **Web Dev** | Frontend & Web Frameworks | `topic:frontend stars:>20000` |
| **DevTools** | Developer Tools & Infra | `topic:developer-tools stars:>10000` |
| **Security** | Security & Privacy | `topic:security stars:>10000` |
| **Blockchain** | Blockchain & Web3 | `topic:blockchain stars:>5000` |
| **Data Engineering** | Data Tools & Pipelines | `topic:data-engineering stars:>5000` |
| **Cloud Native** | Kubernetes & Container Orchestration | `topic:kubernetes stars:>8000` |
| ...and 20+ more | See `CATEGORY_QUERIES` in source |

---

## 🌐 Browser Support

| Browser | Support | Notes |
|---------|---------|-------|
| **Chrome/Edge** | ✅ Full | Recommended for best experience |
| **Firefox** | ✅ Full | All features work perfectly |
| **Safari** | ✅ Full | iOS and macOS supported |
| **IE 11** | ❌ Not supported | Uses ES6+ features |

---

## 💾 Storage & Privacy

- **LocalStorage**: Stores cache data and user preferences (theme, sidebar state)
- **No server tracking**: All data is processed client-side
- **No cookies**: Completely cookie-free
- **No personal data**: Only fetches public GitHub data

Clear your cache anytime:
```javascript
localStorage.removeItem('repoExplorer.cache');
localStorage.removeItem('repoExplorer.newsCache');
```

---

## ⚙️ Advanced Customization

### Modify Filter Defaults
Edit `RELEASE_FILTER_GROUPS` to change which companies/repos are pre-selected:

```javascript
const RELEASE_FILTER_GROUPS = {
    'companies': {
        'ai': { label: 'AI', items: { 'openai': ..., 'anthropic': ... } },
        // ...
    }
};
```

### Add Custom News Sources
Extend `fetchNewsSection()` to pull from your own API:

```javascript
async function fetchNewsSection(section) {
    if (section === 'custom') {
        return await fetch('https://your-api.com/news').then(r => r.json());
    }
    // ... existing logic
}
```

### Override Language Colors
Edit `LANG_COLORS` object:

```javascript
const LANG_COLORS = {
    'TypeScript': '#3178c6',
    'Python': '#3776ab',
    // Add your own
};
```

---

## 🐛 Troubleshooting

### "Rate Limited" Error
- GitHub Search API resets every hour
- Solution: Wait 1 hour or enable GitHub Personal Access Token

### Empty Repository List
- Check browser console (F12) for errors
- Clear cache: `localStorage.clear()`
- Reload the page
- Seed data should load as fallback

### Search Dropdown Not Showing Results
- Ensure you're typing 2+ characters
- Check your internet connection
- GitHub API might be temporarily unavailable

### Charts Not Rendering
- Refresh the page
- Ensure JavaScript is enabled
- Check that Chart.js CDN is accessible

### Mobile Sidebar Issues
- Click the **☰** button to toggle sidebar
- Click category to auto-close sidebar on selection

---

## 📝 License

This project is available under the **MIT License**. See [LICENSE](./LICENSE) for details.

---

## 🤝 Contributing

Contributions are welcome! Here's how:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

### Ideas for Contribution
- Add new repository categories
- Enhance filter UI
- Improve search performance
- Add export features (CSV, JSON)
- Implement API token input field
- Add dark mode animations
- Expand news sources
- Improve mobile responsiveness

---

## 📧 Support

- **Issues**: Report bugs or suggest features via GitHub Issues
- **Discussions**: Ask questions in GitHub Discussions

---

## 🙏 Acknowledgments

- **GitHub** — Repository data and APIs
- **Hacker News & Algolia** — Tech news aggregation
- **Dev.to** — Community discussions
- **Chart.js** — Beautiful data visualization
- All open-source contributors whose repos we feature

---

## 📊 Project Stats

- **Categories**: 30+
- **Seed Repositories**: 200+
- **API Integrations**: 4
- **Supported Themes**: 4
- **Lines of Code**: ~4,000
- **Dependencies**: 1 (Chart.js)
- **Bundle Size**: ~400KB (single HTML file)

---

## 🚀 Roadmap

- [ ] GitHub Personal Access Token support
- [ ] Export repository lists (CSV, JSON)
- [ ] Custom category creation
- [ ] Collaborative filtering & recommendations
- [ ] Integration with CI/CD for seed data updates
- [ ] Multi-language UI
- [ ] Repository comparison tool
- [ ] Bookmarking & saved views
- [ ] API backend (optional, for enhanced features)

---

**Made with ❤️ by [Dinesh](https://github.com/Dinesh0992)**

*Last Updated: May 24, 2026*

# mukeshhackthon
online mode 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GitGrade – AI Repository Mirror | #mukeshhackthon</title>
  <style>
    :root {
      --primary: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      --success: linear-gradient(135deg, #48bb78, #38a169);
      --warning: linear-gradient(135deg, #ed8936, #dd6b20);
      --danger: linear-gradient(135deg, #f56565, #e53e3e);
      --gold: linear-gradient(135deg, #f6ad55, #f59e0b);
      --silver: linear-gradient(135deg, #cbd5e0, #a0aec0);
      --bronze: linear-gradient(135deg, #fed7aa, #fc8181);
    }
    
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { 
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: var(--primary); 
      min-height: 100vh; 
      padding: 1rem;
      line-height: 1.6;
    }
    
    .container { 
      max-width: 900px; 
      margin: 0 auto; 
      background: rgba(255,255,255,0.95);
      backdrop-filter: blur(20px);
      border-radius: 24px; 
      box-shadow: 0 25px 50px rgba(0,0,0,0.15);
      overflow: hidden;
    }
    
    .header {
      background: var(--primary);
      color: white;
      padding: 2.5rem;
      text-align: center;
    }
    
    .header h1 { font-size: 2.5rem; margin-bottom: 0.5rem; }
    .header p { opacity: 0.95; font-size: 1.1rem; }
    
    .input-section {
      padding: 2.5rem;
      background: #f8fafc;
    }
    
    .input-group {
      display: flex; 
      gap: 1rem; 
      margin-bottom: 1rem;
      flex-wrap: wrap;
    }
    
    input[type="url"] {
      flex: 1;
      min-width: 350px;
      padding: 1.25rem 1.5rem;
      border: 2px solid #e2e8f0;
      border-radius: 16px;
      font-size: 1.1rem;
      transition: all 0.3s;
    }
    
    input[type="url"]:focus {
      outline: none;
      border-color: #667eea;
      box-shadow: 0 0 0 4px rgba(102,126,234,0.15);
      transform: translateY(-2px);
    }
    
    .analyze-btn {
      padding: 1.25rem 2.5rem;
      background: var(--primary);
      color: white;
      border: none;
      border-radius: 16px;
      font-size: 1.1rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s;
      white-space: nowrap;
    }
    
    .analyze-btn:hover:not(:disabled) {
      transform: translateY(-3px);
      box-shadow: 0 15px 30px rgba(102,126,234,0.4);
    }
    
    .analyze-btn:disabled {
      opacity: 0.7;
      cursor: not-allowed;
      transform: none;
    }
    
    .loading {
      display: none;
      text-align: center;
      padding: 3rem 2rem;
    }
    
    .spinner {
      width: 50px;
      height: 50px;
      border: 4px solid #e2e8f0;
      border-top: 4px solid #667eea;
      border-radius: 50%;
      animation: spin 1s linear infinite;
      margin: 0 auto 1.5rem;
    }
    
    @keyframes spin { 0% { transform: rotate(0deg); } 100% { transform: rotate(360deg); } }
    
    .results {
      display: none;
      padding: 3rem 2.5rem 2.5rem;
    }
    
    .score-badge {
      display: inline-flex;
      align-items: center;
      gap: 0.75rem;
      padding: 1rem 2rem;
      border-radius: 50px;
      font-size: 1.3rem;
      font-weight: 700;
      margin-bottom: 2rem;
      color: white;
    }
    
    .score-badge.gold { background: var(--gold); }
    .score-badge.silver { background: var(--silver); }
    .score-badge.bronze { background: var(--bronze); }
    
    .summary-section h3 {
      color: #4a5568;
      margin: 2rem 0 1rem 0;
      font-size: 1.5rem;
    }
    
    .summary {
      background: linear-gradient(135deg, #f7fafc, #edf2f7);
      padding: 2rem;
      border-radius: 20px;
      border-left: 6px solid #667eea;
      font-size: 1.1rem;
      line-height: 1.7;
    }
    
    .stats-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
      gap: 1.5rem;
      margin: 2rem 0;
    }
    
    .stat-card {
      background: white;
      padding: 1.5rem 2rem;
      border-radius: 16px;
      text-align: center;
      box-shadow: 0 4px 12px rgba(0,0,0,0.08);
      border-top: 4px solid #667eea;
    }
    
    .roadmap {
      background: linear-gradient(135deg, #f0fff4, #f0f9ff);
      padding: 2rem;
      border-radius: 20px;
      margin-top: 2rem;
    }
    
    .roadmap-item {
      display: flex;
      align-items: flex-start;
      gap: 1rem;
      padding: 1.25rem;
      margin-bottom: 1rem;
      background: white;
      border-radius: 16px;
      box-shadow: 0 2px 8px rgba(0,0,0,0.06);
      border-left: 5px solid #48bb78;
      transition: all 0.2s;
    }
    
    .roadmap-item:hover {
      transform: translateX(8px);
      box-shadow: 0 8px 25px rgba(0,0,0,0.12);
    }
    
    .error {
      display: none;
      padding: 2.5rem;
      background: #fed7d7;
      color: #c53030;
      border-radius: 16px;
      text-align: center;
      border-left: 6px solid #fc8181;
    }
    
    @media (max-width: 768px) {
      .header h1 { font-size: 2rem; }
      .input-group { flex-direction: column; }
      input[type="url"] { min-width: auto; }
      .stats-grid { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>
  <div class="container">
    <!-- Header -->
    <div class="header">
      <h1>🤖 GitGrade</h1>
      <p>AI Repository Mirror | UnsaidTalks Hackathon</p>
    </div>
    
    <!-- Input Section -->
    <div class="input-section">
      <div class="input-group">
        <input type="url" id="repoUrl" placeholder="https://github.com/username/repository" />
        <button class="analyze-btn" onclick="analyzeRepo()">🚀 Analyze Repository</button>
      </div>
      
      <div class="loading" id="loading">
        <div class="spinner"></div>
        <p>🔍 Fetching repository data via GitHub API... (Checking structure, commits, docs & more)</p>
      </div>
      
      <div class="error" id="error"></div>
    </div>
    
    <!-- Results Section -->
    <div class="results" id="results">
      <div class="score-badge" id="scoreBadge"></div>
      
      <div class="summary-section">
        <h3>📝 Written Summary</h3>
        <div class="summary" id="summary"></div>
      </div>
      
      <div class="stats-grid" id="statsGrid"></div>
      
      <div class="roadmap">
        <h3>🛣️ Personalized Roadmap</h3>
        <div id="roadmapList"></div>
      </div>
    </div>
  </div>

  <script>
    async function analyzeRepo() {
      const url = document.getElementById('repoUrl').value.trim();
      const loading = document.getElementById('loading');
      const results = document.getElementById('results');
      const error = document.getElementById('error');
      const btn = document.querySelector('.analyze-btn');
      
      // Reset UI
      results.style.display = 'none';
      error.style.display = 'none';
      btn.disabled = true;
      btn.textContent = 'Analyzing...';
      loading.style.display = 'block';
      
      try {
        if (!url.match(/github\.com\/[^\/]+\/[^\/]+/)) {
          throw new Error('Please enter a valid GitHub repository URL');
        }
        
        const { owner, repo } = parseRepoUrl(url);
        
        // Fetch all data in parallel
        const [filesRes, commitsRes, languagesRes, readmeRes, branchesRes] = await Promise.allSettled([
          fetch(`https://api.github.com/repos/${owner}/${repo}/contents`),
          fetch(`https://api.github.com/repos/${owner}/${repo}/commits?per_page=100`),
          fetch(`https://api.github.com/repos/${owner}/${repo}/languages`),
          fetch(`https://api.github.com/repos/${owner}/${repo}/readme`),
          fetch(`https://api.github.com/repos/${owner}/${repo}/branches`)
        ]);
        
        const files = filesRes.status === 'fulfilled' ? await filesRes.value.json() : [];
        const commits = commitsRes.status === 'fulfilled' ? await commitsRes.value.json() : [];
        const languages = languagesRes.status === 'fulfilled' ? await languagesRes.value.json() : {};
        const readmeRaw = readmeRes.status === 'fulfilled' ? await readmeRes.value.json() : {};
        const branches = branchesRes.status === 'fulfilled' ? await branchesRes.value.json() : [];
        
        const readme = readmeRaw.content ? atob(readmeRaw.content) : '';
        
        // Perform multi-dimensional analysis
        const analysis = evaluateRepository({
          files,
          commits: commits.length,
          languages: Object.keys(languages).length,
          readmeLength: readme.length,
          branches: branches.length,
          hasTests: files.some(f => /test|spec/i.test(f.name)),
          hasStructure: files.some(f => f.type === 'dir'),
          hasConfig: files.some(f => /package\.json|requirements\.txt|dockerfile|pom\.xml/i.test(f.name))
        });
        
        displayResults(analysis, languages);
        
      } catch (err) {
        error.textContent = `❌ ${err.message}`;
        error.style.display = 'block';
      } finally {
        loading.style.display = 'none';
        btn.disabled = false;
        btn.textContent = '🚀 Analyze Repository';
      }
    }
    
    function parseRepoUrl(url) {
      const match = url.match(/github\.com\/([^\/]+)\/([^\/]+(?:\/[^\/]+)?)/);
      if (!match) throw new Error('Invalid GitHub repository URL');
      return { owner: match[1], repo: match[2].split('/')[0] };
    }
    
    function evaluateRepository(data) {
      let score = 0;
      const roadmap = [];
      
      // 1. Project Structure (20 pts)
      if (data.files.length >= 10) score += 10;
      else if (data.files.length >= 5) score += 5;
      else roadmap.push('📁 Add more files and create proper folder structure (src/, docs/, tests/)');
      
      if (data.hasStructure) score += 10;
      else roadmap.push('📂 Organize code into directories');
      
      // 2. Documentation (20 pts)
      if (data.readmeLength >= 800) score += 15;
      else if (data.readmeLength >= 300) score += 10;
      else roadmap.push('📖 Write comprehensive README.md with setup instructions, screenshots, and usage');
      
      // 3. Commit History (15 pts)
      if (data.commits >= 30) score += 15;
      else if (data.commits >= 15) score += 10;
      else roadmap.push('💾 Commit regularly with meaningful, descriptive messages');
      
      // 4. Testing (15 pts)
      if (data.hasTests) score += 15;
      else roadmap.push('🧪 Add unit tests or integration tests');
      
      // 5. Tech Stack (10 pts)
      if (data.languages >= 3) score += 10;
      else if (data.languages >= 2) score += 5;
      else roadmap.push('🔧 Use multiple technologies (HTML/CSS/JS + backend/database)');
      
      // 6. Production Readiness (10 pts)
      if (data.hasConfig) score += 10;
      else roadmap.push('🚀 Add deployment files (package.json, Dockerfile, etc.)');
      
      // 7. Version Control (10 pts)
      if (data.branches >= 2) score += 10;
      else roadmap.push('🌟 Create feature branches and use Pull Requests');
      
      // Always add mentor tips
      roadmap.push(
        '🔄 Set up GitHub Actions for CI/CD pipeline',
        '📊 Add badges to README (build status, coverage)',
        '🔒 Create .gitignore and follow security best practices'
      );
      
      const level = score >= 80 ? 'gold' : score >= 55 ? 'silver' : 'bronze';
      const summaries = {
        gold: 'Excellent project depth with production-ready structure, documentation, and best practices.',
        silver: 'Solid foundation with good structure. Enhance testing and documentation for excellence.',
        bronze: 'Good start! Focus on organization, documentation, and consistent development practices.'
      };
      
      return { score, level, summary: summaries[level], roadmap };
    }
    
    function displayResults({ score, level, summary, roadmap }, languages) {
      document.getElementById('scoreBadge').textContent = `📊 ${score}/100 | ${level.toUpperCase()}`;
      document.getElementById('scoreBadge').className = `score-badge ${level}`;
      document.getElementById('summary').textContent = summary;
      document.getElementById('results').style.display = 'block';
      
      // Stats
      const statsGrid = document.getElementById('statsGrid');
      statsGrid.innerHTML = `
        <div class="stat-card">
          <div style="font-size: 2rem; font-weight: bold; color: #667eea;">${score}</div>
          <div style="color: #718096;">Score /100</div>
        </div>
        <div class="stat-card">
          <div style="font-size: 2rem; font-weight: bold; color: #48bb78;">${roadmap.length}</div>
          <div style="color: #718096;">Action Items</div>
        </div>
        <div class="stat-card">
          <div style="font-size: 2rem; font-weight: bold; color: #ed8936;">${Object.keys(languages).length}</div>
          <div style="color: #718096;">Languages</div>
        </div>
      `;
      
      // Roadmap
      document.getElementById('roadmapList').innerHTML = roadmap.map(item => 
        `<div class="roadmap-item">${item}</div>`
      ).join('');
      
      document.getElementById('results').scrollIntoView({ behavior: 'smooth' });
    }
    
    // Enter key support
    document.getElementById('repoUrl').addEventListener('keypress', e => {
      if (e.key === 'Enter') analyzeRepo();
    });
  </script>
</body>
</html>

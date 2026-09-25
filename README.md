<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>YT Curved — Rounded YouTube Player</title>
<style>
  :root {
    --bg: #0f0f0f;
    --bg-alt: #181818;
    --text: #f1f1f1;
    --text-muted: #aaaaaa;
    --border: #303030;
    --accent: #ff7a00;
    --accent-hover: #ff8a1c;
    --code-bg: #1e1e1e;
    --link: #3ea6ff;
  }

  * { box-sizing: border-box; }

  body {
    margin: 0;
    padding: 0;
    font-family: Roboto, -apple-system, BlinkMacSystemFont, "Segoe UI", Arial, sans-serif;
    background: var(--bg);
    color: var(--text);
    line-height: 1.65;
    font-size: 16px;
  }

  .container {
    max-width: 900px;
    margin: 0 auto;
    padding: 40px 24px 80px;
  }

  /* Header */
  header {
    border-bottom: 1px solid var(--border);
    padding-bottom: 24px;
    margin-bottom: 32px;
  }

  h1 {
    font-size: 2.5rem;
    margin: 0 0 12px;
    font-weight: 700;
    letter-spacing: -0.5px;
    display: flex;
    align-items: center;
    gap: 12px;
  }

  h1::before {
    content: "";
    display: inline-block;
    width: 40px;
    height: 40px;
    background: linear-gradient(135deg, #ff8a1c, #ff5f00);
    border-radius: 10px;
    position: relative;
  }

  .tagline {
    color: var(--text-muted);
    font-size: 1.1rem;
    margin: 0 0 16px;
  }

  /* Badges */
  .badges {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-top: 12px;
  }

  .badge {
    display: inline-block;
    padding: 4px 12px;
    border-radius: 20px;
    font-size: 0.75rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.5px;
    border: 1px solid var(--border);
    color: var(--text-muted);
    background: var(--bg-alt);
  }

  .badge.version { border-color: #1976d2; color: #64b5f6; }
  .badge.manifest { border-color: #388e3c; color: #81c784; }
  .badge.license  { border-color: #f9a825; color: #ffd54f; }
  .badge.chrome   { border-color: #d32f2f; color: #ef9a9a; }

  /* Headings */
  h2 {
    font-size: 1.75rem;
    margin-top: 48px;
    margin-bottom: 16px;
    padding-bottom: 8px;
    border-bottom: 1px solid var(--border);
    font-weight: 600;
  }

  h3 {
    font-size: 1.25rem;
    margin-top: 32px;
    margin-bottom: 12px;
    color: var(--accent);
    font-weight: 600;
  }

  /* Paragraphs */
  p {
    margin: 12px 0;
  }

  a {
    color: var(--link);
    text-decoration: none;
  }
  a:hover { text-decoration: underline; }

  /* Lists */
  ul, ol {
    padding-left: 24px;
    margin: 12px 0;
  }

  li {
    margin: 6px 0;
  }

  ul li::marker {
    color: var(--accent);
  }

  /* Code */
  code {
    background: var(--code-bg);
    padding: 2px 6px;
    border-radius: 4px;
    font-family: "Fira Code", Consolas, Monaco, monospace;
    font-size: 0.9em;
    color: #e0e0e0;
  }

  pre {
    background: var(--code-bg);
    padding: 16px 20px;
    border-radius: 8px;
    overflow-x: auto;
    border: 1px solid var(--border);
    margin: 16px 0;
    font-size: 0.9em;
    line-height: 1.55;
  }

  pre code {
    background: none;
    padding: 0;
    font-size: 1em;
  }

  /* Tables */
  table {
    width: 100%;
    border-collapse: collapse;
    margin: 16px 0;
    font-size: 0.95rem;
    border-radius: 8px;
    overflow: hidden;
  }

  th, td {
    padding: 10px 14px;
    text-align: left;
    border-bottom: 1px solid var(--border);
  }

  th {
    background: var(--bg-alt);
    font-weight: 600;
    color: var(--accent);
    text-transform: uppercase;
    font-size: 0.8rem;
    letter-spacing: 0.5px;
  }

  tr:last-child td { border-bottom: none; }

  tr:hover td { background: rgba(255, 122, 0, 0.04); }

  /* Images */
  .screenshot-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
    margin: 20px 0;
  }

  .screenshot-grid.single {
    grid-template-columns: 1fr;
  }

  figure {
    margin: 20px 0;
    border-radius: 12px;
    overflow: hidden;
    border: 1px solid var(--border);
    background: var(--bg-alt);
  }

  figure img {
    width: 100%;
    height: auto;
    display: block;
  }

  figcaption {
    padding: 10px 14px;
    font-size: 0.85rem;
    color: var(--text-muted);
    text-align: center;
    border-top: 1px solid var(--border);
  }

  /* Callouts */
  .note {
    border-left: 4px solid var(--accent);
    background: rgba(255, 122, 0, 0.08);
    padding: 12px 18px;
    border-radius: 0 8px 8px 0;
    margin: 16px 0;
    font-size: 0.95rem;
  }

  .warning {
    border-left: 4px solid #d32f2f;
    background: rgba(211, 47, 47, 0.08);
    padding: 12px 18px;
    border-radius: 0 8px 8px 0;
    margin: 16px 0;
    font-size: 0.95rem;
  }

  .success {
    border-left: 4px solid #388e3c;
    background: rgba(56, 142, 60, 0.08);
    padding: 12px 18px;
    border-radius: 0 8px 8px 0;
    margin: 16px 0;
    font-size: 0.95rem;
  }

  /* Feature cards */
  .feature-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 16px;
    margin: 20px 0;
  }

  .feature-card {
    background: var(--bg-alt);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 20px;
    transition: transform 0.15s ease, border-color 0.15s ease;
  }

  .feature-card:hover {
    transform: translateY(-2px);
    border-color: var(--accent);
  }

  .feature-card h4 {
    margin: 0 0 8px;
    font-size: 1rem;
    color: var(--accent);
  }

  .feature-card p {
    margin: 0;
    font-size: 0.9rem;
    color: var(--text-muted);
  }

  /* Button-style active icon */
  .btn-preview {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 28px;
    height: 28px;
    border-radius: 50%;
    background: var(--accent);
    color: #fff;
    font-size: 14px;
    margin: 0 4px;
    vertical-align: middle;
  }

  /* Footer */
  footer {
    margin-top: 64px;
    padding-top: 24px;
    border-top: 1px solid var(--border);
    text-align: center;
    color: var(--text-muted);
    font-size: 0.9rem;
  }

  footer .heart { color: #ff5252; }

  /* Back to top */
  .back-to-top {
    display: inline-block;
    margin-top: 16px;
    padding: 8px 20px;
    border-radius: 20px;
    background: var(--accent);
    color: #fff;
    font-weight: 600;
    font-size: 0.85rem;
    transition: background 0.15s ease;
  }
  .back-to-top:hover { background: var(--accent-hover); text-decoration: none; }

  /* Responsive */
  @media (max-width: 640px) {
    .container { padding: 24px 16px 60px; }
    h1 { font-size: 1.75rem; }
    h1::before { width: 32px; height: 32px; }
    h2 { font-size: 1.35rem; }
    .screenshot-grid { grid-template-columns: 1fr; }
    table { font-size: 0.85rem; }
    th, td { padding: 8px 10px; }
  }

  /* Smooth scroll */
  html { scroll-behavior: smooth; }
</style>
</head>
<body>

<div class="container">

  <!-- HEADER -->
  <header>
    <h1>YT Curved</h1>
    <p class="tagline">
      Add 20px rounded corners, blended black bars, and a customizable control bar
      to YouTube's theater mode and fullscreen. Now with screenshot, loop, and
      theater-remember tools.
    </p>
    <div class="badges">
      <span class="badge version">v4.1</span>
      <span class="badge manifest">Manifest v3</span>
      <span class="badge license">MIT License</span>
      <span class="badge chrome">Chrome Compatible</span>
    </div>
  </header>

  <!-- SCREENSHOTS -->
  <h2 id="screenshots">📸 Screenshots</h2>

  <h3>Theater Mode — Before vs After</h3>
  <div class="screenshot-grid">
    <figure>
      <img src="docs/images/before-theater.png" alt="Before theater mode — default YouTube player with square corners and black bars">
      <figcaption>Before — default YouTube player</figcaption>
    </figure>
    <figure>
      <img src="docs/images/after-theater.png" alt="After theater mode — rounded corners, blended bars, control bar visible">
      <figcaption>After — YT Curved applied</figcaption>
    </figure>
  </div>

  <h3>Fullscreen Mode</h3>
  <figure>
    <img src="docs/images/fullscreen.png" alt="Fullscreen mode with rounded corners and symmetric letterboxing">
    <figcaption>Fullscreen — rounded corners with symmetric letterboxing</figcaption>
  </figure>

  <h3>Custom Control Bar</h3>
  <figure>
    <img src="docs/images/control-bar.png" alt="Custom control bar with buttons below the player">
    <figcaption>Control bar — pill-shaped, appears below the player</figcaption>
  </figure>

  <h3>Settings Popup</h3>
  <figure>
    <img src="docs/images/settings-popup.png" alt="Radius slider popup with orange accent">
    <figcaption>Radius slider — 5px to 40px, live preview</figcaption>
  </figure>

  <h3>Light Mode Support</h3>
  <figure>
    <img src="docs/images/light-mode.png" alt="Light mode with header staying light in theater mode">
    <figcaption>Light mode — header stays light in theater mode</figcaption>
  </figure>

  <h3>Extension Icon</h3>
  <figure style="max-width: 200px;">
    <img src="icons/icon128.png" alt="Extension icon — orange rounded rectangle with play triangle">
    <figcaption>Toolbar icon</figcaption>
  </figure>

  <div class="note">
    <strong>📝 Note:</strong> Replace the image paths in <code>docs/images/</code> with your actual
    screenshots. The expected folder structure is:
    <pre><code>docs/
└── images/
    ├── before-theater.png
    ├── after-theater.png
    ├── fullscreen.png
    ├── control-bar.png
    ├── settings-popup.png
    └── light-mode.png</code></pre>
  </div>

  <!-- FEATURES -->
  <h2 id="features">✨ Features</h2>

  <h3>🎥 Visual Enhancements</h3>
  <div class="feature-grid">
    <div class="feature-card">
      <h4>20px Rounded Corners</h4>
      <p>Configurable from 5px to 40px via the settings popup, with live preview.</p>
    </div>
    <div class="feature-card">
      <h4>Blended Black Bars</h4>
      <p>Letterbox areas match YouTube's dark/light theme background
      (<code>#0f0f0f</code> / <code>#f9f9f9</code>).</p>
    </div>
    <div class="feature-card">
      <h4>Fullscreen Support</h4>
      <p>Rounded corners and centered video in fullscreen mode.</p>
    </div>
    <div class="feature-card">
      <h4>Light Mode Header Fix</h4>
      <p>The top bar stays light in theater mode — icons, search, logo, and Create button.</p>
    </div>
  </div>

  <h3>🎛️ Custom Control Bar</h3>
  <p>
    A compact, pill-shaped bar that appears <strong>below the player</strong>
    in theater and fullscreen modes, containing:
  </p>

  <table>
    <thead>
      <tr>
        <th>Button</th>
        <th>Action</th>
        <th>Active Color</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>🔁 <strong>Loop</strong></td>
        <td>Repeats the current video</td>
        <td><span style="color: var(--accent); font-weight: 600;">🟠 Orange</span></td>
      </tr>
      <tr>
        <td>📷 <strong>Screenshot</strong></td>
        <td>Saves the current frame as PNG</td>
        <td>—</td>
      </tr>
      <tr>
        <td>🎭 <strong>Theater Remember</strong></td>
        <td>Auto-enters theater mode on every video</td>
        <td><span style="color: var(--accent); font-weight: 600;">🟠 Orange</span></td>
      </tr>
      <tr>
        <td>⚙️ <strong>Settings</strong></td>
        <td>Opens radius slider (5–40px)</td>
        <td>—</td>
      </tr>
    </tbody>
  </table>

  <h3>🧹 Distraction Removal</h3>
  <ul>
    <li>Hides <strong>annotations</strong>, <strong>info cards</strong>, and <strong>card teasers</strong> during theater mode.</li>
  </ul>

  <h3>⚙️ Persistence</h3>
  <ul>
    <li>Settings saved via <code>chrome.storage.sync</code> — sync across all your Chrome devices.</li>
  </ul>

  <h3>🔄 Robust SPA Handling</h3>
  <ul>
    <li>Works when navigating between videos <strong>without refreshing the page</strong>.</li>
    <li>Re-attaches observers automatically after YouTube's internal navigation.</li>
  </ul>

  <!-- INSTALLATION -->
  <h2 id="installation">🚀 Installation</h2>

  <h3>From Source (Developer Mode)</h3>
  <ol>
    <li>
      <strong>Clone the repository</strong>
      <pre><code>git clone https://github.com/your-username/yt-curved.git
cd yt-curved</code></pre>
    </li>
    <li>
      <strong>Open Chrome Extensions</strong>
      <p>Navigate to <code>chrome://extensions/</code> in your browser.</p>
    </li>
    <li>
      <strong>Enable Developer Mode</strong>
      <p>Toggle <strong>Developer mode</strong> in the top-right corner.</p>
    </li>
    <li>
      <strong>Load Unpacked</strong>
      <p>Click <strong>Load unpacked</strong> and select the <code>yt-curved</code> folder.</p>
    </li>
    <li>
      <strong>Done!</strong>
      <p>The orange play-button icon will appear in your toolbar.</p>
    </li>
  </ol>

  <h3>From Chrome Web Store</h3>
  <p><em>Coming soon — link will be added once published.</em></p>

  <!-- USAGE -->
  <h2 id="usage">🖱️ Usage</h2>

  <ol>
    <li>Open any YouTube video at <code>youtube.com/watch?v=...</code>.</li>
    <li>Press <kbd>T</kbd> (or click the theater mode button) to enter theater mode.</li>
    <li>The video gets <strong>rounded corners</strong> and the <strong>custom bar appears below the player</strong>.</li>
    <li>Click the buttons in the bar:
      <ul>
        <li>🔁 <strong>Loop</strong> — toggles video looping.</li>
        <li>📷 <strong>Camera</strong> — downloads a PNG of the current frame.</li>
        <li>🎭 <strong>Theater icon</strong> — enables auto-theater mode on future videos.</li>
        <li>⚙️ <strong>Settings</strong> — opens the radius slider.</li>
      </ul>
    </li>
    <li>Press <kbd>F</kbd> to go fullscreen — corners stay rounded.</li>
    <li>Press <kbd>T</kbd> again to exit theater mode.</li>
  </ol>

  <!-- SETTINGS -->
  <h2 id="settings">⚙️ Settings</h2>

  <p>The settings popup appears when you click the ⚙️ icon in the control bar.</p>

  <table>
    <thead>
      <tr>
        <th>Setting</th>
        <th>Range</th>
        <th>Default</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><strong>Radius</strong></td>
        <td>5–40 px</td>
        <td>20 px</td>
        <td>Corner rounding of the video</td>
      </tr>
      <tr>
        <td><strong>Remember Theater</strong></td>
        <td>on / off</td>
        <td>off</td>
        <td>Auto-enter theater mode on every video</td>
      </tr>
    </tbody>
  </table>

  <p>All settings are stored in <code>chrome.storage.sync</code> and persist across sessions.</p>

  <!-- FILE STRUCTURE -->
  <h2 id="structure">📂 File Structure</h2>

  <pre><code>yt-curved/
├── manifest.json           # Extension manifest (v3)
├── content.js              # Main logic (detection, bar, buttons)
├── styles.css              # All visual styles
├── icons/
│   ├── icon16.png
│   ├── icon48.png
│   └── icon128.png
├── docs/
│   └── images/             # Screenshots for this README
│       ├── before-theater.png
│       ├── after-theater.png
│       ├── fullscreen.png
│       ├── control-bar.png
│       ├── settings-popup.png
│       └── light-mode.png
└── readme.md</code></pre>

  <!-- TECHNICAL -->
  <h2 id="technical">🛠️ Technical Details</h2>

  <h3>How It Works</h3>
  <p>
    The extension adds two CSS classes to the <code>&lt;html&gt;</code> element based on
    YouTube's player state:
  </p>

  <table>
    <thead>
      <tr>
        <th>Class</th>
        <th>When Applied</th>
        <th>Effect</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>yt-theater-curved</code></td>
        <td>Theater mode is active</td>
        <td>Rounds video, blends bars, shows control bar</td>
      </tr>
      <tr>
        <td><code>yt-fullscreen-curved</code></td>
        <td>Fullscreen is active</td>
        <td>Rounds video, centers it with symmetric letterboxing</td>
      </tr>
    </tbody>
  </table>

  <h3>Detection Methods (Fallback Chain)</h3>
  <ol>
    <li>Theater button's <code>aria-pressed="true"</code> attribute.</li>
    <li><code>ytd-watch-flexy[theater]</code> attribute.</li>
    <li><code>document.body.classList.contains('theater')</code>.</li>
    <li>Fullscreen API + <code>#movie_player.ytp-fullscreen</code> class.</li>
  </ol>

  <h3>Key CSS Variables</h3>
  <pre><code>:root {
  --yt-curved-radius: 20px;      /* Corner radius, updated by JS */
  --yt-curved-orange: #ff7a00;   /* Active button color */
}</code></pre>

  <h3>Permissions</h3>
  <table>
    <thead>
      <tr>
        <th>Permission</th>
        <th>Reason</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><code>storage</code></td>
        <td>Save user settings (radius, remember-theater) across sessions</td>
      </tr>
    </tbody>
  </table>

  <!-- COMPATIBILITY -->
  <h2 id="compatibility">🧪 Compatibility</h2>

  <table>
    <thead>
      <tr>
        <th>Browser</th>
        <th>Version</th>
        <th>Status</th>
      </tr>
    </thead>
    <tbody>
      <tr><td>Google Chrome</td><td>100+</td><td>✅ Tested</td></tr>
      <tr><td>Microsoft Edge</td><td>100+</td><td>✅ Works (Chromium)</td></tr>
      <tr><td>Brave</td><td>1.40+</td><td>✅ Works (Chromium)</td></tr>
      <tr><td>Opera</td><td>90+</td><td>✅ Works (Chromium)</td></tr>
      <tr><td>Firefox</td><td>—</td><td>❌ Not supported (MV3 differences)</td></tr>
      <tr><td>Safari</td><td>—</td><td>❌ Not supported</td></tr>
    </tbody>
  </table>

  <!-- KNOWN ISSUES -->
  <h2 id="issues">🐛 Known Issues</h2>

  <table>
    <thead>
      <tr>
        <th>Issue</th>
        <th>Status</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>"Create" button text may stay white in light mode on some YouTube versions</td>
        <td>🟡 Minor — cosmetic only</td>
      </tr>
      <tr>
        <td>Video centering in fullscreen can occasionally shift on non-16:9 videos</td>
        <td>🟡 Rare — YouTube's native behavior</td>
      </tr>
      <tr>
        <td>Screenshot may fail on DRM-protected content</td>
        <td>⚪ Expected — browser security</td>
      </tr>
    </tbody>
  </table>

  <p>Found a bug? <a href="https://github.com/your-username/yt-curved/issues">Open an issue</a>.</p>

  <!-- ROADMAP -->
  <h2 id="roadmap">🗺️ Roadmap</h2>

  <ul style="list-style: none; padding-left: 0;">
    <li>✅ Rounded corners on video (theater + fullscreen)</li>
    <li>✅ Blended black bars (dark/light theme)</li>
    <li>✅ Custom control bar with buttons</li>
    <li>✅ Configurable radius (5–40px)</li>
    <li>✅ Loop button</li>
    <li>✅ Screenshot button</li>
    <li>✅ Remember theater mode</li>
    <li>✅ Header fix for light mode</li>
    <li>⬜ Blurred background behind video</li>
    <li>⬜ Ambient glow effect</li>
    <li>⬜ Custom CSS injection</li>
    <li>⬜ Per-channel settings</li>
    <li>⬜ Auto-skip intros/outros</li>
    <li>⬜ Firefox port</li>
  </ul>

  <!-- CONTRIBUTING -->
  <h2 id="contributing">🤝 Contributing</h2>

  <p>Contributions are welcome! To get started:</p>

  <ol>
    <li>Fork the repository.</li>
    <li>Create a feature branch: <code>git checkout -b feature/amazing-feature</code></li>
    <li>Commit your changes: <code>git commit -m 'Add some amazing feature'</code></li>
    <li>Push the branch: <code>git push origin feature/amazing-feature</code></li>
    <li>Open a Pull Request.</li>
  </ol>

  <h3>Coding Style</h3>
  <ul>
    <li><strong>JavaScript:</strong> ES6+, 2-space indentation, semicolons.</li>
    <li><strong>CSS:</strong> BEM-ish naming, one property per line.</li>
    <li><strong>Comments:</strong> Clear section headers with <code>/* ===== */</code>.</li>
  </ul>

  <!-- LICENSE -->
  <h2 id="license">📄 License</h2>

  <p>Distributed under the <strong>MIT License</strong>. See <code>LICENSE</code> for more information.</p>

  <!-- ACKNOWLEDGMENTS -->
  <h2 id="acknowledgments">🙏 Acknowledgments</h2>

  <ul>
    <li>Inspired by the YouTube theater mode community.</li>
    <li>Icons by <a href="https://materialdesignicons.com/">Material Design Icons</a>.</li>
    <li>Built with ❤️ using vanilla JavaScript and CSS.</li>
  </ul>

  <!-- CONTACT -->
  <h2 id="contact">📬 Contact</h2>

  <ul>
    <li><strong>Author:</strong> Your Name</li>
    <li><strong>Email:</strong> your.email@example.com</li>
    <li><strong>GitHub:</strong> <a href="https://github.com/your-username">@your-username</a></li>
    <li><strong>Chrome Web Store:</strong> <a href="https://chrome.google.com/webstore/detail/...">YT Curved</a></li>
  </ul>

  <!-- SUPPORT -->
  <h2 id="support">⭐ Show Your Support</h2>

  <p>If you find this extension useful, please:</p>

  <ul>
    <li>⭐ <strong>Star</strong> the repository</li>
    <li>🐛 <strong>Report</strong> bugs</li>
    <li>💡 <strong>Suggest</strong> features</li>
    <li>📢 <strong>Share</strong> with friends</li>
  </ul>

  <!-- FOOTER -->
  <footer>
    <p>Made with <span class="heart">❤</span> for YouTube lovers</p>
    <a class="back-to-top" href="#screenshots">⬆ Back to top</a>
  </footer>

</div>

</body>
</html>

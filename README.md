# resume-builder
<!DOCTYPE html>
<html lang="en" style="--accent: #2b6cb0;">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Resume Builder — Demo</title>

  <style>
    :root {
      --bg: #f6f8fb;
      --card: #fff;
      --muted: #617083;
      --accent: #2b6cb0;
      --paper: #ffffff;
    }
    html, body {
      height: 100%;
      margin: 0;
      padding: 0;
    }
    body {
      background: linear-gradient(180deg, var(--bg), #ffffff);
      font-family: Inter, system-ui, -apple-system, Segoe UI, Roboto, 'Helvetica Neue', Arial;
      color: #0b1220;
    }
    .app {
      max-width: 1200px;
      margin: 28px auto;
      padding: 20px;
    }
    h1 {
      margin: 0 0 6px;
      font-size: 20px;
    }
    .muted {
      color: var(--muted);
      font-size: 13px;
    }
    .toolbar {
      display: flex;
      gap: 12px;
      align-items: center;
      flex-wrap: wrap;
      margin: 14px 0;
    }
    .card {
      background: var(--card);
      border-radius: 12px;
      padding: 12px;
      box-shadow: 0 8px 30px rgba(12,18,30,0.06);
    }
    label {
      font-size: 13px;
      color: var(--muted);
      display: block;
      margin-bottom: 6px;
    }
    select,
    input[type=text],
    input[type=file],
    textarea {
      padding: 8px 10px;
      border-radius: 8px;
      border: 1px solid #e9f0fb;
      background: #fff;
      min-width: 160px;
    }
    .controls {
      display: flex;
      gap: 12px;
      align-items: center;
    }
    button {
      background: var(--accent);
      color: #fff;
      border: none;
      padding: 9px 12px;
      border-radius: 10px;
      cursor: pointer;
    }
    button.ghost {
      background: transparent;
      border: 1px solid rgba(0,0,0,0.06);
      color: var(--muted);
    }
    .layout {
      display: grid;
      grid-template-columns: 1fr 520px;
      gap: 18px;
    }
    .editor {
      display: grid;
      gap: 10px;
    }
    .field {
      display: flex;
      gap: 10px;
      align-items: center;
    }
    .field .label {
      width: 110px;
      font-size: 13px;
      color: var(--muted);
    }
    .field input[type=text],
    .field textarea {
      flex: 1;
    }
    textarea {
      min-height: 72px;
      resize: vertical;
    }
    .preview {
      background: var(--paper);
      border-radius: 10px;
      padding: 18px;
      height: 100%;
      box-shadow: 0 10px 30px rgba(12,18,30,0.06);
      overflow: auto;
    }
    .photo {
      width: 110px;
      height: 110px;
      border-radius: 14px;
      overflow: hidden;
      background: #eef3ff;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .photo.circle { border-radius: 999px; }
    .photo.round { border-radius: 14px; }
    .photo.frame {
      box-shadow: 0 4px 16px rgba(0,0,0,0.08);
      padding: 6px;
      background: linear-gradient(180deg, #fff, #f7fbff);
    }
    .photo img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      display: block;
    }
    .template {
      color: #0b1220;
    }
    .tpl-a .head {
      display: flex;
      gap: 14px;
      align-items: center;
    }
    .tpl-a .name {
      font-size: 22px;
      font-weight: 700;
    }
    .tpl-a .role {
      color: var(--muted);
    }
    .tpl-b {
      font-family: Merriweather, serif;
    }
    .tpl-b .name {
      font-size: 24px;
      font-weight: 700;
    }
    .tpl-b .head {
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .tpl-c {
      display: flex;
      gap: 16px;
    }
    .tpl-c .left {
      width: 160px;
      background: var(--accent);
      color: #fff;
      padding: 14px;
      border-radius: 10px;
    }
    .tpl-c .right {
      flex: 1;
      padding: 4px;
    }
    .tpl-d .head {
      text-align: center;
      padding-bottom: 12px;
      border-bottom: 2px dashed rgba(0,0,0,0.06);
    }
    .tpl-d .name {
      font-size: 26px;
      font-weight: 700;
    }
    .tpl-e {
      border: 1px solid rgba(0,0,0,0.06);
      border-radius: 10px;
      padding: 12px;
    }
    .tpl-e .name {
      font-size: 20px;
      font-weight: 600;
    }
    .tpl-f {
      font-family: 'Roboto Slab', serif;
    }
    .section {
      margin-top: 12px;
    }
    .section h4 {
      margin: 0 0 6px 0;
      font-size: 13px;
      color: var(--accent);
    }
    .skills {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
    }
    .skill {
      padding: 6px 8px;
      border-radius: 999px;
      border: 1px solid rgba(0,0,0,0.06);
      font-size: 13px;
    }
    @media (max-width: 980px) {
      .layout {
        grid-template-columns: 1fr;
      }
      .preview {
        height: auto;
      }
    }
  </style>
</head>
<body>
  <div class="app">
    <h1>Resume Builder — Demo</h1>
    <div class="muted">Live preview enabled — edit fields and see changes instantly.</div>

    <div class="toolbar">
      <div class="card controls">
        <div>
          <label for="template">Template</label>
          <select id="template">
            <option value="tpl-a">Modern Clean</option>
            <option value="tpl-b">Serif Elegant</option>
            <option value="tpl-c">Bold Sidebar</option>
            <option value="tpl-d">Minimal Line</option>
            <option value="tpl-e">Elegant Box</option>
            <option value="tpl-f">Modern Slab</option>
          </select>
        </div>
        <div>
          <label for="font">Font</label>
          <select id="font">
            <option value="Inter">Inter</option>
            <option value="Poppins">Poppins</option>
            <option value="Raleway">Raleway</option>
            <option value="Merriweather">Merriweather</option>
            <option value="Roboto Slab">Roboto Slab</option>
            <option value="Lato">Lato</option>
          </select>
        </div>
        <div>
          <label for="accent">Accent</label>
          <input id="accent" type="color" value="#2b6cb0">
        </div>
        <div>
          <label for="bg">Background</label>
          <select id="bg">
            <option value="#f6f8fb">Light</option>
            <option value="#fff8f0">Warm</option>
            <option value="#f0fff4">Fresh</option>
            <option value="#fdf2f8">Soft Pink</option>
            <option value="#eef5ff">Cool Blue</option>
            <option value="#ffffff">Paper White</option>
          </select>
        </div>
        <div>
          <label for="bgCustom">Custom BG</label>
          <input id="bgCustom" type="color" value="#f6f8fb">
        </div>
        <div>
          <label for="shape">Photo shape</label>
          <select id="shape">
            <option value="circle">Circle</option>
            <option value="round">Rounded</option>
            <option value="square">Square</option>
            <option value="frame">Framed</option>
          </select>
        </div>
        <div style="align-self: end">
          <button id="download">Download PDF</button>
        </div>
      </div>
    </div>

    <div class="layout">
      <div class="editor card">
        <div class="field">
          <div class="label">Photo</div>
          <input id="photoInput" type="file" accept="image/*">
        </div>
        <div class="field">
          <div class="label">Name</div>
          <input id="name" type="text" placeholder="Your name">
        </div>
        <div class="field">
          <div class="label">Title</div>
          <input id="title" type="text" placeholder="Your title / role">
        </div>
        <div class="field">
          <div class="label">Location</div>
          <input id="location" type="text" placeholder="Your location">
        </div>
        <div class="field">
          <div class="label">Contact</div>
          <input id="contact" type="text" placeholder="Email / phone">
        </div>
        <div class="field">
          <div class="label">Summary</div>
          <textarea id="summary" placeholder="Brief summary about you"></textarea>
        </div>
        <div class="field">
          <div class="label">Experience</div>
          <textarea id="experience" placeholder="Work experience details"></textarea>
        </div>
        <div class="field">
          <div class="label">Education</div>
          <textarea id="education" placeholder="Educational background"></textarea>
        </div>
        <div class="field">
          <div class="label">Skills</div>
          <input id="skills" type="text" placeholder="e.g. HTML, CSS, JavaScript">
        </div>
        <div class="field">
          <div class="label">Extras</div>
          <input id="extras" type="text" placeholder="Languages, Awards, etc.">
        </div>
      </div>
      <div class="preview card">
        <div id="previewArea" class="preview template tpl-a" style="font-family: Inter;">
          <!-- preview content injected by JS -->
        </div>
      </div>
    </div>
  </div>

  <!-- you can include html2pdf script if you need PDF download -->
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.9.3/html2pdf.bundle.min.js"></script>

  <script>
    const preview = document.getElementById('previewArea');
    const templateSelect = document.getElementById('template');
    const fontSelect = document.getElementById('font');
    const accentInput = document.getElementById('accent');
    const bgSelect = document.getElementById('bg');
    const bgCustom = document.getElementById('bgCustom');
    const photoInput = document.getElementById('photoInput');
    const shapeSelect = document.getElementById('shape');

    const fields = ['name','title','location','contact','summary','experience','education','skills','extras'];
    const state = {};
    fields.forEach(f => state[f] = '');
    state.photo = null;
    state.photoName = null;

    const el = id => document.getElementById(id);

    function esc(s) {
      if (!s) return '';
      return s
        .replaceAll('&', '&amp;')
        .replaceAll('<', '&lt;')
        .replaceAll('>', '&gt;')
        .replaceAll('\n', '<br>');
    }

    function skillsHtml(str) {
      if (!str) return '';
      return str.split(',')
        .map(s => s.trim())
        .filter(Boolean)
        .map(s => `<span class="skill">${esc(s)}</span>`)
        .join(' ');
    }

    photoInput.addEventListener('change', e => {
      const f = e.target.files && e.target.files[0];
      if (!f) return;
      const reader = new FileReader();
      reader.onload = ev => {
        state.photo = ev.target.result;
        state.photoName = f.name;
        render();
      };
      reader.readAsDataURL(f);
    });

    fields.forEach(id => {
      el(id).addEventListener('input', e => {
        state[id] = e.target.value;
        render();
      });
    });

    [templateSelect, fontSelect, accentInput, bgSelect, bgCustom, shapeSelect]
      .forEach(it => it.addEventListener('change', render));

    function photoHtml() {
      const cls = shapeSelect.value === 'circle'
        ? 'photo circle'
        : shapeSelect.value === 'round'
          ? 'photo round'
          : shapeSelect.value === 'frame'
            ? 'photo frame'
            : 'photo';
      if (state.photo) {
        return `<div class="${cls}"><img src="${state.photo}" alt="${state.photoName || 'photo'}"></div>`;
      } else {
        return `<div class="${cls}"><i class="fa fa-user" style="font-size:44px;color:rgba(0,0,0,0.18)"></i></div>`;
      }
    }

    function render() {
      document.documentElement.style.setProperty('--accent', accentInput.value);
      const bg = bgCustom.value || bgSelect.value || '#f6f8fb';
      // apply to both root variable and body background
      document.documentElement.style.setProperty('--bg', bg);
      document.body.style.background = `linear-gradient(180deg, ${bg}, #ffffff)`;

      preview.className = `preview template ${templateSelect.value}`;
      preview.style.fontFamily = fontSelect.value;

      const commonHeader = `<div style="display:flex;gap:14px;align-items:center;flex-wrap:wrap">
        ${photoHtml()}
        <div>
          <div style="font-size:20px;font-weight:700">${esc(state.name)}</div>
          <div style="color:var(--muted)">${esc(state.title)}</div>
          <div style="margin-top:6px;color:var(--muted);font-size:13px">
            ${esc(state.location)}${state.location && state.contact ? ' · ' : ''}${esc(state.contact)}
          </div>
        </div>
      </div>`;

      let html = '';
      const tpl = templateSelect.value;

      if (tpl === 'tpl-a') {
        html = `${commonHeader}
          <div class="section"><h4>Summary</h4><div>${esc(state.summary)}</div></div>
          <div class="section"><h4>Experience</h4><div>${esc(state.experience)}</div></div>
          <div class="section"><h4>Education</h4><div>${esc(state.education)}</div></div>
          <div class="section"><h4>Skills</h4><div class="skills">${skillsHtml(state.skills)}</div></div>`;
      } else if (tpl === 'tpl-b') {
        html = `${commonHeader}
          <div class="section"><h4>Profile</h4><div>${esc(state.summary)}</div></div>
          <div class="section"><h4>Work</h4><div>${esc(state.experience)}</div></div>
          <div class="section"><h4>Education</h4><div>${esc(state.education)}</div></div>
          <div class="section"><h4>Skills</h4><div class="skills">${skillsHtml(state.skills)}</div></div>`;
      } else if (tpl === 'tpl-c') {
        html = `<div class="tpl-c">
          <div class="left">
            ${photoHtml()}
            <div style="height:10px"></div>
            <div style="font-size:18px;font-weight:700">${esc(state.name)}</div>
            <div style="opacity:0.9">${esc(state.title)}</div>
            <div style="height:10px"></div>
            <div style="font-size:13px;margin-top:6px">${esc(state.contact)}<br>${esc(state.location)}</div>
            <div style="height:10px"></div>
            <div><strong style="font-size:13px;color:#fff">Skills</strong><div style="margin-top:6px">${skillsHtml(state.skills)}</div></div>
          </div>
          <div class="right">
            <div class="section"><h4>Summary</h4><div>${esc(state.summary)}</div></div>
            <div class="section"><h4>Experience</h4><div>${esc(state.experience)}</div></div>
            <div class="section"><h4>Education</h4><div>${esc(state.education)}</div></div>
          </div>
        </div>`;
      } else if (tpl === 'tpl-d') {
        html = `<div class="tpl-d">
          <div class="head">
            ${photoHtml()}
            <div style="margin-top:10px;font-size:22px;font-weight:700">${esc(state.name)}</div>
            <div style="color:var(--muted)">${esc(state.title)}</div>
          </div>
          <div class="section"><h4>Summary</h4><div>${esc(state.summary)}</div></div>
          <div class="section"><h4>Experience</h4><div>${esc(state.experience)}</div></div>
        </div>`;
      } else if (tpl === 'tpl-e') {
        html = `<div class="tpl-e">
          ${photoHtml()}
          <div style="margin-top:10px;text-align:center" class="name">${esc(state.name)}</div>
          <div style="text-align:center;color:var(--muted)">${esc(state.title)}</div>
          <div class="section"><h4>Profile</h4><div>${esc(state.summary)}</div></div>
          <div class="section"><h4>Skills</h4><div class="skills">${skillsHtml(state.skills)}</div></div>
        </div>`;
      } else if (tpl === 'tpl-f') {
        html = `<div class="tpl-f">
          <div class="head">${commonHeader}</div>
          <div class="section"><h4>Summary</h4><div>${esc(state.summary)}</div></div>
          <div class="section"><h4>Experience</h4><div>${esc(state.experience)}</div></div>
          <div class="section"><h4>Education</h4><div>${esc(state.education)}</div></div>
          <div class="section"><h4>Skills</h4><div class="skills">${skillsHtml(state.skills)}</div></div>
        </div>`;
      }

      preview.innerHTML = html;
    }

    // Initial render
    render();

    document.getElementById('download').addEventListener('click', () => {
      const options = {
        margin: 0.4,
        filename: `resume-${Date.now()}.pdf`,
        html2canvas: { scale: 2 },
        jsPDF: { unit: 'in', format: 'a4', orientation: 'portrait' }
      };
      html2pdf().set(options).from(preview).save();
    });
  </script>
</body>
</html>

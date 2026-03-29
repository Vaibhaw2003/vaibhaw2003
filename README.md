<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Vaibhaw Singh – Developer Profile</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,300;0,400;0,500;0,700;1,400&family=Syne:wght@400;700;800&display=swap" rel="stylesheet">
<style>
*,*::before,*::after{box-sizing:border-box;margin:0;padding:0}
:root{
  --bg:#04060f;--bg2:#080d1a;--bg3:#0f1626;--bg4:#141e30;
  --cyan:#00e5ff;--cyan2:#38bdf8;--green:#00ff9d;--purple:#a855f7;
  --amber:#f59e0b;--pink:#ec4899;--red:#ef4444;
  --text:#e2e8f0;--muted:#4a5568;--muted2:#64748b;
  --border:rgba(0,229,255,0.1);--border2:rgba(0,229,255,0.22);
}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--text);font-family:'JetBrains Mono',monospace;overflow-x:hidden}

/* ===== PARTICLE CANVAS ===== */
#bg-canvas{position:fixed;top:0;left:0;width:100%;height:100%;z-index:0;pointer-events:none}

/* ===== GRID OVERLAY ===== */
.grid-overlay{
  position:fixed;inset:0;z-index:0;pointer-events:none;
  background-image:
    linear-gradient(rgba(0,229,255,0.025) 1px,transparent 1px),
    linear-gradient(90deg,rgba(0,229,255,0.025) 1px,transparent 1px);
  background-size:60px 60px;
  animation:gridShift 20s linear infinite;
}
@keyframes gridShift{to{background-position:60px 60px}}

/* ===== SCROLL PROGRESS ===== */
#scroll-bar{
  position:fixed;top:0;left:0;height:2px;z-index:100;
  background:linear-gradient(90deg,var(--cyan),var(--purple),var(--green));
  width:0%;transition:width 0.1s linear;
  box-shadow:0 0 8px var(--cyan);
}

/* ===== CURSOR GLOW ===== */
#cursor-glow{
  position:fixed;width:300px;height:300px;border-radius:50%;
  pointer-events:none;z-index:1;
  background:radial-gradient(circle,rgba(0,229,255,0.06) 0%,transparent 70%);
  transform:translate(-50%,-50%);
  transition:transform 0.05s linear;
}

.content{position:relative;z-index:2;max-width:940px;margin:0 auto;padding:48px 24px 100px}

/* ===== REVEAL ANIMATION ===== */
.reveal{opacity:0;transform:translateY(28px);transition:opacity 0.7s ease,transform 0.7s ease}
.reveal.visible{opacity:1;transform:none}

/* ===== HEADER ===== */
.header{
  border:1px solid var(--border2);
  background:linear-gradient(135deg,rgba(0,229,255,0.03),rgba(168,85,247,0.03));
  border-radius:20px;padding:52px 44px;margin-bottom:36px;
  position:relative;overflow:hidden;
}
.header-corner{position:absolute;width:60px;height:60px;border-color:var(--cyan);border-style:solid;opacity:0.4}
.header-corner.tl{top:16px;left:16px;border-width:2px 0 0 2px;border-radius:4px 0 0 0}
.header-corner.tr{top:16px;right:16px;border-width:2px 2px 0 0;border-radius:0 4px 0 0}
.header-corner.bl{bottom:16px;left:16px;border-width:0 0 2px 2px;border-radius:0 0 0 4px}
.header-corner.br{bottom:16px;right:16px;border-width:0 2px 2px 0;border-radius:0 0 4px 0}

.scan-line{
  position:absolute;top:0;left:-100%;width:100%;height:100%;z-index:0;
  background:linear-gradient(90deg,transparent,rgba(0,229,255,0.04),transparent);
  animation:scan 4s ease-in-out infinite;
}
@keyframes scan{0%,100%{left:-100%}50%{left:100%}}

.status-badge{
  display:inline-flex;align-items:center;gap:8px;font-size:10px;
  color:var(--green);border:1px solid rgba(0,255,157,0.25);
  padding:5px 14px;border-radius:99px;margin-bottom:22px;letter-spacing:0.12em;
  animation:badgePulse 3s ease-in-out infinite;
}
@keyframes badgePulse{
  0%,100%{box-shadow:0 0 0 0 rgba(0,255,157,0)}
  50%{box-shadow:0 0 0 6px rgba(0,255,157,0.06)}
}
.status-dot{width:7px;height:7px;border-radius:50%;background:var(--green);box-shadow:0 0 8px var(--green);animation:dotPulse 2s infinite}
@keyframes dotPulse{0%,100%{transform:scale(1);opacity:1}50%{transform:scale(1.4);opacity:0.6}}

.name{
  font-family:'Syne',sans-serif;font-size:clamp(42px,7vw,72px);font-weight:800;
  letter-spacing:-0.03em;line-height:1;margin-bottom:10px;
  background:linear-gradient(135deg,#ffffff 20%,var(--cyan) 55%,var(--purple));
  -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
  animation:nameGlow 4s ease-in-out infinite;
}
@keyframes nameGlow{0%,100%{filter:brightness(1)}50%{filter:brightness(1.15)}}

.role-row{display:flex;align-items:center;gap:0;margin-bottom:22px;flex-wrap:wrap}
.role-item{font-size:11px;letter-spacing:0.18em;color:var(--muted2);padding:0 14px}
.role-item:first-child{padding-left:0}
.role-sep{color:var(--cyan);opacity:0.4}

.typed-line{font-size:13px;color:var(--muted2);line-height:1.8;margin-bottom:28px;min-height:24px}
.typed-line .hl{color:var(--text)}
#cursor{display:inline-block;width:2px;height:13px;background:var(--cyan);margin-left:2px;vertical-align:middle;animation:blink 1s step-end infinite}
@keyframes blink{50%{opacity:0}}

.social-row{display:flex;gap:8px;flex-wrap:wrap}
.social-btn{
  display:inline-flex;align-items:center;gap:7px;font-size:11px;letter-spacing:0.08em;
  color:var(--muted2);border:1px solid rgba(255,255,255,0.08);
  padding:7px 16px;border-radius:8px;text-decoration:none;
  transition:all 0.25s;position:relative;overflow:hidden;
}
.social-btn::before{
  content:'';position:absolute;inset:0;
  background:linear-gradient(135deg,rgba(0,229,255,0.08),rgba(168,85,247,0.08));
  opacity:0;transition:opacity 0.25s;
}
.social-btn:hover{color:var(--cyan);border-color:var(--border2);transform:translateY(-2px)}
.social-btn:hover::before{opacity:1}

/* ===== SECTION LABEL ===== */
.sl{
  font-size:10px;letter-spacing:0.22em;color:var(--cyan);opacity:0.65;
  margin-bottom:18px;display:flex;align-items:center;gap:12px;
}
.sl::before{content:'//';color:var(--muted);font-size:10px;opacity:0.8}
.sl::after{content:'';flex:1;height:1px;background:linear-gradient(90deg,var(--border),transparent)}

/* ===== INFO GRID ===== */
.info-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(180px,1fr));gap:12px;margin-bottom:36px}
.info-card{
  background:var(--bg2);border:1px solid var(--border);border-radius:12px;
  padding:18px 20px;transition:all 0.3s;position:relative;overflow:hidden;
}
.info-card::after{
  content:'';position:absolute;bottom:0;left:0;right:0;height:2px;
  background:linear-gradient(90deg,var(--cyan),var(--purple));
  transform:scaleX(0);transition:transform 0.3s;transform-origin:left;
}
.info-card:hover{border-color:var(--border2);transform:translateY(-3px);background:var(--bg3)}
.info-card:hover::after{transform:scaleX(1)}
.ic-icon{font-size:22px;margin-bottom:12px}
.ic-title{font-size:9px;color:var(--muted);letter-spacing:0.14em;margin-bottom:5px}
.ic-value{font-size:12px;color:var(--text);line-height:1.5}

/* ===== BACKEND SECTION ===== */
.backend-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:20px;margin-bottom:36px}

.be-card{
  background:var(--bg2);border:1px solid var(--border);border-radius:16px;
  overflow:hidden;transition:all 0.3s;position:relative;
}
.be-card:hover{transform:translateY(-4px);border-color:var(--border2)}

.be-card-header{
  padding:22px 24px 18px;position:relative;
  border-bottom:1px solid var(--border);
}
.be-card-header::before{
  content:'';position:absolute;top:0;left:0;right:0;height:3px;
}
.be-card.spring .be-card-header::before{background:linear-gradient(90deg,#6aad3d,#a8d462)}
.be-card.node   .be-card-header::before{background:linear-gradient(90deg,#3c873a,#68a063)}
.be-card.flask  .be-card-header::before{background:linear-gradient(90deg,#666,#fff)}

.be-logo-row{display:flex;align-items:center;gap:12px;margin-bottom:8px}
.be-logo{
  width:38px;height:38px;border-radius:10px;display:flex;align-items:center;
  justify-content:center;font-size:20px;font-weight:800;font-family:'Syne',sans-serif;
  flex-shrink:0;
}
.be-card.spring .be-logo{background:rgba(106,173,61,0.12);color:#6aad3d;border:1px solid rgba(106,173,61,0.2)}
.be-card.node   .be-logo{background:rgba(104,160,99,0.12);color:#68a063;border:1px solid rgba(104,160,99,0.2)}
.be-card.flask  .be-logo{background:rgba(255,255,255,0.06);color:#eee;border:1px solid rgba(255,255,255,0.1)}

.be-name{font-family:'Syne',sans-serif;font-size:18px;font-weight:700;color:#fff}
.be-sub{font-size:10px;color:var(--muted2);letter-spacing:0.08em;margin-top:2px}

.be-level{
  display:inline-flex;align-items:center;gap:6px;
  font-size:10px;letter-spacing:0.1em;padding:4px 12px;border-radius:99px;
}
.be-card.spring .be-level{color:#6aad3d;background:rgba(106,173,61,0.1);border:1px solid rgba(106,173,61,0.2)}
.be-card.node   .be-level{color:#68a063;background:rgba(104,160,99,0.1);border:1px solid rgba(104,160,99,0.2)}
.be-card.flask  .be-level{color:#aaa;background:rgba(255,255,255,0.05);border:1px solid rgba(255,255,255,0.1)}

.be-body{padding:20px 24px}

.be-desc{font-size:12px;color:var(--muted2);line-height:1.8;margin-bottom:16px}

.be-features{list-style:none;margin-bottom:18px}
.be-features li{
  font-size:11px;color:var(--muted2);padding:6px 0;
  border-bottom:1px solid rgba(255,255,255,0.04);
  display:flex;align-items:flex-start;gap:8px;line-height:1.5;
}
.be-features li:last-child{border-bottom:none}
.be-features li::before{content:'▸';font-size:9px;flex-shrink:0;margin-top:2px}
.be-card.spring .be-features li::before{color:#6aad3d}
.be-card.node   .be-features li::before{color:#68a063}
.be-card.flask  .be-features li::before{color:#888}

.be-tags{display:flex;flex-wrap:wrap;gap:6px}
.be-tag{font-size:10px;padding:3px 10px;border-radius:5px;background:rgba(255,255,255,0.04);color:var(--muted2);border:1px solid rgba(255,255,255,0.07);transition:all 0.2s}
.be-tag:hover{background:rgba(0,229,255,0.06);color:var(--cyan);border-color:rgba(0,229,255,0.2)}

/* ===== SKILL BARS ===== */
.skills-section{margin-bottom:36px}
.skill-item{margin-bottom:16px}
.skill-head{display:flex;justify-content:space-between;align-items:center;margin-bottom:7px}
.skill-name{font-size:12px;color:var(--text)}
.skill-pct{font-size:11px;color:var(--muted2)}
.bar-track{height:6px;background:rgba(255,255,255,0.05);border-radius:99px;overflow:hidden;position:relative}
.bar-fill{height:100%;border-radius:99px;transform:scaleX(0);transform-origin:left;transition:transform 1.2s cubic-bezier(0.4,0,0.2,1)}
.bar-fill::after{
  content:'';position:absolute;top:0;right:0;width:4px;height:100%;border-radius:99px;
  background:white;opacity:0.8;animation:shine 2s ease-in-out infinite;
}
@keyframes shine{0%,100%{opacity:0.8}50%{opacity:0.2}}

.bar-java    {background:linear-gradient(90deg,#f59e0b,#fcd34d);width:88%}
.bar-spring  {background:linear-gradient(90deg,#6aad3d,#a8d462);width:83%}
.bar-node    {background:linear-gradient(90deg,#68a063,#86efac);width:72%}
.bar-dart    {background:linear-gradient(90deg,#00e5ff,#38bdf8);width:80%}
.bar-flask   {background:linear-gradient(90deg,#94a3b8,#e2e8f0);width:65%}
.bar-react   {background:linear-gradient(90deg,#61dafb,#a5f3fc);width:68%}
.bar-python  {background:linear-gradient(90deg,#a855f7,#d8b4fe);width:62%}
.bar-sql     {background:linear-gradient(90deg,#00ff9d,#6ee7b7);width:70%}

/* ===== TECH TAGS ===== */
.stack-section{margin-bottom:36px}
.cat-row{margin-bottom:20px}
.cat-head{
  font-size:10px;letter-spacing:0.15em;margin-bottom:10px;
  display:flex;align-items:center;gap:8px;
}
.cat-head .dot{width:5px;height:5px;border-radius:50%}
.cat-lang .dot{background:var(--cyan)}
.cat-front .dot{background:var(--purple)}
.cat-back .dot{background:var(--green)}
.cat-db .dot{background:var(--amber)}
.cat-cloud .dot{background:#818cf8}
.cat-tool .dot{background:var(--muted2)}

.cat-lang .cat-head{color:var(--cyan)}
.cat-front .cat-head{color:var(--purple)}
.cat-back .cat-head{color:var(--green)}
.cat-db .cat-head{color:var(--amber)}
.cat-cloud .cat-head{color:#818cf8}
.cat-tool .cat-head{color:var(--muted2)}

.tag-wrap{display:flex;flex-wrap:wrap;gap:8px}
.tag{
  font-family:'JetBrains Mono',monospace;font-size:11px;
  padding:5px 13px;border-radius:6px;border:1px solid;
  transition:all 0.25s;cursor:default;letter-spacing:0.04em;
  position:relative;overflow:hidden;
}
.tag::before{
  content:'';position:absolute;inset:0;opacity:0;
  background:linear-gradient(135deg,rgba(255,255,255,0.06),transparent);
  transition:opacity 0.2s;
}
.tag:hover{transform:translateY(-2px)}
.tag:hover::before{opacity:1}
.cat-lang  .tag{border-color:rgba(0,229,255,0.3);color:var(--cyan);background:rgba(0,229,255,0.06)}
.cat-front .tag{border-color:rgba(168,85,247,0.3);color:var(--purple);background:rgba(168,85,247,0.06)}
.cat-back  .tag{border-color:rgba(0,255,157,0.3);color:var(--green);background:rgba(0,255,157,0.06)}
.cat-db    .tag{border-color:rgba(245,158,11,0.3);color:var(--amber);background:rgba(245,158,11,0.06)}
.cat-cloud .tag{border-color:rgba(129,140,248,0.3);color:#818cf8;background:rgba(129,140,248,0.06)}
.cat-tool  .tag{border-color:rgba(100,116,139,0.25);color:var(--muted2);background:rgba(100,116,139,0.05)}

/* ===== PROJECTS ===== */
.proj-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(270px,1fr));gap:18px;margin-bottom:36px}
.proj-card{
  background:var(--bg2);border:1px solid var(--border);border-radius:16px;
  padding:26px;transition:all 0.3s;position:relative;overflow:hidden;cursor:default;
}
.proj-card::before{
  content:'';position:absolute;top:0;left:0;right:0;bottom:0;
  background:radial-gradient(circle at 50% 0%,rgba(0,229,255,0.06),transparent 60%);
  opacity:0;transition:opacity 0.35s;
}
.proj-card:hover{border-color:rgba(0,229,255,0.3);transform:translateY(-5px)}
.proj-card:hover::before{opacity:1}

.proj-badge{
  font-size:9px;letter-spacing:0.14em;margin-bottom:14px;
  display:inline-flex;align-items:center;gap:6px;
  color:var(--cyan);
}
.proj-badge::before{content:'';width:5px;height:5px;border-radius:50%;background:var(--cyan);box-shadow:0 0 6px var(--cyan)}
.proj-card h3{font-family:'Syne',sans-serif;font-size:17px;font-weight:700;color:#fff;margin-bottom:10px;line-height:1.3}
.proj-card p{font-size:12px;color:var(--muted2);line-height:1.8;margin-bottom:14px}
.proj-footer{display:flex;flex-wrap:wrap;gap:6px}
.mini-tag{font-size:10px;padding:3px 9px;border-radius:4px;background:rgba(255,255,255,0.05);color:var(--muted2);border:1px solid rgba(255,255,255,0.07)}

/* ===== STATS ===== */
.stats-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(155px,1fr));gap:12px;margin-bottom:36px}
.stat-card{
  background:var(--bg2);border:1px solid var(--border);border-radius:14px;
  padding:22px 16px;text-align:center;transition:all 0.3s;position:relative;overflow:hidden;
}
.stat-card::after{
  content:'';position:absolute;bottom:0;left:0;right:0;height:1px;
  background:linear-gradient(90deg,transparent,var(--cyan),transparent);
  transform:scaleX(0);transition:transform 0.3s;
}
.stat-card:hover{border-color:var(--border2);transform:translateY(-3px)}
.stat-card:hover::after{transform:scaleX(1)}
.stat-val{font-family:'Syne',sans-serif;font-size:38px;font-weight:800;color:var(--cyan);line-height:1;display:block}
.stat-lbl{font-size:9px;color:var(--muted);letter-spacing:0.12em;margin-top:6px;display:block}

/* ===== FOOTER ===== */
.footer{
  border-top:1px solid var(--border);padding-top:28px;margin-top:48px;
  display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:16px;
}
.footer-sig{font-family:'Syne',sans-serif;font-size:14px;color:var(--muted2)}
.footer-sig span{color:var(--cyan)}
.footer-quote{font-size:11px;color:var(--muted);font-style:italic;max-width:380px;text-align:right;line-height:1.6}

/* ===== FLOATING PARTICLES ===== */
.particle{
  position:fixed;pointer-events:none;border-radius:50%;z-index:1;
  animation:floatUp linear infinite;opacity:0;
}
@keyframes floatUp{
  0%{transform:translateY(0) translateX(0) scale(1);opacity:0}
  10%{opacity:0.6}
  90%{opacity:0.2}
  100%{transform:translateY(-100vh) translateX(var(--dx)) scale(0);opacity:0}
}

.divider{height:1px;background:var(--border);margin:28px 0}
</style>
</head>
<body>

<div id="scroll-bar"></div>
<div id="cursor-glow"></div>
<canvas id="bg-canvas"></canvas>
<div class="grid-overlay"></div>

<div class="content">

  <!-- HEADER -->
  <div class="header reveal">
    <div class="scan-line"></div>
    <div class="header-corner tl"></div>
    <div class="header-corner tr"></div>
    <div class="header-corner bl"></div>
    <div class="header-corner br"></div>

    <div class="status-badge" style="position:relative;z-index:2">
      <span class="status-dot"></span>
      AVAILABLE FOR COLLABORATION
    </div>

    <div class="name" style="position:relative;z-index:2">Vaibhaw Singh</div>

    <div class="role-row" style="position:relative;z-index:2">
      <span class="role-item">FULL-STACK DEV</span>
      <span class="role-sep">◆</span>
      <span class="role-item">MOBILE ENGINEER</span>
      <span class="role-sep">◆</span>
      <span class="role-item">BACKEND ARCHITECT</span>
      <span class="role-sep">◆</span>
      <span class="role-item">OSS CONTRIBUTOR</span>
    </div>

    <div class="typed-line" style="position:relative;z-index:2">
      <span id="typed"></span><span id="cursor"></span>
    </div>

    <div class="social-row" style="position:relative;z-index:2">
      <a class="social-btn" href="https://github.com/vaibhaw2003">⬡ GitHub</a>
      <a class="social-btn" href="#">⬡ LinkedIn</a>
      <a class="social-btn" href="#">⬡ Twitter</a>
      <a class="social-btn" href="#">⬡ Portfolio</a>
      <a class="social-btn" href="mailto:vaibhaw@email.com">⬡ Email</a>
    </div>
  </div>

  <!-- QUICK INFO -->
  <div class="sl reveal">QUICK INFO</div>
  <div class="info-grid reveal">
    <div class="info-card"><div class="ic-icon">🔭</div><div class="ic-title">WORKING ON</div><div class="ic-value">Flutter + Spring Boot Projects</div></div>
    <div class="info-card"><div class="ic-icon">🌱</div><div class="ic-title">LEARNING</div><div class="ic-value">DSA · Cloud · Microservices</div></div>
    <div class="info-card"><div class="ic-icon">🤝</div><div class="ic-title">SEEKING HELP WITH</div><div class="ic-value">System Design · Advanced Backend</div></div>
    <div class="info-card"><div class="ic-icon">⚡</div><div class="ic-title">FUN FACT</div><div class="ic-value">Debugs faster than he explains bugs</div></div>
  </div>

  <!-- BACKEND DEEP DIVE -->
  <div class="sl reveal">BACKEND EXPERTISE</div>
  <div class="backend-grid reveal">

    <!-- SPRING BOOT -->
    <div class="be-card spring">
      <div class="be-card-header">
        <div class="be-logo-row">
          <div class="be-logo">S</div>
          <div>
            <div class="be-name">Spring Boot</div>
            <div class="be-sub">JAVA ECOSYSTEM · ENTERPRISE GRADE</div>
          </div>
        </div>
        <span class="be-level">★ ADVANCED</span>
      </div>
      <div class="be-body">
        <p class="be-desc">Primary backend framework. Builds production-ready REST APIs and microservices with the full Spring ecosystem — Security, Data JPA, Actuator, and more.</p>
        <ul class="be-features">
          <li>RESTful API design with versioning and HATEOAS</li>
          <li>Spring Security + JWT / OAuth2 authentication flows</li>
          <li>Spring Data JPA with Hibernate ORM, custom queries</li>
          <li>Microservice architecture with Spring Cloud</li>
          <li>Exception handling, validation, and API documentation (Swagger/OpenAPI)</li>
          <li>Unit & integration testing with JUnit 5 + Mockito</li>
          <li>Docker-containerized Spring Boot deployments</li>
        </ul>
        <div class="be-tags">
          <span class="be-tag">Spring MVC</span>
          <span class="be-tag">Spring Security</span>
          <span class="be-tag">Spring Data JPA</span>
          <span class="be-tag">Spring Cloud</span>
          <span class="be-tag">Actuator</span>
          <span class="be-tag">Swagger</span>
          <span class="be-tag">Maven</span>
          <span class="be-tag">Gradle</span>
        </div>
      </div>
    </div>

    <!-- NODE.JS -->
    <div class="be-card node">
      <div class="be-card-header">
        <div class="be-logo-row">
          <div class="be-logo">N</div>
          <div>
            <div class="be-name">Node.js</div>
            <div class="be-sub">JAVASCRIPT RUNTIME · ASYNC FIRST</div>
          </div>
        </div>
        <span class="be-level">★ PROFICIENT</span>
      </div>
      <div class="be-body">
        <p class="be-desc">Builds fast, event-driven backends and real-time APIs. Uses Express.js for REST APIs and is exploring NestJS for scalable TypeScript backends.</p>
        <ul class="be-features">
          <li>Express.js REST APIs with middleware pipelines</li>
          <li>JWT-based auth, bcrypt password hashing</li>
          <li>Mongoose ODM with MongoDB for schema-based data modeling</li>
          <li>Socket.io for real-time bi-directional communication</li>
          <li>Rate limiting, CORS, Helmet.js for API hardening</li>
          <li>npm ecosystem, dotenv, nodemon, PM2 for process management</li>
          <li>Deployed on AWS EC2 / Render / Railway</li>
        </ul>
        <div class="be-tags">
          <span class="be-tag">Express.js</span>
          <span class="be-tag">NestJS</span>
          <span class="be-tag">Socket.io</span>
          <span class="be-tag">Mongoose</span>
          <span class="be-tag">JWT</span>
          <span class="be-tag">Multer</span>
          <span class="be-tag">Axios</span>
          <span class="be-tag">PM2</span>
        </div>
      </div>
    </div>

    <!-- FLASK -->
    <div class="be-card flask">
      <div class="be-card-header">
        <div class="be-logo-row">
          <div class="be-logo">F</div>
          <div>
            <div class="be-name">Flask</div>
            <div class="be-sub">PYTHON · MICROFRAMEWORK · ML BRIDGE</div>
          </div>
        </div>
        <span class="be-level">★ INTERMEDIATE</span>
      </div>
      <div class="be-body">
        <p class="be-desc">Uses Flask to expose ML/AI models as REST APIs and build lightweight backend services. Integrates Python's data science stack seamlessly with web backends.</p>
        <ul class="be-features">
          <li>RESTful routes with Flask Blueprints for modular structure</li>
          <li>Serving ML models (OpenCV, scikit-learn, TensorFlow) via API endpoints</li>
          <li>SQLAlchemy ORM for relational database integration</li>
          <li>Flask-JWT for token-based authentication</li>
          <li>File upload handling and image processing pipelines</li>
          <li>Deployed with Gunicorn + Nginx on Linux servers</li>
        </ul>
        <div class="be-tags">
          <span class="be-tag">Flask-RESTful</span>
          <span class="be-tag">SQLAlchemy</span>
          <span class="be-tag">Flask-JWT</span>
          <span class="be-tag">Gunicorn</span>
          <span class="be-tag">OpenCV</span>
          <span class="be-tag">scikit-learn</span>
          <span class="be-tag">Marshmallow</span>
        </div>
      </div>
    </div>

  </div>

  <!-- SKILL BARS -->
  <div class="skills-section reveal">
    <div class="sl">PROFICIENCY</div>
    <div class="skill-item"><div class="skill-head"><span class="skill-name">Java</span><span class="skill-pct">88%</span></div><div class="bar-track"><div class="bar-fill bar-java"></div></div></div>
    <div class="skill-item"><div class="skill-head"><span class="skill-name">Spring Boot</span><span class="skill-pct">83%</span></div><div class="bar-track"><div class="bar-fill bar-spring"></div></div></div>
    <div class="skill-item"><div class="skill-head"><span class="skill-name">Dart / Flutter</span><span class="skill-pct">80%</span></div><div class="bar-track"><div class="bar-fill bar-dart"></div></div></div>
    <div class="skill-item"><div class="skill-head"><span class="skill-name">Node.js</span><span class="skill-pct">72%</span></div><div class="bar-track"><div class="bar-fill bar-node"></div></div></div>
    <div class="skill-item"><div class="skill-head"><span class="skill-name">SQL / Databases</span><span class="skill-pct">70%</span></div><div class="bar-track"><div class="bar-fill bar-sql"></div></div></div>
    <div class="skill-item"><div class="skill-head"><span class="skill-name">React</span><span class="skill-pct">68%</span></div><div class="bar-track"><div class="bar-fill bar-react"></div></div></div>
    <div class="skill-item"><div class="skill-head"><span class="skill-name">Flask / Python</span><span class="skill-pct">65%</span></div><div class="bar-track"><div class="bar-fill bar-flask"></div></div></div>
    <div class="skill-item"><div class="skill-head"><span class="skill-name">Python (Data/AI)</span><span class="skill-pct">62%</span></div><div class="bar-track"><div class="bar-fill bar-python"></div></div></div>
  </div>

  <!-- FULL TECH STACK -->
  <div class="stack-section reveal">
    <div class="sl">FULL TECH STACK</div>
    <div class="cat-row cat-lang"><div class="cat-head"><span class="dot"></span>LANGUAGES</div><div class="tag-wrap"><span class="tag">Java</span><span class="tag">Dart</span><span class="tag">JavaScript</span><span class="tag">TypeScript</span><span class="tag">Python</span><span class="tag">C++</span><span class="tag">SQL</span><span class="tag">Bash</span></div></div>
    <div class="cat-row cat-front"><div class="cat-head"><span class="dot"></span>FRONTEND & MOBILE</div><div class="tag-wrap"><span class="tag">Flutter</span><span class="tag">React</span><span class="tag">HTML5</span><span class="tag">CSS3</span><span class="tag">Tailwind</span><span class="tag">GetX</span><span class="tag">Provider</span></div></div>
    <div class="cat-row cat-back"><div class="cat-head"><span class="dot"></span>BACKEND & APIs</div><div class="tag-wrap"><span class="tag">Spring Boot</span><span class="tag">Node.js</span><span class="tag">Express.js</span><span class="tag">Flask</span><span class="tag">REST API</span><span class="tag">GraphQL</span><span class="tag">WebSockets</span><span class="tag">JWT</span><span class="tag">OAuth2</span></div></div>
    <div class="cat-row cat-db"><div class="cat-head"><span class="dot"></span>DATABASES</div><div class="tag-wrap"><span class="tag">MySQL</span><span class="tag">PostgreSQL</span><span class="tag">MongoDB</span><span class="tag">Firebase</span><span class="tag">Redis</span><span class="tag">SQLite</span></div></div>
    <div class="cat-row cat-cloud"><div class="cat-head"><span class="dot"></span>CLOUD & DEVOPS</div><div class="tag-wrap"><span class="tag">AWS EC2</span><span class="tag">Docker</span><span class="tag">GitHub Actions</span><span class="tag">Nginx</span><span class="tag">Linux</span><span class="tag">CI/CD</span></div></div>
    <div class="cat-row cat-tool"><div class="cat-head"><span class="dot"></span>TOOLS</div><div class="tag-wrap"><span class="tag">IntelliJ IDEA</span><span class="tag">VS Code</span><span class="tag">Postman</span><span class="tag">Figma</span><span class="tag">Android Studio</span><span class="tag">Git</span></div></div>
  </div>

  <div class="divider"></div>

  <!-- PROJECTS -->
  <div class="sl reveal">FEATURED PROJECTS</div>
  <div class="proj-grid reveal">
    <div class="proj-card">
      <div class="proj-badge">IMAGE PROCESSING · ML</div>
      <h3>ALB-SENSE App</h3>
      <p>Detects albumin concentration from camera images using OpenCV pipelines. Flask backend serves the ML model as an API consumed by the Flutter client.</p>
      <div class="proj-footer"><span class="mini-tag">Flutter</span><span class="mini-tag">Flask</span><span class="mini-tag">OpenCV</span><span class="mini-tag">Python</span><span class="mini-tag">REST API</span></div>
    </div>
    <div class="proj-card">
      <div class="proj-badge">FINTECH · REAL-TIME</div>
      <h3>Currency Converter</h3>
      <p>Real-time multi-currency conversion with live exchange rate API, AdMob ads integration, and state management via GetX. Clean material design UI.</p>
      <div class="proj-footer"><span class="mini-tag">Flutter</span><span class="mini-tag">REST API</span><span class="mini-tag">AdMob</span><span class="mini-tag">GetX</span></div>
    </div>
    <div class="proj-card">
      <div class="proj-badge">COMPUTER VISION</div>
      <h3>Color Detection App</h3>
      <p>Extracts dominant and average RGB colors from images in real time. Useful for designers, accessibility checkers, and data labeling workflows.</p>
      <div class="proj-footer"><span class="mini-tag">Flutter</span><span class="mini-tag">Dart</span><span class="mini-tag">Image API</span></div>
    </div>
  </div>

  <!-- GITHUB STATS -->
  <div class="sl reveal">GITHUB STATS</div>
  <div class="stats-grid reveal">
    <div class="stat-card"><span class="stat-val" data-target="120">0</span><span class="stat-lbl">COMMITS THIS YEAR</span></div>
    <div class="stat-card"><span class="stat-val" data-target="18">0</span><span class="stat-lbl">REPOSITORIES</span></div>
    <div class="stat-card"><span class="stat-val" data-target="6">0</span><span class="stat-lbl">PULL REQUESTS</span></div>
    <div class="stat-card"><span class="stat-val" data-target="3">0</span><span class="stat-lbl">ISSUES OPENED</span></div>
    <div class="stat-card"><span class="stat-val" data-target="420">0</span><span class="stat-lbl">LINES PUSHED TODAY</span></div>
  </div>

  <!-- FOOTER -->
  <div class="footer reveal">
    <div class="footer-sig">⭐ From <span>Vaibhaw Singh</span></div>
    <div class="footer-quote">"The best code is no code. The second best is code that actually runs."</div>
  </div>

</div>

<script>
// ===== PARTICLE BACKGROUND =====
const canvas = document.getElementById('bg-canvas');
const ctx = canvas.getContext('2d');
let W, H;
function resize(){W=canvas.width=window.innerWidth;H=canvas.height=window.innerHeight}
resize();
window.addEventListener('resize',resize);

const CHARS='01アイウエオカサシスJAVASPRINGNODEFLASK<>{}[]();=>const let async await'.split('');
const cols=[];
function initCols(){cols.length=0;for(let x=20;x<W;x+=22)cols.push({x,y:Math.random()*H,speed:0.4+Math.random()*1.2,opacity:0.02+Math.random()*0.05})}
initCols();
window.addEventListener('resize',initCols);

function drawBg(){
  ctx.fillStyle='rgba(4,6,15,0.08)';
  ctx.fillRect(0,0,W,H);
  ctx.font='13px JetBrains Mono,monospace';
  cols.forEach(c=>{
    ctx.fillStyle=`rgba(0,229,255,${c.opacity})`;
    ctx.fillText(CHARS[Math.floor(Math.random()*CHARS.length)],c.x,c.y);
    c.y+=c.speed;
    if(c.y>H){c.y=0;c.opacity=0.02+Math.random()*0.05}
  });
}
setInterval(drawBg,50);

// ===== FLOATING PARTICLES =====
for(let i=0;i<18;i++){
  const p=document.createElement('div');
  p.className='particle';
  const size=1+Math.random()*3;
  const colors=['rgba(0,229,255,0.6)','rgba(168,85,247,0.6)','rgba(0,255,157,0.5)'];
  p.style.cssText=`
    left:${Math.random()*100}vw;bottom:-10px;
    width:${size}px;height:${size}px;
    background:${colors[Math.floor(Math.random()*colors.length)]};
    --dx:${(Math.random()-0.5)*120}px;
    animation-duration:${8+Math.random()*16}s;
    animation-delay:${Math.random()*10}s;
  `;
  document.body.appendChild(p);
}

// ===== CURSOR GLOW =====
const glow=document.getElementById('cursor-glow');
document.addEventListener('mousemove',e=>{
  glow.style.left=e.clientX+'px';
  glow.style.top=e.clientY+'px';
});

// ===== SCROLL PROGRESS =====
const bar=document.getElementById('scroll-bar');
window.addEventListener('scroll',()=>{
  const pct=(window.scrollY/(document.body.scrollHeight-window.innerHeight))*100;
  bar.style.width=pct+'%';
});

// ===== TYPING ANIMATION =====
const lines=[
  '> Building <span class="hl">scalable systems</span> with Spring Boot & Flutter.',
  '> Exploring <span class="hl">microservices, cloud</span>, and clean architecture.',
  '> Node.js + <span class="hl">Flask</span> for real-time & ML-powered APIs.',
  '> Debugs faster than he can <span class="hl">explain the bug.</span>',
  '> Open for <span class="hl">collaboration</span> on OSS and AI/ML projects.'
];
let li=0,ci=0,del=false,raw='';
const tel=document.getElementById('typed');
function type(){
  const stripped=lines[li].replace(/<[^>]+>/g,'');
  if(!del){
    raw=stripped.substring(0,++ci);
    const ratio=ci/stripped.length;
    const html=lines[li];
    const vis=Math.floor(html.replace(/<[^>]+>/g,'').length*ratio);
    let count=0,result='';
    for(let k=0;k<html.length;k++){
      if(html[k]==='<'){while(html[k]!=='>')result+=html[k++];result+=html[k];continue}
      if(count++<ci)result+=html[k];
    }
    tel.innerHTML=result;
    if(ci>=stripped.length){del=true;setTimeout(type,2200);return}
  }else{
    tel.innerHTML=tel.innerHTML.replace(/<[^>]+>/g,'').substring(0,--ci);
    if(ci===0){del=false;li=(li+1)%lines.length}
  }
  setTimeout(type,del?35:70);
}
type();

// ===== REVEAL ON SCROLL =====
const revEls=document.querySelectorAll('.reveal');
const revObs=new IntersectionObserver(entries=>{
  entries.forEach((e,i)=>{
    if(e.isIntersecting){
      setTimeout(()=>e.target.classList.add('visible'),i*60);
      revObs.unobserve(e.target);
    }
  });
},{threshold:0.08});
revEls.forEach(el=>revObs.observe(el));

// ===== BAR ANIMATIONS =====
const barObs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      e.target.querySelectorAll('.bar-fill').forEach((b,i)=>{
        setTimeout(()=>b.style.transform='scaleX(1)',i*120);
      });
      barObs.unobserve(e.target);
    }
  });
},{threshold:0.2});
document.querySelectorAll('.skills-section').forEach(s=>barObs.observe(s));

// ===== COUNTER ANIMATION =====
const ctrObs=new IntersectionObserver(entries=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      const t=+e.target.dataset.target;
      let c=0;
      const step=Math.max(1,Math.ceil(t/50));
      const iv=setInterval(()=>{
        c=Math.min(c+step,t);
        e.target.textContent=c;
        if(c>=t)clearInterval(iv);
      },28);
      ctrObs.unobserve(e.target);
    }
  });
},{threshold:0.5});
document.querySelectorAll('.stat-val[data-target]').forEach(el=>ctrObs.observe(el));
</script>
</body>
</html>

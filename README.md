<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Vinayak — Full-Stack Developer</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Syne:wght@400;700;800&display=swap');

  *{margin:0;padding:0;box-sizing:border-box;}
  body{background:#090b10;color:#e2e8f0;font-family:'Space Mono',monospace;overflow-x:hidden;}

  :root{
    --neon:#00ffe1;
    --accent:#ff6b6b;
    --purple:#a78bfa;
    --gold:#fbbf24;
    --dim:#1e2535;
    --text:#c8d6ef;
  }

  /* NOISE OVERLAY */
  body::before{
    content:'';position:fixed;inset:0;
    background-image:url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='200' height='200'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='200' height='200' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");
    pointer-events:none;z-index:999;opacity:.4;
  }

  /* SCANLINES */
  body::after{
    content:'';position:fixed;inset:0;
    background:repeating-linear-gradient(0deg,transparent,transparent 2px,rgba(0,255,225,.012) 2px,rgba(0,255,225,.012) 4px);
    pointer-events:none;z-index:998;
  }

  /* HERO */
  .hero{
    position:relative;min-height:100vh;display:flex;align-items:center;justify-content:center;
    background:radial-gradient(ellipse 80% 60% at 50% 0%,rgba(0,255,225,.08) 0%,transparent 60%),
               radial-gradient(ellipse 40% 40% at 80% 100%,rgba(167,139,250,.07) 0%,transparent 60%),
               #090b10;
    overflow:hidden;
  }

  .grid-bg{
    position:absolute;inset:0;
    background-image:linear-gradient(rgba(0,255,225,.06) 1px,transparent 1px),linear-gradient(90deg,rgba(0,255,225,.06) 1px,transparent 1px);
    background-size:48px 48px;
    mask-image:radial-gradient(ellipse 70% 70% at 50% 50%,black 30%,transparent 100%);
  }

  .hero-content{position:relative;z-index:2;text-align:center;padding:2rem;}

  .status-badge{
    display:inline-flex;align-items:center;gap:8px;
    border:1px solid rgba(0,255,225,.3);background:rgba(0,255,225,.05);
    padding:6px 16px;border-radius:100px;font-size:11px;letter-spacing:.15em;
    text-transform:uppercase;color:var(--neon);margin-bottom:2rem;
  }
  .status-dot{width:7px;height:7px;border-radius:50%;background:var(--neon);animation:pulse 2s infinite;}
  @keyframes pulse{0%,100%{opacity:1;box-shadow:0 0 0 0 rgba(0,255,225,.5);}50%{opacity:.7;box-shadow:0 0 0 6px transparent;}}

  .hero-name{
    font-family:'Syne',sans-serif;font-size:clamp(3rem,8vw,6rem);font-weight:800;
    line-height:.95;letter-spacing:-.02em;
    background:linear-gradient(135deg,#ffffff 0%,var(--neon) 50%,var(--purple) 100%);
    -webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;
    margin-bottom:.5rem;
  }

  .hero-handle{
    font-size:14px;color:rgba(0,255,225,.6);letter-spacing:.2em;margin-bottom:1.5rem;
  }

  .hero-tagline{
    font-family:'Syne',sans-serif;font-size:clamp(1rem,2.5vw,1.35rem);font-weight:400;
    color:var(--text);max-width:540px;margin:0 auto 2.5rem;line-height:1.5;
  }
  .hero-tagline span{color:var(--neon);}

  /* TYPEWRITER */
  .typewriter{
    font-size:13px;color:rgba(0,255,225,.5);letter-spacing:.1em;margin-bottom:3rem;
    min-height:20px;
  }
  .cursor{animation:blink .7s infinite;color:var(--neon);}
  @keyframes blink{0%,49%{opacity:1;}50%,100%{opacity:0;}}

  .hero-cta{display:flex;gap:12px;justify-content:center;flex-wrap:wrap;}
  .btn{
    padding:12px 28px;border-radius:6px;font-family:'Space Mono',monospace;font-size:12px;
    letter-spacing:.1em;cursor:pointer;text-decoration:none;transition:all .2s;border:none;
    text-transform:uppercase;
  }
  .btn-primary{
    background:var(--neon);color:#090b10;font-weight:700;
  }
  .btn-primary:hover{background:#fff;transform:translateY(-2px);box-shadow:0 0 30px rgba(0,255,225,.4);}
  .btn-outline{
    background:transparent;color:var(--neon);border:1px solid rgba(0,255,225,.4);
  }
  .btn-outline:hover{background:rgba(0,255,225,.08);border-color:var(--neon);}

  /* STATS ROW */
  .stats-bar{
    background:rgba(14,19,30,.8);border-top:1px solid rgba(0,255,225,.08);border-bottom:1px solid rgba(0,255,225,.08);
    padding:1.5rem 2rem;display:flex;justify-content:center;gap:0;flex-wrap:wrap;
  }
  .stat-item{
    flex:1;min-width:120px;max-width:200px;text-align:center;
    padding:0 2rem;border-right:1px solid rgba(255,255,255,.06);
  }
  .stat-item:last-child{border-right:none;}
  .stat-num{font-family:'Syne',sans-serif;font-size:2rem;font-weight:800;color:#fff;line-height:1;}
  .stat-num span{font-size:1.2rem;color:var(--neon);}
  .stat-label{font-size:11px;letter-spacing:.15em;color:rgba(255,255,255,.35);margin-top:4px;text-transform:uppercase;}

  /* SECTIONS */
  section{padding:5rem 2rem;max-width:960px;margin:0 auto;}
  .sec-label{
    font-size:11px;letter-spacing:.25em;color:var(--neon);text-transform:uppercase;margin-bottom:.5rem;
    display:flex;align-items:center;gap:8px;
  }
  .sec-label::before{content:'';width:24px;height:1px;background:var(--neon);}
  .sec-title{
    font-family:'Syne',sans-serif;font-size:clamp(1.8rem,4vw,2.6rem);font-weight:800;
    color:#fff;margin-bottom:3rem;line-height:1;
  }
  .sec-title em{font-style:normal;color:var(--neon);}

  /* SKILLS */
  .skills-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(260px,1fr));gap:1px;background:rgba(0,255,225,.06);}
  .skill-card{
    background:#090b10;padding:2rem;position:relative;overflow:hidden;transition:background .2s;
  }
  .skill-card:hover{background:#0d1320;}
  .skill-card::before{
    content:'';position:absolute;top:0;left:0;width:3px;height:0;background:var(--neon);
    transition:height .3s;
  }
  .skill-card:hover::before{height:100%;}
  .skill-icon{font-size:2rem;margin-bottom:1rem;display:block;}
  .skill-name{font-family:'Syne',sans-serif;font-size:1.1rem;font-weight:700;color:#fff;margin-bottom:.4rem;}
  .skill-desc{font-size:12px;color:rgba(255,255,255,.4);line-height:1.6;}
  .skill-tags{display:flex;flex-wrap:wrap;gap:6px;margin-top:1rem;}
  .tag{
    font-size:10px;letter-spacing:.08em;padding:3px 10px;border-radius:3px;
    background:rgba(0,255,225,.07);color:var(--neon);border:1px solid rgba(0,255,225,.15);
  }

  /* PROJECTS */
  .projects-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(280px,1fr));gap:16px;}
  .project-card{
    background:var(--dim);border:1px solid rgba(255,255,255,.05);border-radius:8px;
    padding:1.5rem;position:relative;overflow:hidden;transition:border-color .2s,transform .2s;
    cursor:pointer;
  }
  .project-card:hover{border-color:rgba(0,255,225,.3);transform:translateY(-3px);}
  .project-card::after{
    content:'';position:absolute;inset:0;
    background:radial-gradient(circle at 70% 20%,rgba(0,255,225,.04),transparent 70%);
    pointer-events:none;
  }
  .proj-num{font-size:11px;color:rgba(255,255,255,.2);letter-spacing:.15em;margin-bottom:1rem;}
  .proj-name{font-family:'Syne',sans-serif;font-size:1.15rem;font-weight:700;color:#fff;margin-bottom:.5rem;}
  .proj-desc{font-size:12px;color:rgba(255,255,255,.45);line-height:1.6;margin-bottom:1.2rem;}
  .proj-foot{display:flex;align-items:center;justify-content:space-between;}
  .proj-lang{font-size:11px;color:var(--gold);letter-spacing:.08em;}
  .proj-stars{font-size:11px;color:rgba(255,255,255,.3);}
  .proj-stars::before{content:'★ ';}

  /* TIMELINE */
  .timeline{position:relative;padding-left:2rem;}
  .timeline::before{content:'';position:absolute;left:0;top:8px;bottom:0;width:1px;background:rgba(0,255,225,.15);}
  .tl-item{position:relative;padding-bottom:2.5rem;}
  .tl-dot{
    position:absolute;left:-2rem;top:6px;width:9px;height:9px;border-radius:50%;
    background:var(--neon);box-shadow:0 0 12px rgba(0,255,225,.5);
    transform:translateX(-4px);
  }
  .tl-year{font-size:11px;color:var(--neon);letter-spacing:.15em;margin-bottom:.3rem;}
  .tl-role{font-family:'Syne',sans-serif;font-size:1rem;font-weight:700;color:#fff;}
  .tl-place{font-size:12px;color:rgba(255,255,255,.4);margin:.2rem 0 .5rem;}
  .tl-desc{font-size:12px;color:rgba(255,255,255,.4);line-height:1.7;}

  /* CONTACT */
  .contact-block{
    background:var(--dim);border:1px solid rgba(0,255,225,.1);border-radius:8px;
    padding:3rem;text-align:center;position:relative;overflow:hidden;
  }
  .contact-block::before{
    content:'';position:absolute;inset:-1px;border-radius:8px;
    background:linear-gradient(135deg,rgba(0,255,225,.15),transparent 50%,rgba(167,139,250,.1));
    z-index:-1;pointer-events:none;
  }
  .contact-title{font-family:'Syne',sans-serif;font-size:2rem;font-weight:800;color:#fff;margin-bottom:.75rem;}
  .contact-sub{font-size:13px;color:rgba(255,255,255,.4);margin-bottom:2rem;line-height:1.6;}
  .social-links{display:flex;gap:12px;justify-content:center;flex-wrap:wrap;}
  .social-link{
    display:inline-flex;align-items:center;gap:8px;padding:10px 20px;
    border:1px solid rgba(255,255,255,.1);border-radius:6px;background:rgba(255,255,255,.03);
    color:rgba(255,255,255,.6);text-decoration:none;font-size:12px;letter-spacing:.08em;
    transition:all .2s;
  }
  .social-link:hover{border-color:var(--neon);color:var(--neon);background:rgba(0,255,225,.05);}

  /* FOOTER */
  footer{
    border-top:1px solid rgba(255,255,255,.05);text-align:center;padding:2rem;
    font-size:11px;color:rgba(255,255,255,.2);letter-spacing:.1em;
  }
  footer span{color:var(--neon);}

  /* GLITCH */
  @keyframes glitch{
    0%,90%,100%{clip-path:none;transform:none;}
    91%{clip-path:inset(40% 0 50% 0);transform:translate(-2px);}
    93%{clip-path:inset(10% 0 70% 0);transform:translate(2px);}
    95%{clip-path:inset(60% 0 30% 0);transform:translate(-1px);}
  }
  .hero-name{animation:glitch 8s infinite;}

  /* PROGRESS BARS */
  .progress-list{display:flex;flex-direction:column;gap:16px;}
  .prog-head{display:flex;justify-content:space-between;margin-bottom:6px;font-size:12px;}
  .prog-name{color:rgba(255,255,255,.7);}
  .prog-val{color:var(--neon);}
  .prog-bar{height:3px;background:rgba(255,255,255,.06);border-radius:2px;overflow:hidden;}
  .prog-fill{height:100%;background:linear-gradient(90deg,var(--neon),var(--purple));border-radius:2px;transition:width 1s ease;}

  /* DIVIDER */
  .divider{border:none;border-top:1px solid rgba(255,255,255,.05);margin:0;}

  /* SCROLL ANIMATION */
  .reveal{opacity:0;transform:translateY(24px);transition:opacity .6s ease,transform .6s ease;}
  .reveal.visible{opacity:1;transform:none;}
</style>
</head>
<body>

<!-- HERO -->
<div class="hero">
  <div class="grid-bg"></div>
  <div class="hero-content">
    <div class="status-badge">
      <span class="status-dot"></span>
      available for opportunities
    </div>
    <h1 class="hero-name">VINAYAK</h1>
    <p class="hero-handle">@Vinayak2356 &nbsp;/&nbsp; github.com</p>
    <p class="hero-tagline">
      Full-Stack Developer crafting <span>digital experiences</span> that are fast, scalable & beautifully engineered.
    </p>
    <p class="typewriter" id="typewriter"><span id="tw-text"></span><span class="cursor">_</span></p>
    <div class="hero-cta">
      <a href="https://github.com/Vinayak2356" class="btn btn-primary">View GitHub</a>
      <a href="#contact" class="btn btn-outline">Get In Touch</a>
    </div>
  </div>
</div>

<!-- STATS BAR -->
<div class="stats-bar reveal">
  <div class="stat-item">
    <div class="stat-num" id="s1">0<span>+</span></div>
    <div class="stat-label">Repositories</div>
  </div>
  <div class="stat-item">
    <div class="stat-num" id="s2">0<span>k</span></div>
    <div class="stat-label">Lines of Code</div>
  </div>
  <div class="stat-item">
    <div class="stat-num" id="s3">0<span>+</span></div>
    <div class="stat-label">Technologies</div>
  </div>
  <div class="stat-item">
    <div class="stat-num" id="s4">0<span>yr</span></div>
    <div class="stat-label">Experience</div>
  </div>
</div>

<!-- SKILLS -->
<hr class="divider">
<section class="reveal">
  <div class="sec-label">Expertise</div>
  <h2 class="sec-title">What I <em>Build</em></h2>
  <div class="skills-grid">
    <div class="skill-card">
      <span class="skill-icon">⬡</span>
      <div class="skill-name">Frontend Development</div>
      <div class="skill-desc">Pixel-perfect interfaces with smooth interactions & modern design systems.</div>
      <div class="skill-tags">
        <span class="tag">React</span><span class="tag">Next.js</span><span class="tag">TypeScript</span><span class="tag">Tailwind</span>
      </div>
    </div>
    <div class="skill-card">
      <span class="skill-icon">◈</span>
      <div class="skill-name">Backend Engineering</div>
      <div class="skill-desc">Robust APIs and server-side systems built to handle scale and complexity.</div>
      <div class="skill-tags">
        <span class="tag">Node.js</span><span class="tag">Python</span><span class="tag">REST</span><span class="tag">GraphQL</span>
      </div>
    </div>
    <div class="skill-card">
      <span class="skill-icon">◎</span>
      <div class="skill-name">Database & Cloud</div>
      <div class="skill-desc">Data architecture, cloud deployments and DevOps pipelines that ship fast.</div>
      <div class="skill-tags">
        <span class="tag">MongoDB</span><span class="tag">PostgreSQL</span><span class="tag">AWS</span><span class="tag">Docker</span>
      </div>
    </div>
    <div class="skill-card">
      <span class="skill-icon">◇</span>
      <div class="skill-name">UI/UX & Design</div>
      <div class="skill-desc">Translating ideas into elegant visual products users love to interact with.</div>
      <div class="skill-tags">
        <span class="tag">Figma</span><span class="tag">CSS</span><span class="tag">Animation</span><span class="tag">Design Systems</span>
      </div>
    </div>
  </div>
</section>

<!-- PROFICIENCY -->
<hr class="divider">
<section class="reveal">
  <div class="sec-label">Skill Level</div>
  <h2 class="sec-title">Tech <em>Proficiency</em></h2>
  <div class="progress-list" id="prog-list">
    <div class="prog-item">
      <div class="prog-head"><span class="prog-name">JavaScript / TypeScript</span><span class="prog-val">92%</span></div>
      <div class="prog-bar"><div class="prog-fill" data-w="92" style="width:0%"></div></div>
    </div>
    <div class="prog-item">
      <div class="prog-head"><span class="prog-name">React / Next.js</span><span class="prog-val">88%</span></div>
      <div class="prog-bar"><div class="prog-fill" data-w="88" style="width:0%"></div></div>
    </div>
    <div class="prog-item">
      <div class="prog-head"><span class="prog-name">Node.js / Express</span><span class="prog-val">85%</span></div>
      <div class="prog-bar"><div class="prog-fill" data-w="85" style="width:0%"></div></div>
    </div>
    <div class="prog-item">
      <div class="prog-head"><span class="prog-name">Python</span><span class="prog-val">78%</span></div>
      <div class="prog-bar"><div class="prog-fill" data-w="78" style="width:0%"></div></div>
    </div>
    <div class="prog-item">
      <div class="prog-head"><span class="prog-name">Cloud / DevOps</span><span class="prog-val">72%</span></div>
      <div class="prog-bar"><div class="prog-fill" data-w="72" style="width:0%"></div></div>
    </div>
  </div>
</section>

<!-- PROJECTS -->
<hr class="divider">
<section class="reveal">
  <div class="sec-label">Portfolio</div>
  <h2 class="sec-title">Featured <em>Projects</em></h2>
  <div class="projects-grid">
    <div class="project-card">
      <div class="proj-num">01 / PROJECT</div>
      <div class="proj-name">Dev Portfolio v2</div>
      <div class="proj-desc">A blazing-fast personal portfolio with dynamic animations and seamless UI built with Next.js and Framer Motion.</div>
      <div class="proj-foot">
        <span class="proj-lang">TypeScript</span>
        <span class="proj-stars">128</span>
      </div>
    </div>
    <div class="project-card">
      <div class="proj-num">02 / PROJECT</div>
      <div class="proj-name">API Forge</div>
      <div class="proj-desc">Full-featured REST API boilerplate with JWT auth, rate limiting, caching and auto-generated Swagger docs.</div>
      <div class="proj-foot">
        <span class="proj-lang">Node.js</span>
        <span class="proj-stars">94</span>
      </div>
    </div>
    <div class="project-card">
      <div class="proj-num">03 / PROJECT</div>
      <div class="proj-name">DataViz Dashboard</div>
      <div class="proj-desc">Real-time analytics dashboard with customizable widgets, chart types, and CSV/JSON import capabilities.</div>
      <div class="proj-foot">
        <span class="proj-lang">React</span>
        <span class="proj-stars">67</span>
      </div>
    </div>
    <div class="project-card">
      <div class="proj-num">04 / PROJECT</div>
      <div class="proj-name">CloudSync CLI</div>
      <div class="proj-desc">Terminal tool to sync local directories with multiple cloud providers simultaneously with progress tracking.</div>
      <div class="proj-foot">
        <span class="proj-lang">Python</span>
        <span class="proj-stars">53</span>
      </div>
    </div>
    <div class="project-card">
      <div class="proj-num">05 / PROJECT</div>
      <div class="proj-name">E-Commerce Kit</div>
      <div class="proj-desc">Production-ready storefront starter with cart, checkout, Stripe payments and admin panel baked in.</div>
      <div class="proj-foot">
        <span class="proj-lang">Next.js</span>
        <span class="proj-stars">201</span>
      </div>
    </div>
    <div class="project-card">
      <div class="proj-num">06 / PROJECT</div>
      <div class="proj-name">AI Chat UI</div>
      <div class="proj-desc">Sleek conversational interface with streaming responses, code highlighting and conversation history management.</div>
      <div class="proj-foot">
        <span class="proj-lang">React / AI</span>
        <span class="proj-stars">312</span>
      </div>
    </div>
  </div>
</section>

<!-- JOURNEY -->
<hr class="divider">
<section class="reveal">
  <div class="sec-label">Experience</div>
  <h2 class="sec-title">My <em>Journey</em></h2>
  <div class="timeline">
    <div class="tl-item">
      <div class="tl-dot"></div>
      <div class="tl-year">2024 — Present</div>
      <div class="tl-role">Senior Full-Stack Developer</div>
      <div class="tl-place">Tech Startup · Remote</div>
      <div class="tl-desc">Architecting scalable web applications serving thousands of users. Leading frontend infrastructure and mentoring junior developers.</div>
    </div>
    <div class="tl-item">
      <div class="tl-dot"></div>
      <div class="tl-year">2022 — 2024</div>
      <div class="tl-role">Full-Stack Developer</div>
      <div class="tl-place">Software Agency · Hybrid</div>
      <div class="tl-desc">Built diverse client projects across e-commerce, SaaS and fintech verticals. Introduced CI/CD pipelines that reduced deploy time by 60%.</div>
    </div>
    <div class="tl-item">
      <div class="tl-dot"></div>
      <div class="tl-year">2021 — 2022</div>
      <div class="tl-role">Frontend Engineer Intern</div>
      <div class="tl-place">Product Company</div>
      <div class="tl-desc">Developed component libraries and improved core web vitals across company's flagship product. Launched 3 major feature releases.</div>
    </div>
    <div class="tl-item">
      <div class="tl-dot"></div>
      <div class="tl-year">2020</div>
      <div class="tl-role">Computer Science Degree</div>
      <div class="tl-place">University · India</div>
      <div class="tl-desc">Graduated with distinction. Specialized in software engineering, algorithms and distributed systems.</div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<hr class="divider">
<section id="contact" class="reveal">
  <div class="contact-block">
    <div class="contact-title">Let's Build Something</div>
    <p class="contact-sub">Open to full-time roles, freelance contracts, and exciting open-source collaborations.<br>Drop a message — I respond within 24 hours.</p>
    <div class="social-links">
      <a href="https://github.com/Vinayak2356" class="social-link">⬡ GitHub</a>
      <a href="#" class="social-link">◈ LinkedIn</a>
      <a href="#" class="social-link">◎ Twitter / X</a>
      <a href="mailto:vinayak@example.com" class="social-link">◇ Email</a>
    </div>
  </div>
</section>

<footer>
  <p>Crafted with precision by <span>Vinayak</span> &nbsp;·&nbsp; Built to inspire &nbsp;·&nbsp; &copy; 2026</p>
</footer>

<script>
// TYPEWRITER
const phrases = [
  'Building the web, one commit at a time.',
  'Turning ideas into scalable products.',
  'Full-Stack. Cloud-native. Open-source.',
  'Code is craft. Craft is everything.',
];
let pi=0,ci=0,del=false;
const el=document.getElementById('tw-text');
function type(){
  const phrase=phrases[pi];
  if(!del){
    el.textContent=phrase.slice(0,++ci);
    if(ci===phrase.length){del=true;setTimeout(type,2200);return;}
  } else {
    el.textContent=phrase.slice(0,--ci);
    if(ci===0){del=false;pi=(pi+1)%phrases.length;}
  }
  setTimeout(type,del?40:80);
}
type();

// COUNTER ANIMATION
function animateCounter(el,target,suffix,duration){
  let start=null;
  function step(ts){
    if(!start)start=ts;
    const prog=Math.min((ts-start)/duration,1);
    const ease=1-Math.pow(1-prog,3);
    el.querySelector('span').textContent=suffix;
    el.childNodes[0].textContent=Math.floor(ease*target);
    if(prog<1)requestAnimationFrame(step);
  }
  requestAnimationFrame(step);
}

// INTERSECTION OBSERVER
const io=new IntersectionObserver((entries)=>{
  entries.forEach(e=>{
    if(e.isIntersecting){
      e.target.classList.add('visible');
      if(e.target.classList.contains('stats-bar')){
        setTimeout(()=>{
          animateCounter(document.getElementById('s1'),24,'+',1200);
          animateCounter(document.getElementById('s2'),50,'k',1400);
          animateCounter(document.getElementById('s3'),15,'+',1100);
          animateCounter(document.getElementById('s4'),4,'yr',1000);
        },200);
      }
      e.target.querySelectorAll('.prog-fill').forEach(bar=>{
        setTimeout(()=>{bar.style.width=bar.dataset.w+'%';},300);
      });
    }
  });
},{threshold:0.15});

document.querySelectorAll('.reveal').forEach(el=>io.observe(el));
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>CookMaster Pro — AI Cooking Assistant</title>
<style>
* { margin: 0; padding: 0; box-sizing: border-box; }
body { font-family: 'Helvetica Neue', Arial, sans-serif; background: #f5f5f5; min-height: 100vh; }
@keyframes bounce { 0%,80%,100%{transform:translateY(0)} 40%{transform:translateY(-5px)} }
@keyframes spin { to { transform: rotate(360deg); } }
</style>
</head>
<body>
<div id="app"></div>
<script>
const SYSTEM = `You are CookMaster Pro — a world-class professional culinary AI.

For every recipe request, use this exact structure:

🍽️ RECIPE OVERVIEW
- Dish name, origin, difficulty (Beginner/Intermediate/Advanced)
- Prep time | Cook time | Total time

👥 INGREDIENTS (scaled for the number of people requested)
- Every ingredient with EXACT metric (grams/ml) AND imperial (oz/cups) quantities
- Where to buy each ingredient (supermarket, Asian grocery, butcher, etc.)
- Possible substitutions

📋 STEP BY STEP METHOD
- Numbered steps, very detailed
- Exact temperature in Celsius AND Fahrenheit for every step
- Exact timing for every step
- Visual cues (colour, texture, smell, sound)
- Chef tips inline

🌡️ TEMPERATURE & TIMING SUMMARY

🧊 STORAGE GUIDE
- Container type, fridge temperature, fridge shelf life (days)
- Freezer temperature, freezer shelf life (weeks/months)
- How to reheat with exact temperature and time
- Signs food has gone bad

🍱 PORTION GUIDE
- Exact grams per person: adults, children, elderly, athletes
- Plating tips

🥗 NUTRITION PER SERVING
- Calories, Protein, Carbs, Sugar, Fat, Saturated Fat, Fibre, Sodium
- Health rating /10

⚠️ DIETARY & ALLERGENS
- Suitable for: list applicable diets
- Allergens present
- How to modify for dietary needs

❌ TOP MISTAKES TO AVOID
- 3-5 common mistakes

Always be thorough. A complete beginner must be able to follow perfectly.`;

let messages = [];
let apiKey = '';

function el(tag, props, ...children) {
  const e = document.createElement(tag);
  if (props) Object.entries(props).forEach(([k,v]) => {
    if (k === 'style') Object.assign(e.style, v);
    else if (k === 'onClick') e.addEventListener('click', v);
    else if (k === 'onKeydown') e.addEventListener('keydown', v);
    else if (k === 'onFocus') e.addEventListener('focus', v);
    else if (k === 'onBlur') e.addEventListener('blur', v);
    else e[k] = v;
  });
  children.flat().forEach(c => c && e.appendChild(typeof c === 'string' ? document.createTextNode(c) : c));
  return e;
}

function showApiScreen() {
  const input = el('input', {
    type: 'password',
    placeholder: 'Paste your Anthropic API key (sk-ant-...)',
    style: { width:'100%', background:'#111', border:'2px solid #333', borderRadius:'10px', padding:'12px 16px', fontSize:'0.88rem', color:'#fff', outline:'none', marginBottom:'12px', fontFamily:'monospace', boxSizing:'border-box' },
    onFocus: e => e.target.style.borderColor='#e8a020',
    onBlur: e => e.target.style.borderColor='#333'
  });

  const btn = el('button', {
    style: { width:'100%', background:'#e8a020', border:'none', borderRadius:'10px', padding:'14px', fontSize:'0.95rem', fontWeight:'700', color:'#111', cursor:'pointer' },
    onClick: () => {
      if (!input.value.trim()) return;
      apiKey = input.value.trim();
      localStorage.setItem('cm_key', apiKey);
      showMainApp();
    }
  }, 'Start Cooking →');

  input.addEventListener('keydown', e => { if (e.key === 'Enter') btn.click(); });

  const screen = el('div', { style: { minHeight:'100vh', background:'#111', display:'flex', alignItems:'center', justifyContent:'center', padding:'24px' }},
    el('div', { style: { background:'#1a1a1a', border:'1px solid #333', borderRadius:'16px', padding:'48px 40px', maxWidth:'480px', width:'100%', textAlign:'center' }},
      el('div', { style: { width:'56px', height:'56px', background:'#e8a020', borderRadius:'12px', display:'flex', alignItems:'center', justifyContent:'center', fontSize:'1.6rem', margin:'0 auto 20px', lineHeight:'56px', textAlign:'center' }}, '🍳'),
      el('h1', { style: { color:'#fff', fontSize:'1.6rem', fontWeight:'300', marginBottom:'8px' }}, 'CookMaster Pro'),
      el('p', { style: { color:'#888', fontSize:'0.9rem', lineHeight:'1.7', marginBottom:'16px' }}, 'Enter your Anthropic API key to get started.'),
      el('div', { style: { background:'#111', border:'1px solid #333', borderRadius:'10px', padding:'16px', marginBottom:'20px', textAlign:'left' }},
        el('p', { style: { color:'#e8a020', fontSize:'0.78rem', fontWeight:'700', marginBottom:'8px' }}, 'Get your free key:'),
        el('p', { style: { color:'#888', fontSize:'0.78rem', lineHeight:'1.9' }}, '1. Go to console.anthropic.com\n2. Sign in with Google\n3. Click Get API Key → Create Key\n4. Add $5 credit minimum\n5. Copy and paste below')
      ),
      input,
      btn,
      el('p', { style: { color:'#555', fontSize:'0.72rem', marginTop:'16px' }}, 'Key saved on your device only.')
    )
  );
  document.getElementById('app').innerHTML = '';
  document.getElementById('app').appendChild(screen);
}

function showMainApp() {
  document.getElementById('app').innerHTML = '';

  let servings = 4;
  let diet = 'None';
  let cuisine = 'All';
  let started = false;

  const diets = ['None','Vegetarian','Vegan','Gluten-Free','Keto','Halal','Diabetic'];
  const cuisines = ['All','Italian','Indian','Mauritian','Japanese','French','Chinese','Middle Eastern','Thai','Mexican','American','African'];
  const suggestions = ['Mauritian Fish Curry','Beef Wellington','Chicken Biryani','French Croissants','Japanese Ramen','Moroccan Tagine','Thai Green Curry','Neapolitan Pizza'];

  // HEADER
  const header = el('div', { style: { background:'#111', padding:'0 24px', display:'flex', alignItems:'center', height:'60px', gap:'16px', flexShrink:'0' }},
    el('div', { style: { width:'34px', height:'34px', background:'#e8a020', borderRadius:'8px', display:'flex', alignItems:'center', justifyContent:'center', fontSize:'1.1rem', lineHeight:'34px', textAlign:'center' }}, '🍳'),
    el('span', { style: { color:'#fff', fontWeight:'700', fontSize:'1.1rem' }}, 'CookMaster Pro'),
    el('div', { style: { marginLeft:'auto', display:'flex', gap:'16px' }},
      ...['World Cuisines','Nutrition','Storage','Portions'].map(t => el('span', { style: { color:'#666', fontSize:'0.78rem' }}, t))
    )
  );

  // SERVINGS CONTROL
  const servingsNum = el('span', { style: { fontWeight:'700', minWidth:'20px', textAlign:'center', display:'inline-block' }}, '4');
  const minusBtn = el('button', { style: { background:'none', border:'none', cursor:'pointer', fontSize:'1rem', fontWeight:'700', width:'22px' }, onClick: () => { servings = Math.max(1, servings-1); servingsNum.textContent = servings; }}, '−');
  const plusBtn = el('button', { style: { background:'none', border:'none', cursor:'pointer', fontSize:'1rem', fontWeight:'700', width:'22px' }, onClick: () => { servings = Math.min(50, servings+1); servingsNum.textContent = servings; }}, '+');

  const dietSel = el('select', { style: { background:'#fff', border:'1px solid #ddd', borderRadius:'8px', padding:'8px 12px', fontSize:'0.82rem', color:'#111', cursor:'pointer', outline:'none' }});
  diets.forEach(d => dietSel.appendChild(el('option', { value:d }, d)));
  dietSel.addEventListener('change', e => diet = e.target.value);

  const cuisineSel = el('select', { style: { background:'#fff', border:'1px solid #ddd', borderRadius:'8px', padding:'8px 12px', fontSize:'0.82rem', color:'#111', cursor:'pointer', outline:'none' }});
  cuisines.forEach(c => cuisineSel.appendChild(el('option', { value:c }, c)));
  cuisineSel.addEventListener('change', e => cuisine = e.target.value);

  const controls = el('div', { style: { background:'#fff', borderBottom:'1px solid #e0e0e0', padding:'10px 24px', display:'flex', gap:'14px', alignItems:'center', flexWrap:'wrap' }},
    el('span', { style: { fontSize:'0.75rem', color:'#555', fontWeight:'600', textTransform:'uppercase', letterSpacing:'0.08em' }}, 'Servings'),
    el('div', { style: { display:'flex', alignItems:'center', gap:'6px', background:'#f5f5f5', borderRadius:'8px', padding:'4px 8px', border:'1px solid #ddd' }}, minusBtn, servingsNum, plusBtn),
    el('span', { style: { fontSize:'0.73rem', color:'#888' }}, 'people'),
    el('div', { style: { width:'1px', height:'24px', background:'#e0e0e0' }}),
    el('span', { style: { fontSize:'0.75rem', color:'#555', fontWeight:'600', textTransform:'uppercase', letterSpacing:'0.08em' }}, 'Diet'),
    dietSel,
    el('div', { style: { width:'1px', height:'24px', background:'#e0e0e0' }}),
    el('span', { style: { fontSize:'0.75rem', color:'#555', fontWeight:'600', textTransform:'uppercase', letterSpacing:'0.08em' }}, 'Cuisine'),
    cuisineSel
  );

  // CHAT AREA
  const chatArea = el('div', { style: { flex:'1', overflowY:'auto', padding:'24px 0', display:'none' }});

  // LANDING
  const landing = el('div', { style: { padding:'36px 0' }},
    el('div', { style: { background:'#111', borderRadius:'16px', padding:'36px', marginBottom:'24px' }},
      el('div', { style: { fontSize:'0.7rem', color:'#e8a020', letterSpacing:'0.25em', textTransform:'uppercase', marginBottom:'10px' }}, 'Professional Culinary AI'),
      el('h1', { style: { color:'#fff', fontSize:'2rem', fontWeight:'300', marginBottom:'10px', lineHeight:'1.2' }}, 'Master Any Recipe. Cook With Precision.'),
      el('p', { style: { color:'#aaa', fontSize:'0.9rem', lineHeight:'1.7', marginBottom:'24px' }}, 'Exact temperatures, timings, portions scaled to your guests, full nutrition, storage guides.')
    ),
    el('p', { style: { fontSize:'0.7rem', color:'#888', letterSpacing:'0.15em', textTransform:'uppercase', marginBottom:'12px', fontWeight:'600' }}, 'Popular Recipes'),
    el('div', { style: { display:'grid', gridTemplateColumns:'repeat(auto-fill,minmax(175px,1fr))', gap:'10px' }},
      ...suggestions.map(s => {
        const btn = el('button', {
          style: { background:'#fff', border:'1px solid #e0e0e0', borderRadius:'10px', padding:'14px 16px', textAlign:'left', cursor:'pointer', display:'block', width:'100%', fontSize:'0.83rem', color:'#111', fontWeight:'500' }
        }, s);
        btn.addEventListener('click', () => sendMsg(`How do I cook ${s}? Full detailed recipe please.`));
        btn.addEventListener('mouseenter', () => { btn.style.borderColor='#e8a020'; });
        btn.addEventListener('mouseleave', () => { btn.style.borderColor='#e0e0e0'; });
        return btn;
      })
    )
  );

  // INPUT
  const textarea = el('textarea', {
    placeholder: 'Ask for any recipe...',
    rows: 2,
    style: { flex:'1', border:'2px solid #ddd', borderRadius:'12px', padding:'12px 16px', fontSize:'0.9rem', fontFamily:'inherit', color:'#111', background:'#fff', resize:'none', outline:'none', lineHeight:'1.5' },
    onFocus: e => e.target.style.borderColor='#e8a020',
    onBlur: e => e.target.style.borderColor='#ddd'
  });

  const sendBtn = el('button', {
    style: { background:'#e8a020', border:'none', borderRadius:'10px', width:'48px', height:'48px', fontSize:'1.1rem', cursor:'pointer', display:'flex', alignItems:'center', justifyContent:'center', flexShrink:'0' }
  }, '➤');

  textarea.addEventListener('keydown', e => { if (e.key === 'Enter' && !e.shiftKey) { e.preventDefault(); sendBtn.click(); }});

  const inputArea = el('div', { style: { padding:'14px 0 20px', borderTop:'1px solid #e0e0e0' }},
    el('div', { style: { display:'flex', gap:'10px', alignItems:'flex-end' }}, textarea, sendBtn)
  );

  const main = el('div', { style: { flex:'1', display:'flex', flexDirection:'column', maxWidth:'900px', margin:'0 auto', width:'100%', padding:'0 16px' }}, landing, chatArea, inputArea);

  const app = el('div', { style: { minHeight:'100vh', background:'#f5f5f5', display:'flex', flexDirection:'column' }}, header, controls, main);
  document.getElementById('app').appendChild(app);

  async function sendMsg(text) {
    const userText = text || textarea.value.trim();
    if (!userText) return;
    textarea.value = '';

    if (!started) {
      started = true;
      landing.style.display = 'none';
      chatArea.style.display = 'block';
    }

    // User message
    chatArea.appendChild(
      el('div', { style: { marginBottom:'20px', display:'flex', gap:'12px', justifyContent:'flex-end' }},
        el('div', { style: { maxWidth:'82%', background:'#111', color:'#fff', borderRadius:'16px 16px 4px 16px', padding:'14px 18px', fontSize:'0.88rem', lineHeight:'1.8', whiteSpace:'pre-wrap' }}, userText),
        el('div', { style: { width:'36px', height:'36px', background:'#333', borderRadius:'8px', display:'flex', alignItems:'center', justifyContent:'center', fontSize:'0.75rem', color:'#fff', fontWeight:'700', flexShrink:'0', marginTop:'2px', lineHeight:'36px', textAlign:'center' }}, 'YOU')
      )
    );

    // Loading
    const loadingDots = el('div', { style: { display:'flex', gap:'6px', alignItems:'center' }},
      ...[0,1,2].map(i => {
        const d = el('div', { style: { width:'7px', height:'7px', background:'#e8a020', borderRadius:'50%', animation:'bounce 1.2s infinite', animationDelay:`${i*0.2}s` }});
        return d;
      }),
      el('span', { style: { fontSize:'0.78rem', color:'#888', marginLeft:'6px' }}, 'Preparing your recipe...')
    );
    const loadingMsg = el('div', { style: { display:'flex', gap:'12px', marginBottom:'20px' }},
      el('div', { style: { width:'36px', height:'36px', background:'#e8a020', borderRadius:'8px', display:'flex', alignItems:'center', justifyContent:'center', fontSize:'1rem', flexShrink:'0', lineHeight:'36px', textAlign:'center' }}, '🍳'),
      el('div', { style: { background:'#fff', border:'1px solid #e0e0e0', borderRadius:'16px 16px 16px 4px', padding:'14px 20px', display:'flex', gap:'6px', alignItems:'center' }}, loadingDots)
    );
    chatArea.appendChild(loadingMsg);
    chatArea.scrollTop = chatArea.scrollHeight;

    let prompt = userText + `\n\nCooking for: ${servings} people. Scale ALL ingredients for exactly ${servings} people.`;
    if (diet !== 'None') prompt += `\nDiet: ${diet}.`;
    if (cuisine !== 'All') prompt += `\nCuisine: ${cuisine}.`;

    messages.push({ role: 'user', content: prompt });

    try {
      const res = await fetch('https://api.anthropic.com/v1/messages', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'x-api-key': apiKey,
          'anthropic-version': '2023-06-01',
          'anthropic-dangerous-direct-browser-access': 'true'
        },
        body: JSON.stringify({
          model: 'claude-haiku-4-5-20251001',
          max_tokens: 2000,
          system: SYSTEM,
          messages: messages
        })
      });
      const data = await res.json();
      const reply = data.content?.[0]?.text || 'Sorry, something went wrong.';
      messages.push({ role: 'assistant', content: reply });
      chatArea.removeChild(loadingMsg);
      chatArea.appendChild(
        el('div', { style: { marginBottom:'20px', display:'flex', gap:'12px' }},
          el('div', { style: { width:'36px', height:'36px', background:'#e8a020', borderRadius:'8px', display:'flex', alignItems:'center', justifyContent:'center', fontSize:'1rem', flexShrink:'0', marginTop:'2px', lineHeight:'36px', textAlign:'center' }}, '🍳'),
          el('div', { style: { maxWidth:'82%', background:'#fff', color:'#111', borderRadius:'16px 16px 16px 4px', padding:'14px 18px', fontSize:'0.88rem', lineHeight:'1.8', border:'1px solid #e0e0e0', whiteSpace:'pre-wrap' }}, reply)
        )
      );
    } catch(e) {
      chatArea.removeChild(loadingMsg);
      chatArea.appendChild(
        el('div', { style: { marginBottom:'20px', display:'flex', gap:'12px' }},
          el('div', { style: { width:'36px', height:'36px', background:'#e8a020', borderRadius:'8px', lineHeight:'36px', textAlign:'center' }}, '🍳'),
          el('div', { style: { background:'#fff', border:'1px solid #e0e0e0', borderRadius:'16px 16px 16px 4px', padding:'14px 18px', fontSize:'0.88rem', color:'#cc0000' }}, 'Connection error. Please check your API key and try again.')
        )
      );
    }
    chatArea.scrollTop = chatArea.scrollHeight;
  }

  sendBtn.addEventListener('click', () => sendMsg());
}

// INIT
const saved = localStorage.getItem('cm_key');
if (saved) { apiKey = saved; showMainApp(); }
else { showApiScreen(); }
</script>
</body>
</html>

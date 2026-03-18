<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Simulation — Second tour Municipales Paris 2026</title>
<meta name="description" content="Modèle de transfert de voix par graphe stochastique — Municipales Paris 2026" />
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700;800&family=JetBrains+Mono:wght@400;500;600;700;800&display=swap" rel="stylesheet" />
<script src="https://cdnjs.cloudflare.com/ajax/libs/react/18.2.0/umd/react.production.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/react-dom/18.2.0/umd/react-dom.production.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/7.23.9/babel.min.js"></script>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { font-family: 'DM Sans', sans-serif; }
  input[type=range] { -webkit-appearance: none; appearance: none; height: 22px; background: transparent; cursor: pointer; width: 100%; margin-top: -4px; }
  input[type=range]::-webkit-slider-thumb { -webkit-appearance: none; appearance: none; width: 16px; height: 16px; border-radius: 50%; background: #1e293b; border: 2px solid white; box-shadow: 0 1px 4px rgba(0,0,0,0.25); cursor: pointer; margin-top: -5px; }
  input[type=range]::-moz-range-thumb { width: 14px; height: 14px; border-radius: 50%; background: #1e293b; border: 2px solid white; box-shadow: 0 1px 4px rgba(0,0,0,0.25); cursor: pointer; }
  input[type=range]::-webkit-slider-runnable-track { height: 0; }
  input[type=range]::-moz-range-track { height: 0; }
</style>
</head>
<body>
<div id="root"></div>
<script type="text/babel">
const { useState, useMemo } = React;

const FIRST_ROUND = {
  gregoire: 309693, dati: 207613, bournazel: 92448, chikirou: 95551,
  knafo: 84809, mariani: 13096, deg: 5991 + 5544,
};
const TOTAL_VOTES = Object.values(FIRST_ROUND).reduce((a, b) => a + b, 0);
const CANDIDATE_COLORS = { gregoire: "#e8436e", dati: "#3b82f6", chikirou: "#c2185b", abstention: "#94a3b8" };
const CANDIDATE_LABELS = { gregoire: "Grégoire", dati: "Dati", chikirou: "Chikirou" };
const CANDIDATE_SUBTITLES = { gregoire: "PS – Gauche", dati: "LR – Droite (+ Bournazel)", chikirou: "LFI – Gauche rad." };
const QUALIFIED = ["gregoire", "dati", "chikirou"];

const DEFAULT_PARAMS = {
  ret_gregoire: 0.90, ret_dati: 0.88,
  bournazel_gregoire: 0.25, bournazel_dati: 0.55,
  chikirou_gregoire: 0.20, ret_chikirou: 0.60,
  ret_knafo: 0.70, ret_mariani: 0.55, ret_deg: 0.75,
};

function computeResults(params) {
  const { ret_gregoire, ret_dati, bournazel_gregoire, bournazel_dati, chikirou_gregoire, ret_chikirou, ret_knafo, ret_mariani, ret_deg } = params;
  const bournazel_abs = Math.max(0, 1 - bournazel_gregoire - bournazel_dati);
  const chikirou_abs = Math.max(0, 1 - chikirou_gregoire - ret_chikirou);
  const r = { gregoire: 0, dati: 0, chikirou: 0, abstention: 0 };
  r.gregoire += FIRST_ROUND.gregoire * ret_gregoire;
  r.abstention += FIRST_ROUND.gregoire * (1 - ret_gregoire);
  r.dati += FIRST_ROUND.dati * ret_dati;
  r.abstention += FIRST_ROUND.dati * (1 - ret_dati);
  r.gregoire += FIRST_ROUND.bournazel * bournazel_gregoire;
  r.dati += FIRST_ROUND.bournazel * bournazel_dati;
  r.abstention += FIRST_ROUND.bournazel * bournazel_abs;
  r.gregoire += FIRST_ROUND.chikirou * chikirou_gregoire;
  r.chikirou += FIRST_ROUND.chikirou * ret_chikirou;
  r.abstention += FIRST_ROUND.chikirou * chikirou_abs;
  r.dati += FIRST_ROUND.knafo * ret_knafo;
  r.abstention += FIRST_ROUND.knafo * (1 - ret_knafo);
  r.dati += FIRST_ROUND.mariani * ret_mariani;
  r.abstention += FIRST_ROUND.mariani * (1 - ret_mariani);
  r.chikirou += FIRST_ROUND.deg * ret_deg;
  r.abstention += FIRST_ROUND.deg * (1 - ret_deg);
  return r;
}

function Slider({ label, sublabel, value, onChange, min=0, max=1, step=0.01, color="#e8436e", warn }) {
  const pct = ((value - min) / (max - min)) * 100;
  return (
    <div style={{ marginBottom: 14 }}>
      <div style={{ display: "flex", justifyContent: "space-between", alignItems: "baseline", marginBottom: 3 }}>
        <span style={{ fontSize: 13, fontWeight: 600, color: "#1e293b" }}>
          {label}{sublabel && <span style={{ fontWeight: 400, color: "#64748b", marginLeft: 6, fontSize: 11 }}>{sublabel}</span>}
        </span>
        <span style={{ fontFamily: "'JetBrains Mono', monospace", fontSize: 13, fontWeight: 700, color: warn ? "#dc2626" : color, minWidth: 48, textAlign: "right" }}>
          {(value * 100).toFixed(0)}%
        </span>
      </div>
      <div style={{ position: "relative", height: 6, borderRadius: 3, background: "#e2e8f0" }}>
        <div style={{ position: "absolute", left: 0, top: 0, height: "100%", width: `${pct}%`, borderRadius: 3, background: warn ? "#dc2626" : color, transition: "width 0.1s" }} />
      </div>
      <input type="range" min={min} max={max} step={step} value={value} onChange={(e) => onChange(parseFloat(e.target.value))} />
    </div>
  );
}

function ResultBar({ name, subtitle, votes, totalExpressed, maxVotes, color, isWinner }) {
  const pct = totalExpressed > 0 ? (votes / totalExpressed) * 100 : 0;
  const barWidth = maxVotes > 0 ? (votes / maxVotes) * 100 : 0;
  return (
    <div style={{ marginBottom: 16 }}>
      <div style={{ display: "flex", justifyContent: "space-between", alignItems: "baseline", marginBottom: 5 }}>
        <div style={{ display: "flex", alignItems: "center", gap: 8 }}>
          {isWinner && <span style={{ fontSize: 14 }}>👑</span>}
          <span style={{ fontSize: 15, fontWeight: 700, color: "#0f172a" }}>{name}</span>
          <span style={{ fontSize: 11, color: "#64748b", fontWeight: 500 }}>{subtitle}</span>
        </div>
        <div style={{ textAlign: "right" }}>
          <span style={{ fontFamily: "'JetBrains Mono', monospace", fontSize: 18, fontWeight: 800, color }}>{pct.toFixed(1)}%</span>
          <span style={{ fontFamily: "'JetBrains Mono', monospace", fontSize: 11, color: "#94a3b8", marginLeft: 8 }}>{Math.round(votes).toLocaleString("fr-FR")}</span>
        </div>
      </div>
      <div style={{ position: "relative", height: 28, borderRadius: 6, background: "#f1f5f9", overflow: "hidden" }}>
        <div style={{ height: "100%", width: `${barWidth}%`, borderRadius: 6, background: `linear-gradient(90deg, ${color}, ${color}dd)`, transition: "width 0.3s cubic-bezier(0.4,0,0.2,1)", boxShadow: isWinner ? `0 2px 12px ${color}55` : "none" }} />
      </div>
    </div>
  );
}

function SankeyMini({ params }) {
  const sources = [
    { key: "gregoire", label: "Grégoire", votes: FIRST_ROUND.gregoire, color: CANDIDATE_COLORS.gregoire },
    { key: "dati", label: "Dati", votes: FIRST_ROUND.dati, color: CANDIDATE_COLORS.dati },
    { key: "bournazel", label: "Bournazel", votes: FIRST_ROUND.bournazel, color: "#6d9eeb" },
    { key: "chikirou", label: "Chikirou", votes: FIRST_ROUND.chikirou, color: CANDIDATE_COLORS.chikirou },
    { key: "knafo", label: "Knafo", votes: FIRST_ROUND.knafo, color: "#f59e0b" },
    { key: "mariani", label: "Mariani", votes: FIRST_ROUND.mariani, color: "#1e3a5f" },
    { key: "deg", label: "DEG", votes: FIRST_ROUND.deg, color: "#9333ea" },
  ];
  const bAbs = Math.max(0, 1 - params.bournazel_gregoire - params.bournazel_dati);
  const cAbs = Math.max(0, 1 - params.chikirou_gregoire - params.ret_chikirou);
  const flows = {
    gregoire: { gregoire: params.ret_gregoire, abstention: 1 - params.ret_gregoire },
    dati: { dati: params.ret_dati, abstention: 1 - params.ret_dati },
    bournazel: { gregoire: params.bournazel_gregoire, dati: params.bournazel_dati, abstention: bAbs },
    chikirou: { gregoire: params.chikirou_gregoire, chikirou: params.ret_chikirou, abstention: cAbs },
    knafo: { dati: params.ret_knafo, abstention: 1 - params.ret_knafo },
    mariani: { dati: params.ret_mariani, abstention: 1 - params.ret_mariani },
    deg: { chikirou: params.ret_deg, abstention: 1 - params.ret_deg },
  };
  const destinations = ["gregoire", "dati", "chikirou", "abstention"];
  const destColors = { ...CANDIDATE_COLORS };
  const W = 700, H = 300, srcX = 60, dstX = W - 60, usableH = H - 40, srcGap = 4;
  const srcTotalVotes = sources.reduce((a, s) => a + s.votes, 0);
  const srcScale = (usableH - srcGap * (sources.length - 1)) / srcTotalVotes;
  let sY = 20;
  const srcPos = sources.map((s) => { const h = Math.max(2, s.votes * srcScale); const p = { ...s, y: sY, h }; sY += h + srcGap; return p; });
  const destTotals = {}; destinations.forEach((d) => { destTotals[d] = 0; });
  sources.forEach((s) => { Object.entries(flows[s.key] || {}).forEach(([dest, ratio]) => { destTotals[dest] = (destTotals[dest] || 0) + s.votes * ratio; }); });
  const totalDst = destinations.reduce((a, d) => a + destTotals[d], 0);
  const dstGap = 5, dstScale = (usableH - dstGap * (destinations.length - 1)) / totalDst;
  let dY = 20; const dstPos = {};
  destinations.forEach((d) => { const h = Math.max(2, destTotals[d] * dstScale); dstPos[d] = { y: dY, h, filled: 0 }; dY += h + dstGap; });
  const paths = [];
  srcPos.forEach((src) => { let sf = 0; Object.entries(flows[src.key] || {}).forEach(([dest, ratio]) => {
    if (ratio <= 0) return; const fhs = src.h * ratio; const fhd = dstPos[dest].h * ((src.votes * ratio) / destTotals[dest]);
    const y1 = src.y + sf, y2 = dstPos[dest].y + dstPos[dest].filled, cp = (dstX - srcX) * 0.45;
    paths.push({ d: `M${srcX},${y1} C${srcX+cp},${y1} ${dstX-cp},${y2} ${dstX},${y2} L${dstX},${y2+fhd} C${dstX-cp},${y2+fhd} ${srcX+cp},${y1+fhs} ${srcX},${y1+fhs} Z`,
      color: destColors[dest] || "#94a3b8", opacity: dest === "abstention" ? 0.15 : 0.35 });
    sf += fhs; dstPos[dest].filled += fhd; }); });
  const dl = { gregoire: "Grégoire", dati: "Dati", chikirou: "Chikirou", abstention: "Abstention" };
  return (
    <svg viewBox={`0 0 ${W} ${H}`} style={{ width: "100%", maxWidth: 700 }}>
      {paths.map((p, i) => <path key={i} d={p.d} fill={p.color} opacity={p.opacity} />)}
      {srcPos.map((s, i) => <g key={`s${i}`}><rect x={srcX-6} y={s.y} width={6} height={s.h} rx={2} fill={s.color}/><text x={srcX-12} y={s.y+s.h/2} textAnchor="end" dominantBaseline="central" style={{fontSize:10,fontFamily:"'DM Sans',sans-serif",fontWeight:600,fill:"#475569"}}>{s.label}</text></g>)}
      {destinations.map((d) => <g key={`d${d}`}><rect x={dstX} y={dstPos[d].y} width={6} height={dstPos[d].h} rx={2} fill={destColors[d]}/><text x={dstX+14} y={dstPos[d].y+dstPos[d].h/2} textAnchor="start" dominantBaseline="central" style={{fontSize:10,fontFamily:"'DM Sans',sans-serif",fontWeight:600,fill:"#475569"}}>{dl[d]}</text></g>)}
    </svg>
  );
}

function App() {
  const [params, setParams] = useState(DEFAULT_PARAMS);
  const setParam = (key, val) => setParams((p) => ({ ...p, [key]: val }));
  const results = useMemo(() => computeResults(params), [params]);
  const totalExpressed = QUALIFIED.reduce((a, c) => a + results[c], 0);
  const maxVotes = Math.max(...QUALIFIED.map((c) => results[c]));
  const winner = QUALIFIED.reduce((a, b) => (results[a] > results[b] ? a : b));
  const bournAbs = Math.max(0, 1 - params.bournazel_gregoire - params.bournazel_dati);
  const bournWarn = bournAbs < 0.001;
  const chikAbs = Math.max(0, 1 - params.chikirou_gregoire - params.ret_chikirou);
  const chikWarn = chikAbs < 0.001;
  const abstRate = ((results.abstention / TOTAL_VOTES) * 100).toFixed(1);

  return (
    <div style={{ fontFamily: "'DM Sans', sans-serif", minHeight: "100vh", background: "linear-gradient(135deg, #f8fafc 0%, #eef2f7 100%)", padding: "24px 16px" }}>
      <div style={{ maxWidth: 880, margin: "0 auto" }}>
        <div style={{ textAlign: "center", marginBottom: 28 }}>
          <div style={{ fontSize: 11, fontWeight: 700, letterSpacing: "0.15em", textTransform: "uppercase", color: "#94a3b8", marginBottom: 4 }}>Simulation · Second tour</div>
          <h1 style={{ fontSize: 26, fontWeight: 800, color: "#0f172a", margin: 0, letterSpacing: "-0.03em", lineHeight: 1.1 }}>Municipales Paris 2026</h1>
          <div style={{ fontSize: 12, color: "#64748b", marginTop: 6 }}>Modèle de transfert de voix · 3 qualifiés · Bournazel fusionné avec Dati · 9 paramètres</div>
        </div>

        <div style={{ background: "white", borderRadius: 16, padding: "24px 28px", boxShadow: "0 1px 3px rgba(0,0,0,0.06), 0 8px 24px rgba(0,0,0,0.04)", marginBottom: 20, border: "1px solid #e2e8f0" }}>
          <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 18 }}>
            <h2 style={{ fontSize: 14, fontWeight: 700, color: "#0f172a", margin: 0 }}>Résultats du second tour</h2>
            <div style={{ fontSize: 11, fontWeight: 600, padding: "4px 10px", borderRadius: 20, background: "#f1f5f9", color: "#64748b" }}>
              Exprimés : {Math.round(totalExpressed).toLocaleString("fr-FR")} · Abst./blanc : {abstRate}%
            </div>
          </div>
          {QUALIFIED.sort((a, b) => results[b] - results[a]).map((c) => (
            <ResultBar key={c} name={CANDIDATE_LABELS[c]} subtitle={CANDIDATE_SUBTITLES[c]} votes={results[c]} totalExpressed={totalExpressed} maxVotes={maxVotes} color={CANDIDATE_COLORS[c]} isWinner={c === winner} />
          ))}
        </div>

        <div style={{ background: "white", borderRadius: 16, padding: "20px 24px", boxShadow: "0 1px 3px rgba(0,0,0,0.06), 0 8px 24px rgba(0,0,0,0.04)", marginBottom: 20, border: "1px solid #e2e8f0" }}>
          <h2 style={{ fontSize: 14, fontWeight: 700, color: "#0f172a", margin: "0 0 8px 0" }}>Flux de transfert de voix</h2>
          <div style={{ fontSize: 11, color: "#94a3b8", marginBottom: 8 }}>Tour 1 → Tour 2 · Bournazel redistribué (fusion Dati)</div>
          <SankeyMini params={params} />
        </div>

        <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 16 }}>
          <div style={{ background: "white", borderRadius: 16, padding: "20px 24px", boxShadow: "0 1px 3px rgba(0,0,0,0.06), 0 8px 24px rgba(0,0,0,0.04)", border: "1px solid #e2e8f0" }}>
            <h3 style={{ fontSize: 12, fontWeight: 700, color: "#64748b", margin: "0 0 14px 0", textTransform: "uppercase", letterSpacing: "0.08em" }}>Rétention – Qualifiés</h3>
            <Slider label="Grégoire → Grégoire" value={params.ret_gregoire} onChange={(v) => setParam("ret_gregoire", v)} color={CANDIDATE_COLORS.gregoire} />
            <Slider label="Dati → Dati" value={params.ret_dati} onChange={(v) => setParam("ret_dati", v)} color={CANDIDATE_COLORS.dati} />
            <div style={{ borderTop: "1px solid #e2e8f0", margin: "10px 0 14px" }} />
            <div style={{ fontSize: 11, fontWeight: 600, color: "#94a3b8", marginBottom: 8 }}>BOURNAZEL — fusionné, 2 destinations <span style={{ marginLeft: 6, fontSize: 9, padding: "1px 6px", background: "#dbeafe", color: "#3b82f6", borderRadius: 8, fontWeight: 700 }}>fusion Dati</span></div>
            <Slider label="→ Grégoire" value={params.bournazel_gregoire} onChange={(v) => setParam("bournazel_gregoire", v)} color={CANDIDATE_COLORS.gregoire} />
            <Slider label="→ Dati" value={params.bournazel_dati} onChange={(v) => setParam("bournazel_dati", v)} color={CANDIDATE_COLORS.dati} />
            <div style={{ fontSize: 11, color: bournWarn ? "#dc2626" : "#94a3b8", fontWeight: 500 }}>→ Abstention implicite : {(bournAbs * 100).toFixed(0)}% {bournWarn && "⚠ nul !"}</div>
            <div style={{ borderTop: "1px solid #e2e8f0", margin: "14px 0" }} />
            <div style={{ fontSize: 11, fontWeight: 600, color: "#94a3b8", marginBottom: 8 }}>CHIKIROU — 2 destinations</div>
            <Slider label="→ Grégoire" value={params.chikirou_gregoire} onChange={(v) => setParam("chikirou_gregoire", v)} color={CANDIDATE_COLORS.gregoire} />
            <Slider label="→ Chikirou" value={params.ret_chikirou} onChange={(v) => setParam("ret_chikirou", v)} color={CANDIDATE_COLORS.chikirou} />
            <div style={{ fontSize: 11, color: chikWarn ? "#dc2626" : "#94a3b8", fontWeight: 500 }}>→ Abstention implicite : {(chikAbs * 100).toFixed(0)}% {chikWarn && "⚠ nul !"}</div>
          </div>

          <div style={{ background: "white", borderRadius: 16, padding: "20px 24px", boxShadow: "0 1px 3px rgba(0,0,0,0.06), 0 8px 24px rgba(0,0,0,0.04)", border: "1px solid #e2e8f0" }}>
            <h3 style={{ fontSize: 12, fontWeight: 700, color: "#64748b", margin: "0 0 14px 0", textTransform: "uppercase", letterSpacing: "0.08em" }}>Report – Non qualifiés</h3>
            <Slider label="Knafo → Dati" sublabel="(reste → abst.)" value={params.ret_knafo} onChange={(v) => setParam("ret_knafo", v)} color={CANDIDATE_COLORS.dati} />
            <Slider label="Mariani → Dati" sublabel="(reste → abst.)" value={params.ret_mariani} onChange={(v) => setParam("ret_mariani", v)} color={CANDIDATE_COLORS.dati} />
            <Slider label="DEG → Chikirou" sublabel="(reste → abst.)" value={params.ret_deg} onChange={(v) => setParam("ret_deg", v)} color={CANDIDATE_COLORS.chikirou} />
            <div style={{ borderTop: "1px solid #e2e8f0", marginTop: 18, paddingTop: 16 }}>
              <h3 style={{ fontSize: 12, fontWeight: 700, color: "#64748b", margin: "0 0 12px 0", textTransform: "uppercase", letterSpacing: "0.08em" }}>Matrice de transfert</h3>
              <table style={{ width: "100%", fontSize: 12, borderCollapse: "collapse", fontFamily: "'JetBrains Mono', monospace" }}>
                <thead><tr style={{ borderBottom: "2px solid #e2e8f0" }}>
                  <th style={{ textAlign: "left", padding: "6px 4px", fontWeight: 700, color: "#475569", fontFamily: "'DM Sans', sans-serif" }}>Source</th>
                  <th style={{ textAlign: "right", padding: "6px 4px", fontWeight: 600, color: CANDIDATE_COLORS.gregoire, fontSize: 10 }}>GRÉ</th>
                  <th style={{ textAlign: "right", padding: "6px 4px", fontWeight: 600, color: CANDIDATE_COLORS.dati, fontSize: 10 }}>DAT</th>
                  <th style={{ textAlign: "right", padding: "6px 4px", fontWeight: 600, color: CANDIDATE_COLORS.chikirou, fontSize: 10 }}>CHI</th>
                  <th style={{ textAlign: "right", padding: "6px 4px", fontWeight: 600, color: "#94a3b8", fontSize: 10 }}>ABS</th>
                </tr></thead>
                <tbody>
                  {[
                    { name: "Grégoire", vals: [params.ret_gregoire, 0, 0, 1 - params.ret_gregoire] },
                    { name: "Dati", vals: [0, params.ret_dati, 0, 1 - params.ret_dati] },
                    { name: "Bournazel", vals: [params.bournazel_gregoire, params.bournazel_dati, 0, bournAbs] },
                    { name: "Chikirou", vals: [params.chikirou_gregoire, 0, params.ret_chikirou, chikAbs] },
                    { name: "Knafo", vals: [0, params.ret_knafo, 0, 1 - params.ret_knafo] },
                    { name: "Mariani", vals: [0, params.ret_mariani, 0, 1 - params.ret_mariani] },
                    { name: "DEG", vals: [0, 0, params.ret_deg, 1 - params.ret_deg] },
                  ].map((row) => (
                    <tr key={row.name} style={{ borderBottom: "1px solid #f1f5f9" }}>
                      <td style={{ padding: "5px 4px", fontWeight: 600, fontFamily: "'DM Sans', sans-serif", color: "#334155" }}>{row.name}</td>
                      {row.vals.map((v, i) => (
                        <td key={i} style={{ padding: "5px 4px", textAlign: "right", fontSize: 11, color: v === 0 ? "#cbd5e1" : v > 0.5 ? "#0f172a" : "#64748b", fontWeight: v > 0.5 ? 700 : 400 }}>
                          {v === 0 ? "·" : (v * 100).toFixed(0) + "%"}
                        </td>
                      ))}
                    </tr>
                  ))}
                </tbody>
              </table>
            </div>
          </div>
        </div>
        <div style={{ textAlign: "center", marginTop: 16, fontSize: 10, color: "#94a3b8" }}>Modèle simplifié — ne constitue pas une prédiction électorale</div>
      </div>
    </div>
  );
}

ReactDOM.createRoot(document.getElementById("root")).render(<App />);
</script>
</body>
</html>

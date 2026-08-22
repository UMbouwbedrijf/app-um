<!DOCTYPE html>
<html lang="nl">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>UM Bouwbedrijf</title>
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
<script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
<style>
  body { background:#1C2321; margin:0; }
  ::-webkit-scrollbar { width: 8px; }
</style>
</head>
<body>
<div id="root"></div>
<script>
(() => {
  // extracted.jsx
  var { useState, useEffect, useRef, useCallback } = React;
  var SUPABASE_URL = "https://wsostlssqzenbppvzsxt.supabase.co";
  var SUPABASE_ANON_KEY = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Indzb3N0bHNzcXplbmJwcHZ6c3h0Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3ODcyNDgxOTcsImV4cCI6MjEwMjgyNDE5N30.qCv4GS9DhBsue12Tny36lm7QzJT_-G2wJlZckdLo8EY";
  var NAV = [
    { key: "dashboard", label: "Overzicht", icon: "\u25A6" },
    { key: "customers", label: "Klanten", icon: "\u{1F465}" },
    { key: "quotations", label: "Offertes", icon: "\u{1F4C4}" },
    { key: "pricelist", label: "Prijslijst", icon: "\u{1F4CB}" },
    { key: "projects", label: "Projecten", icon: "\u{1F3D7}\uFE0F" }
  ];
  var STATUS_STYLES = {
    concept: "text-stone-500 border-stone-400",
    verzonden: "text-[#2B4C7E] border-[#2B4C7E]",
    geaccepteerd: "text-[#4A7C59] border-[#4A7C59]",
    afgewezen: "text-[#B3441E] border-[#B3441E]",
    lopend: "text-[#2B4C7E] border-[#2B4C7E]",
    afgerond: "text-[#4A7C59] border-[#4A7C59]"
  };
  function euro(n) {
    const v = Number(n) || 0;
    return v.toLocaleString("nl-NL", { style: "currency", currency: "EUR" });
  }
  function uid() {
    return Date.now().toString(36) + Math.random().toString(36).slice(2, 7);
  }
  function quoteSubtotal(q) {
    return q.items.reduce((s, it) => s + it.qty * it.price, 0);
  }
  function quoteTotal(q) {
    var _a;
    const sub = quoteSubtotal(q);
    return sub * (1 + Number((_a = q.btw_percent) != null ? _a : 21) / 100);
  }
  function Stamp({ status, children }) {
    const cls = STATUS_STYLES[status] || "text-stone-500 border-stone-400";
    return /* @__PURE__ */ React.createElement("span", { className: `inline-block select-none border-2 rounded px-2 py-0.5 text-[10px] font-black uppercase tracking-[0.12em] -rotate-2 ${cls}` }, children);
  }
  function resizeImage(file, maxW = 900, quality = 0.6) {
    return new Promise((resolve, reject) => {
      const reader = new FileReader();
      reader.onload = (e) => {
        const img = new Image();
        img.onload = () => {
          const scale = Math.min(1, maxW / img.width);
          const canvas = document.createElement("canvas");
          canvas.width = img.width * scale;
          canvas.height = img.height * scale;
          const ctx = canvas.getContext("2d");
          ctx.drawImage(img, 0, 0, canvas.width, canvas.height);
          resolve(canvas.toDataURL("image/jpeg", quality));
        };
        img.onerror = reject;
        img.src = e.target.result;
      };
      reader.onerror = reject;
      reader.readAsDataURL(file);
    });
  }
  async function authRequest(path, body) {
    const res = await fetch(`${SUPABASE_URL}/auth/v1/${path}`, {
      method: "POST",
      headers: { "Content-Type": "application/json", apikey: SUPABASE_ANON_KEY },
      body: JSON.stringify(body)
    });
    const data = await res.json().catch(() => ({}));
    if (!res.ok) {
      throw new Error(data.error_description || data.msg || data.error || "Er ging iets mis.");
    }
    return data;
  }
  function sessionFromAuthData(data) {
    return {
      access_token: data.access_token,
      refresh_token: data.refresh_token,
      expires_at: Date.now() + (data.expires_in || 3600) * 1e3 - 3e4,
      user: data.user
    };
  }
  async function refreshSession(session) {
    const data = await authRequest("token?grant_type=refresh_token", { refresh_token: session.refresh_token });
    return sessionFromAuthData(data);
  }
  async function db(path, { method = "GET", token, body, prefer } = {}) {
    const headers = {
      "Content-Type": "application/json",
      apikey: SUPABASE_ANON_KEY,
      Authorization: `Bearer ${token}`
    };
    if (prefer) headers["Prefer"] = prefer;
    const res = await fetch(`${SUPABASE_URL}/rest/v1/${path}`, {
      method,
      headers,
      body: body !== void 0 ? JSON.stringify(body) : void 0
    });
    if (!res.ok) {
      const err = await res.json().catch(() => ({}));
      throw new Error(err.message || `Serverfout (${res.status})`);
    }
    if (res.status === 204) return null;
    const text = await res.text();
    return text ? JSON.parse(text) : null;
  }
  function App() {
    const [session, setSession] = useState(null);
    const [view, setView] = useState("dashboard");
    const [data, setData] = useState({ customers: [], price_list: [], quotations: [], projects: [] });
    const [loaded, setLoaded] = useState(false);
    const [globalError, setGlobalError] = useState("");
    const getToken = useCallback(async () => {
      if (!session) throw new Error("Niet ingelogd.");
      if (Date.now() < session.expires_at) return session.access_token;
      const fresh = await refreshSession(session);
      setSession(fresh);
      return fresh.access_token;
    }, [session]);
    const call = useCallback(async (fn) => {
      try {
        const token = await getToken();
        return await fn(token);
      } catch (e) {
        const msg = String(e.message || "");
        if (msg.toLowerCase().includes("token") || msg.includes("401") || msg.toLowerCase().includes("jwt") || msg.toLowerCase().includes("ingelogd")) {
          setSession(null);
          setGlobalError("Je sessie is verlopen. Log opnieuw in.");
        } else {
          setGlobalError(msg);
        }
        throw e;
      }
    }, [getToken]);
    const loadAll = useCallback(async () => {
      setLoaded(false);
      try {
        await call(async (token) => {
          const [customers, price_list, quotations, projects] = await Promise.all([
            db("customers?select=*&order=name.asc", { token }),
            db("price_list?select=*&order=name.asc", { token }),
            db("quotations?select=*&order=date.desc", { token }),
            db("projects?select=*&order=created_at.desc", { token })
          ]);
          setData({ customers, price_list, quotations, projects });
        });
      } catch (e) {
        console.error(e);
      }
      setLoaded(true);
    }, [call]);
    useEffect(() => {
      if (session) loadAll();
    }, [session]);
    if (!session) {
      return /* @__PURE__ */ React.createElement(AuthScreen, { onAuthed: setSession });
    }
    const stats = {
      customers: data.customers.length,
      openQuotes: data.quotations.filter((q) => q.status !== "geaccepteerd" && q.status !== "afgewezen").length,
      quoteValue: data.quotations.filter((q) => q.status === "verzonden" || q.status === "geaccepteerd").reduce((sum, q) => sum + quoteTotal(q), 0),
      activeProjects: data.projects.filter((p) => p.status !== "afgerond").length
    };
    const logout = async () => {
      try {
        await fetch(`${SUPABASE_URL}/auth/v1/logout`, { method: "POST", headers: { apikey: SUPABASE_ANON_KEY, Authorization: `Bearer ${session.access_token}` } });
      } catch (e) {
      }
      setSession(null);
    };
    return /* @__PURE__ */ React.createElement("div", { className: "min-h-screen bg-[#1C2321] flex flex-col font-sans" }, /* @__PURE__ */ React.createElement(Header, { onLogout: logout, view, setView }), globalError && /* @__PURE__ */ React.createElement("div", { className: "bg-[#B3441E] text-white text-xs px-4 py-2 flex items-center justify-between" }, /* @__PURE__ */ React.createElement("span", null, "\u26A0\uFE0F ", globalError), /* @__PURE__ */ React.createElement("button", { onClick: () => setGlobalError("") }, "\u2715")), /* @__PURE__ */ React.createElement("main", { className: "flex-1 overflow-y-auto pb-24 md:pb-8" }, !loaded ? /* @__PURE__ */ React.createElement(CenterShell, null, /* @__PURE__ */ React.createElement("p", { className: "text-stone-400 text-sm" }, "Laden\u2026")) : view === "dashboard" ? /* @__PURE__ */ React.createElement(Dashboard, { stats, customers: data.customers, quotations: data.quotations, setView }) : view === "customers" ? /* @__PURE__ */ React.createElement(CustomersView, { customers: data.customers, call, onChange: loadAll }) : view === "pricelist" ? /* @__PURE__ */ React.createElement(PriceListView, { priceList: data.price_list, call, onChange: loadAll }) : view === "quotations" ? /* @__PURE__ */ React.createElement(QuotationsView, { quotations: data.quotations, customers: data.customers, priceList: data.price_list, call, onChange: loadAll }) : view === "projects" ? /* @__PURE__ */ React.createElement(ProjectsView, { projects: data.projects, customers: data.customers, call, onChange: loadAll }) : null), /* @__PURE__ */ React.createElement(BottomNav, { view, setView }));
  }
  function CenterShell({ children }) {
    return /* @__PURE__ */ React.createElement("div", { className: "min-h-screen bg-[#1C2321] flex items-center justify-center" }, children);
  }
  function AuthScreen({ onAuthed }) {
    const [mode, setMode] = useState("login");
    const [email, setEmail] = useState("");
    const [pw, setPw] = useState("");
    const [error, setError] = useState("");
    const [busy, setBusy] = useState(false);
    const submit = async (e) => {
      e.preventDefault();
      setError("");
      setBusy(true);
      try {
        const result = mode === "signup" ? await authRequest("signup", { email: email.trim(), password: pw }) : await authRequest("token?grant_type=password", { email: email.trim(), password: pw });
        if (!result.access_token) {
          setError("Account aangemaakt. Controleer of e-mailbevestiging uitstaat in Supabase, of log nu in.");
          setMode("login");
        } else {
          onAuthed(sessionFromAuthData(result));
        }
      } catch (err) {
        setError(err.message);
      } finally {
        setBusy(false);
      }
    };
    return /* @__PURE__ */ React.createElement("div", { className: "min-h-screen bg-[#1C2321] overflow-y-auto p-6 relative" }, /* @__PURE__ */ React.createElement("div", { className: "fixed inset-0 opacity-[0.04] pointer-events-none", style: {
      backgroundImage: "repeating-linear-gradient(0deg, #F5F3EE 0, #F5F3EE 1px, transparent 1px, transparent 40px), repeating-linear-gradient(90deg, #F5F3EE 0, #F5F3EE 1px, transparent 1px, transparent 40px)"
    } }), /* @__PURE__ */ React.createElement("div", { className: "relative w-full max-w-sm mx-auto py-10" }, /* @__PURE__ */ React.createElement("div", { className: "text-center mb-8" }, /* @__PURE__ */ React.createElement("div", { className: "inline-flex items-center justify-center w-14 h-14 rounded-full bg-[#E8590C] mb-4 text-2xl" }, "\u{1F3D7}\uFE0F"), /* @__PURE__ */ React.createElement("h1", { className: "text-2xl font-black tracking-tight text-[#F5F3EE] uppercase" }, "UM Bouwbedrijf"), /* @__PURE__ */ React.createElement("p", { className: "text-stone-400 text-sm mt-1" }, "Bedrijfsomgeving \u2014 alleen voor jou")), /* @__PURE__ */ React.createElement("form", { onSubmit: submit, className: "bg-[#F5F3EE] rounded-xl p-6 shadow-2xl" }, /* @__PURE__ */ React.createElement("h2", { className: "font-black uppercase tracking-wide text-[#1C2321] text-sm mb-4" }, mode === "signup" ? "Account aanmaken" : "Inloggen"), /* @__PURE__ */ React.createElement("label", { className: "block text-xs font-bold uppercase tracking-wide text-stone-600 mb-1" }, "E-mail"), /* @__PURE__ */ React.createElement("div", { className: "flex items-center gap-2 border-2 border-stone-300 rounded-lg px-3 py-2 mb-4 bg-white focus-within:border-[#2B4C7E]" }, /* @__PURE__ */ React.createElement("span", null, "\u2709\uFE0F"), /* @__PURE__ */ React.createElement("input", { type: "email", required: true, value: email, onChange: (e) => setEmail(e.target.value), className: "flex-1 outline-none text-sm bg-transparent", placeholder: "jij@umbouwbedrijf.nl" })), /* @__PURE__ */ React.createElement("label", { className: "block text-xs font-bold uppercase tracking-wide text-stone-600 mb-1" }, "Wachtwoord"), /* @__PURE__ */ React.createElement("div", { className: "flex items-center gap-2 border-2 border-stone-300 rounded-lg px-3 py-2 mb-4 bg-white focus-within:border-[#2B4C7E]" }, /* @__PURE__ */ React.createElement("span", null, "\u{1F512}"), /* @__PURE__ */ React.createElement("input", { type: "password", required: true, minLength: 6, value: pw, onChange: (e) => setPw(e.target.value), className: "flex-1 outline-none text-sm bg-transparent", placeholder: "\u2022\u2022\u2022\u2022\u2022\u2022\u2022\u2022" })), error && /* @__PURE__ */ React.createElement("p", { className: "text-[#B3441E] text-xs font-semibold mb-3" }, "\u26A0\uFE0F ", error), /* @__PURE__ */ React.createElement("button", { type: "submit", disabled: busy, className: "w-full bg-[#E8590C] hover:bg-[#d14f0a] disabled:opacity-60 text-white font-black uppercase tracking-wide text-sm py-3 rounded-lg transition-colors" }, busy ? "Bezig\u2026" : mode === "signup" ? "Account aanmaken" : "Inloggen"), /* @__PURE__ */ React.createElement("button", { type: "button", onClick: () => {
      setMode(mode === "signup" ? "login" : "signup");
      setError("");
    }, className: "w-full text-center text-xs text-stone-500 mt-3 underline" }, mode === "signup" ? "Heb je al een account? Inloggen" : "Eerste keer hier? Account aanmaken")), /* @__PURE__ */ React.createElement("p", { className: "text-center text-stone-500 text-[11px] mt-5 leading-relaxed px-4" }, "Echte login: je wachtwoord wordt nooit door deze app gezien of opgeslagen \u2014 alleen gecontroleerd door je eigen Supabase-database.")));
  }
  function Header({ onLogout, view, setView }) {
    var _a;
    const label = ((_a = NAV.find((n) => n.key === view)) == null ? void 0 : _a.label) || "";
    return /* @__PURE__ */ React.createElement("header", { className: "bg-[#2B4C7E] px-4 py-4 flex items-center justify-between sticky top-0 z-20 shadow-md" }, /* @__PURE__ */ React.createElement("div", { className: "flex items-center gap-2" }, /* @__PURE__ */ React.createElement("span", null, "\u{1F3D7}\uFE0F"), /* @__PURE__ */ React.createElement("div", null, /* @__PURE__ */ React.createElement("p", { className: "text-[#F5F3EE] font-black uppercase tracking-tight text-sm leading-none" }, "UM Bouwbedrijf"), /* @__PURE__ */ React.createElement("p", { className: "text-[#a9bcd8] text-[11px] mt-0.5" }, label))), /* @__PURE__ */ React.createElement("div", { className: "flex items-center gap-3" }, /* @__PURE__ */ React.createElement("nav", { className: "hidden md:flex items-center gap-1" }, NAV.map((n) => /* @__PURE__ */ React.createElement("button", { key: n.key, onClick: () => setView(n.key), className: `text-xs font-bold uppercase tracking-wide px-3 py-1.5 rounded transition-colors ${view === n.key ? "bg-[#E8590C] text-white" : "text-[#c7d5ea] hover:bg-white/10"}` }, n.label))), /* @__PURE__ */ React.createElement("button", { onClick: onLogout, className: "text-[#c7d5ea] hover:text-white p-1.5", title: "Uitloggen" }, "\u238B")));
  }
  function BottomNav({ view, setView }) {
    return /* @__PURE__ */ React.createElement("nav", { className: "md:hidden fixed bottom-0 left-0 right-0 bg-[#F5F3EE] border-t-2 border-stone-300 flex justify-around py-2 z-20" }, NAV.map((n) => {
      const active = view === n.key;
      return /* @__PURE__ */ React.createElement("button", { key: n.key, onClick: () => setView(n.key), className: `flex flex-col items-center gap-0.5 px-2 py-1 rounded-lg ${active ? "text-[#E8590C]" : "text-stone-500"}` }, /* @__PURE__ */ React.createElement("span", { className: "text-lg leading-none" }, n.icon), /* @__PURE__ */ React.createElement("span", { className: "text-[10px] font-bold uppercase tracking-wide" }, n.label));
    }));
  }
  function SectionHeader({ title, action }) {
    return /* @__PURE__ */ React.createElement("div", { className: "flex items-center justify-between mb-4" }, /* @__PURE__ */ React.createElement("h2", { className: "text-[#F5F3EE] font-black uppercase tracking-tight text-lg" }, title), action);
  }
  function EmptyState({ icon, text, sub }) {
    return /* @__PURE__ */ React.createElement("div", { className: "border-2 border-dashed border-stone-600 rounded-xl py-10 px-4 text-center" }, /* @__PURE__ */ React.createElement("div", { className: "text-3xl mb-2" }, icon), /* @__PURE__ */ React.createElement("p", { className: "text-stone-300 font-semibold text-sm" }, text), sub && /* @__PURE__ */ React.createElement("p", { className: "text-stone-500 text-xs mt-1" }, sub));
  }
  function Dashboard({ stats, customers, quotations, setView }) {
    const cards = [
      { label: "Klanten", value: stats.customers, icon: "\u{1F465}", onClick: () => setView("customers") },
      { label: "Openstaande offertes", value: stats.openQuotes, icon: "\u{1F4C4}", onClick: () => setView("quotations") },
      { label: "Waarde offertes", value: euro(stats.quoteValue), icon: "\u2705", onClick: () => setView("quotations") },
      { label: "Lopende projecten", value: stats.activeProjects, icon: "\u{1F3D7}\uFE0F", onClick: () => setView("projects") }
    ];
    const recentQuotes = [...quotations].sort((a, b) => b.date.localeCompare(a.date)).slice(0, 4);
    return /* @__PURE__ */ React.createElement("div", { className: "p-4 max-w-3xl mx-auto" }, /* @__PURE__ */ React.createElement(SectionHeader, { title: "Overzicht" }), /* @__PURE__ */ React.createElement("div", { className: "grid grid-cols-2 gap-3 mb-6" }, cards.map((c) => /* @__PURE__ */ React.createElement("button", { key: c.label, onClick: c.onClick, className: "bg-[#F5F3EE] rounded-xl p-4 text-left hover:-translate-y-0.5 transition-transform shadow" }, /* @__PURE__ */ React.createElement("div", { className: "text-xl mb-2" }, c.icon), /* @__PURE__ */ React.createElement("p", { className: "text-xl font-black text-[#1C2321] leading-none" }, c.value), /* @__PURE__ */ React.createElement("p", { className: "text-[11px] font-bold uppercase tracking-wide text-stone-500 mt-1" }, c.label)))), /* @__PURE__ */ React.createElement("h3", { className: "text-[#F5F3EE] font-black uppercase tracking-wide text-sm mb-3" }, "Recente offertes"), recentQuotes.length === 0 ? /* @__PURE__ */ React.createElement(EmptyState, { icon: "\u{1F4C4}", text: "Nog geen offertes", sub: "Maak er een aan bij 'Offertes'." }) : /* @__PURE__ */ React.createElement("div", { className: "space-y-2" }, recentQuotes.map((q) => {
      const cust = customers.find((c) => c.id === q.customer_id);
      const total = quoteTotal(q);
      return /* @__PURE__ */ React.createElement("div", { key: q.id, className: "bg-[#F5F3EE] rounded-lg p-3 flex items-center justify-between" }, /* @__PURE__ */ React.createElement("div", null, /* @__PURE__ */ React.createElement("p", { className: "font-bold text-[#1C2321] text-sm" }, cust ? cust.name : "Onbekende klant"), /* @__PURE__ */ React.createElement("p", { className: "text-stone-500 text-xs" }, q.date)), /* @__PURE__ */ React.createElement("div", { className: "text-right" }, /* @__PURE__ */ React.createElement("p", { className: "font-black text-[#1C2321] text-sm" }, euro(total)), /* @__PURE__ */ React.createElement(Stamp, { status: q.status }, q.status)));
    })));
  }
  function Modal({ title, onClose, children, wide }) {
    return /* @__PURE__ */ React.createElement("div", { className: "fixed inset-0 bg-black/60 z-30 flex items-end md:items-center justify-center p-0 md:p-6" }, /* @__PURE__ */ React.createElement("div", { className: `bg-[#F5F3EE] w-full ${wide ? "md:max-w-2xl" : "md:max-w-md"} md:rounded-xl rounded-t-xl max-h-[92vh] overflow-y-auto` }, /* @__PURE__ */ React.createElement("div", { className: "flex items-center justify-between px-5 py-4 border-b border-stone-300 sticky top-0 bg-[#F5F3EE]" }, /* @__PURE__ */ React.createElement("h3", { className: "font-black uppercase tracking-wide text-[#1C2321]" }, title), /* @__PURE__ */ React.createElement("button", { onClick: onClose, className: "text-stone-500 hover:text-[#1C2321] text-lg" }, "\u2715")), /* @__PURE__ */ React.createElement("div", { className: "p-5" }, children)));
  }
  function Field({ label, children }) {
    return /* @__PURE__ */ React.createElement("div", { className: "mb-3" }, /* @__PURE__ */ React.createElement("label", { className: "block text-xs font-bold uppercase tracking-wide text-stone-600 mb-1" }, label), children);
  }
  var inputCls = "w-full border-2 border-stone-300 rounded-lg px-3 py-2 text-sm outline-none focus:border-[#2B4C7E] bg-white";
  function SaveBtn({ busy, children }) {
    return /* @__PURE__ */ React.createElement("button", { disabled: busy, className: "w-full bg-[#2B4C7E] disabled:opacity-60 text-white font-black uppercase text-sm tracking-wide py-3 rounded-lg mt-2" }, busy ? "Bezig\u2026" : children);
  }
  function CustomersView({ customers, call, onChange }) {
    const [editing, setEditing] = useState(null);
    const [busy, setBusy] = useState(false);
    const empty = { name: "", phone: "", email: "", address: "" };
    const save = async (c) => {
      setBusy(true);
      try {
        if (c.id) await call((token) => db(`customers?id=eq.${c.id}`, { method: "PATCH", token, body: { name: c.name, phone: c.phone, email: c.email, address: c.address } }));
        else await call((token) => db("customers", { method: "POST", token, body: c, prefer: "return=representation" }));
        setEditing(null);
        await onChange();
      } catch (e) {
      } finally {
        setBusy(false);
      }
    };
    const remove = async (id) => {
      if (!confirm("Klant verwijderen?")) return;
      try {
        await call((token) => db(`customers?id=eq.${id}`, { method: "DELETE", token }));
        await onChange();
      } catch (e) {
      }
    };
    return /* @__PURE__ */ React.createElement("div", { className: "p-4 max-w-3xl mx-auto" }, /* @__PURE__ */ React.createElement(SectionHeader, { title: "Klanten", action: /* @__PURE__ */ React.createElement("button", { onClick: () => setEditing({ ...empty }), className: "bg-[#E8590C] text-white rounded-lg p-2 w-9 h-9 flex items-center justify-center text-lg" }, "\uFF0B") }), customers.length === 0 ? /* @__PURE__ */ React.createElement(EmptyState, { icon: "\u{1F465}", text: "Nog geen klanten", sub: "Voeg je eerste klant toe met de +." }) : /* @__PURE__ */ React.createElement("div", { className: "space-y-2" }, customers.map((c) => /* @__PURE__ */ React.createElement("div", { key: c.id, className: "bg-[#F5F3EE] rounded-lg p-4" }, /* @__PURE__ */ React.createElement("div", { className: "flex items-start justify-between" }, /* @__PURE__ */ React.createElement("p", { className: "font-bold text-[#1C2321]" }, c.name), /* @__PURE__ */ React.createElement("div", { className: "flex gap-1" }, /* @__PURE__ */ React.createElement("button", { onClick: () => setEditing(c), className: "p-1.5 text-stone-500 hover:text-[#2B4C7E]" }, "\u270F\uFE0F"), /* @__PURE__ */ React.createElement("button", { onClick: () => remove(c.id), className: "p-1.5 text-stone-500 hover:text-[#B3441E]" }, "\u{1F5D1}\uFE0F"))), /* @__PURE__ */ React.createElement("div", { className: "text-xs text-stone-600 mt-1 space-y-0.5" }, c.phone && /* @__PURE__ */ React.createElement("p", null, "\u260E ", c.phone), c.email && /* @__PURE__ */ React.createElement("p", null, "\u2709\uFE0F ", c.email), c.address && /* @__PURE__ */ React.createElement("p", null, "\u{1F4CD} ", c.address))))), editing && /* @__PURE__ */ React.createElement(Modal, { title: editing.id ? "Klant bewerken" : "Nieuwe klant", onClose: () => setEditing(null) }, /* @__PURE__ */ React.createElement("form", { onSubmit: (e) => {
      e.preventDefault();
      if (editing.name.trim()) save(editing);
    } }, /* @__PURE__ */ React.createElement(Field, { label: "Naam" }, /* @__PURE__ */ React.createElement("input", { required: true, className: inputCls, value: editing.name, onChange: (e) => setEditing({ ...editing, name: e.target.value }) })), /* @__PURE__ */ React.createElement(Field, { label: "Telefoon" }, /* @__PURE__ */ React.createElement("input", { className: inputCls, value: editing.phone || "", onChange: (e) => setEditing({ ...editing, phone: e.target.value }) })), /* @__PURE__ */ React.createElement(Field, { label: "E-mail" }, /* @__PURE__ */ React.createElement("input", { type: "email", className: inputCls, value: editing.email || "", onChange: (e) => setEditing({ ...editing, email: e.target.value }) })), /* @__PURE__ */ React.createElement(Field, { label: "Adres" }, /* @__PURE__ */ React.createElement("input", { className: inputCls, value: editing.address || "", onChange: (e) => setEditing({ ...editing, address: e.target.value }) })), /* @__PURE__ */ React.createElement(SaveBtn, { busy }, "Opslaan"))));
  }
  function PriceListView({ priceList, call, onChange }) {
    const [editing, setEditing] = useState(null);
    const [busy, setBusy] = useState(false);
    const empty = { name: "", unit: "stuk", price: "" };
    const save = async (item) => {
      setBusy(true);
      const body = { name: item.name, unit: item.unit, price: Number(item.price) || 0 };
      try {
        if (item.id) await call((token) => db(`price_list?id=eq.${item.id}`, { method: "PATCH", token, body }));
        else await call((token) => db("price_list", { method: "POST", token, body, prefer: "return=representation" }));
        setEditing(null);
        await onChange();
      } catch (e) {
      } finally {
        setBusy(false);
      }
    };
    const remove = async (id) => {
      if (!confirm("Prijs verwijderen?")) return;
      try {
        await call((token) => db(`price_list?id=eq.${id}`, { method: "DELETE", token }));
        await onChange();
      } catch (e) {
      }
    };
    return /* @__PURE__ */ React.createElement("div", { className: "p-4 max-w-3xl mx-auto" }, /* @__PURE__ */ React.createElement(SectionHeader, { title: "Prijslijst", action: /* @__PURE__ */ React.createElement("button", { onClick: () => setEditing({ ...empty }), className: "bg-[#E8590C] text-white rounded-lg p-2 w-9 h-9 flex items-center justify-center text-lg" }, "\uFF0B") }), priceList.length === 0 ? /* @__PURE__ */ React.createElement(EmptyState, { icon: "\u{1F4CB}", text: "Nog geen prijzen", sub: "Voeg standaardposten toe (bv. m\xB2 tegelwerk, uurtarief)." }) : /* @__PURE__ */ React.createElement("div", { className: "space-y-2" }, priceList.map((item) => /* @__PURE__ */ React.createElement("div", { key: item.id, className: "bg-[#F5F3EE] rounded-lg p-3 flex items-center justify-between" }, /* @__PURE__ */ React.createElement("div", null, /* @__PURE__ */ React.createElement("p", { className: "font-bold text-[#1C2321] text-sm" }, item.name), /* @__PURE__ */ React.createElement("p", { className: "text-stone-500 text-xs" }, "per ", item.unit)), /* @__PURE__ */ React.createElement("div", { className: "flex items-center gap-3" }, /* @__PURE__ */ React.createElement("p", { className: "font-black text-[#1C2321] text-sm" }, euro(item.price)), /* @__PURE__ */ React.createElement("button", { onClick: () => setEditing(item), className: "p-1 text-stone-500 hover:text-[#2B4C7E]" }, "\u270F\uFE0F"), /* @__PURE__ */ React.createElement("button", { onClick: () => remove(item.id), className: "p-1 text-stone-500 hover:text-[#B3441E]" }, "\u{1F5D1}\uFE0F"))))), editing && /* @__PURE__ */ React.createElement(Modal, { title: editing.id ? "Prijs bewerken" : "Nieuwe prijs", onClose: () => setEditing(null) }, /* @__PURE__ */ React.createElement("form", { onSubmit: (e) => {
      e.preventDefault();
      if (editing.name.trim()) save(editing);
    } }, /* @__PURE__ */ React.createElement(Field, { label: "Omschrijving" }, /* @__PURE__ */ React.createElement("input", { required: true, className: inputCls, value: editing.name, onChange: (e) => setEditing({ ...editing, name: e.target.value }) })), /* @__PURE__ */ React.createElement(Field, { label: "Eenheid" }, /* @__PURE__ */ React.createElement("input", { className: inputCls, value: editing.unit || "", onChange: (e) => setEditing({ ...editing, unit: e.target.value }), placeholder: "m\xB2, uur, stuk\u2026" })), /* @__PURE__ */ React.createElement(Field, { label: "Prijs (\u20AC)" }, /* @__PURE__ */ React.createElement("input", { required: true, type: "number", step: "0.01", className: inputCls, value: editing.price, onChange: (e) => setEditing({ ...editing, price: e.target.value }) })), /* @__PURE__ */ React.createElement(SaveBtn, { busy }, "Opslaan"))));
  }
  function QuotationsView({ quotations, customers, priceList, call, onChange }) {
    const [editing, setEditing] = useState(null);
    const [viewing, setViewing] = useState(null);
    const empty = { customer_id: "", date: (/* @__PURE__ */ new Date()).toISOString().slice(0, 10), status: "concept", notes: "", items: [], btw_percent: 21 };
    const save = async (q) => {
      const body = { customer_id: q.customer_id, date: q.date, status: q.status, notes: q.notes, items: q.items, btw_percent: q.btw_percent };
      try {
        let saved;
        if (q.id) saved = (await call((token) => db(`quotations?id=eq.${q.id}`, { method: "PATCH", token, body, prefer: "return=representation" })))[0];
        else saved = (await call((token) => db("quotations", { method: "POST", token, body, prefer: "return=representation" })))[0];
        setEditing(null);
        await onChange();
        return saved;
      } catch (e) {
      }
    };
    const remove = async (id) => {
      if (!confirm("Offerte verwijderen?")) return;
      try {
        await call((token) => db(`quotations?id=eq.${id}`, { method: "DELETE", token }));
        setViewing(null);
        await onChange();
      } catch (e) {
      }
    };
    return /* @__PURE__ */ React.createElement("div", { className: "p-4 max-w-3xl mx-auto" }, /* @__PURE__ */ React.createElement(SectionHeader, { title: "Offertes", action: /* @__PURE__ */ React.createElement("button", { onClick: () => setEditing({ ...empty }), disabled: customers.length === 0, className: "bg-[#E8590C] disabled:opacity-40 text-white rounded-lg p-2 w-9 h-9 flex items-center justify-center text-lg" }, "\uFF0B") }), customers.length === 0 && /* @__PURE__ */ React.createElement("p", { className: "text-stone-400 text-xs mb-3" }, "Voeg eerst een klant toe voordat je een offerte maakt."), quotations.length === 0 ? /* @__PURE__ */ React.createElement(EmptyState, { icon: "\u{1F4C4}", text: "Nog geen offertes" }) : /* @__PURE__ */ React.createElement("div", { className: "space-y-2" }, quotations.map((q) => {
      const cust = customers.find((c) => c.id === q.customer_id);
      const total = quoteTotal(q);
      return /* @__PURE__ */ React.createElement("button", { key: q.id, onClick: () => setViewing(q), className: "w-full text-left bg-[#F5F3EE] rounded-lg p-4 flex items-center justify-between" }, /* @__PURE__ */ React.createElement("div", null, /* @__PURE__ */ React.createElement("p", { className: "font-bold text-[#1C2321] text-sm" }, cust ? cust.name : "Onbekende klant"), /* @__PURE__ */ React.createElement("p", { className: "text-stone-500 text-xs" }, q.date, " \xB7 ", q.items.length, " regel", q.items.length !== 1 ? "s" : "")), /* @__PURE__ */ React.createElement("div", { className: "text-right" }, /* @__PURE__ */ React.createElement("p", { className: "font-black text-[#1C2321] text-sm mb-1" }, euro(total)), /* @__PURE__ */ React.createElement(Stamp, { status: q.status }, q.status)));
    })), editing && /* @__PURE__ */ React.createElement(Modal, { title: editing.id ? "Offerte bewerken" : "Nieuwe offerte", onClose: () => setEditing(null), wide: true }, /* @__PURE__ */ React.createElement(QuotationForm, { value: editing, customers, priceList, onSave: save })), viewing && /* @__PURE__ */ React.createElement(Modal, { title: "Offerte", onClose: () => setViewing(null), wide: true }, /* @__PURE__ */ React.createElement(
      QuotationDetail,
      {
        q: viewing,
        customer: customers.find((c) => c.id === viewing.customer_id),
        onEdit: () => {
          setEditing(viewing);
          setViewing(null);
        },
        onDelete: () => remove(viewing.id),
        onStatus: async (status) => {
          const saved = await save({ ...viewing, status });
          if (saved) setViewing(saved);
        }
      }
    )));
  }
  function QuotationForm({ value, customers, priceList, onSave }) {
    var _a;
    const [f, setF] = useState(value);
    const [pick, setPick] = useState("");
    const [busy, setBusy] = useState(false);
    const addLine = (fromPrice) => {
      const line = fromPrice ? { id: uid(), desc: fromPrice.name, unit: fromPrice.unit, qty: 1, price: fromPrice.price } : { id: uid(), desc: "", unit: "stuk", qty: 1, price: 0 };
      setF({ ...f, items: [...f.items, line] });
    };
    const updateLine = (id, patch) => setF({ ...f, items: f.items.map((it) => it.id === id ? { ...it, ...patch } : it) });
    const removeLine = (id) => setF({ ...f, items: f.items.filter((it) => it.id !== id) });
    const subtotal = f.items.reduce((s, it) => s + (Number(it.qty) || 0) * (Number(it.price) || 0), 0);
    const btwPct = Number((_a = f.btw_percent) != null ? _a : 21);
    const btwAmount = subtotal * (btwPct / 100);
    const total = subtotal + btwAmount;
    const submit = async (e) => {
      e.preventDefault();
      if (!f.customer_id || !f.items.length) return;
      setBusy(true);
      const clean = { ...f, items: f.items.map((it) => ({ ...it, qty: Number(it.qty) || 0, price: Number(it.price) || 0 })) };
      await onSave(clean);
      setBusy(false);
    };
    return /* @__PURE__ */ React.createElement("form", { onSubmit: submit }, /* @__PURE__ */ React.createElement("div", { className: "grid grid-cols-2 gap-3" }, /* @__PURE__ */ React.createElement(Field, { label: "Klant" }, /* @__PURE__ */ React.createElement("select", { required: true, className: inputCls, value: f.customer_id, onChange: (e) => setF({ ...f, customer_id: e.target.value }) }, /* @__PURE__ */ React.createElement("option", { value: "" }, "Kies klant\u2026"), customers.map((c) => /* @__PURE__ */ React.createElement("option", { key: c.id, value: c.id }, c.name)))), /* @__PURE__ */ React.createElement(Field, { label: "Datum" }, /* @__PURE__ */ React.createElement("input", { type: "date", className: inputCls, value: f.date, onChange: (e) => setF({ ...f, date: e.target.value }) }))), /* @__PURE__ */ React.createElement("div", { className: "flex items-center justify-between mt-3 mb-2" }, /* @__PURE__ */ React.createElement("p", { className: "text-xs font-bold uppercase tracking-wide text-stone-600" }, "Regels"), priceList.length > 0 && /* @__PURE__ */ React.createElement("div", { className: "flex gap-2" }, /* @__PURE__ */ React.createElement("select", { className: "text-xs border-2 border-stone-300 rounded-lg px-2 py-1 bg-white", value: pick, onChange: (e) => setPick(e.target.value) }, /* @__PURE__ */ React.createElement("option", { value: "" }, "Uit prijslijst\u2026"), priceList.map((p) => /* @__PURE__ */ React.createElement("option", { key: p.id, value: p.id }, p.name))), /* @__PURE__ */ React.createElement("button", { type: "button", onClick: () => {
      const p = priceList.find((x) => x.id === pick);
      if (p) addLine(p);
      setPick("");
    }, className: "text-xs font-bold text-[#2B4C7E]" }, "Toevoegen"))), /* @__PURE__ */ React.createElement("div", { className: "space-y-2 mb-2" }, f.items.map((it) => /* @__PURE__ */ React.createElement("div", { key: it.id, className: "bg-white border border-stone-300 rounded-lg p-2 grid grid-cols-12 gap-1.5 items-center" }, /* @__PURE__ */ React.createElement("input", { className: "col-span-5 text-xs border border-stone-300 rounded px-2 py-1.5", placeholder: "Omschrijving", value: it.desc, onChange: (e) => updateLine(it.id, { desc: e.target.value }) }), /* @__PURE__ */ React.createElement("input", { type: "number", step: "0.01", className: "col-span-2 text-xs border border-stone-300 rounded px-2 py-1.5", placeholder: "Aantal", value: it.qty, onChange: (e) => updateLine(it.id, { qty: e.target.value }) }), /* @__PURE__ */ React.createElement("input", { className: "col-span-2 text-xs border border-stone-300 rounded px-2 py-1.5", placeholder: "Eenh.", value: it.unit, onChange: (e) => updateLine(it.id, { unit: e.target.value }) }), /* @__PURE__ */ React.createElement("input", { type: "number", step: "0.01", className: "col-span-2 text-xs border border-stone-300 rounded px-2 py-1.5", placeholder: "Prijs", value: it.price, onChange: (e) => updateLine(it.id, { price: e.target.value }) }), /* @__PURE__ */ React.createElement("button", { type: "button", onClick: () => removeLine(it.id), className: "col-span-1 text-stone-400 hover:text-[#B3441E] flex justify-center" }, "\u{1F5D1}\uFE0F")))), /* @__PURE__ */ React.createElement("button", { type: "button", onClick: () => addLine(null), className: "text-xs font-bold text-[#2B4C7E] mb-3" }, "\uFF0B Losse regel toevoegen"), /* @__PURE__ */ React.createElement(Field, { label: "Notities" }, /* @__PURE__ */ React.createElement("textarea", { className: inputCls, rows: 2, value: f.notes || "", onChange: (e) => setF({ ...f, notes: e.target.value }) })), /* @__PURE__ */ React.createElement("div", { className: "flex items-center justify-between mb-3" }, /* @__PURE__ */ React.createElement("p", { className: "text-xs font-bold uppercase tracking-wide text-stone-600" }, "BTW"), /* @__PURE__ */ React.createElement("div", { className: "flex gap-2" }, [0, 9, 21].map((pct) => /* @__PURE__ */ React.createElement("button", { key: pct, type: "button", onClick: () => setF({ ...f, btw_percent: pct }), className: `text-xs font-bold px-3 py-1.5 rounded border-2 ${btwPct === pct ? "bg-[#2B4C7E] text-white border-[#2B4C7E]" : "border-stone-300 text-stone-600"}` }, pct, "%")))), /* @__PURE__ */ React.createElement("div", { className: "border-t border-stone-300 pt-3 mt-2 space-y-1" }, /* @__PURE__ */ React.createElement("div", { className: "flex items-center justify-between text-sm" }, /* @__PURE__ */ React.createElement("p", { className: "text-stone-600" }, "Subtotaal (excl. btw)"), /* @__PURE__ */ React.createElement("p", { className: "font-semibold text-[#1C2321]" }, euro(subtotal))), /* @__PURE__ */ React.createElement("div", { className: "flex items-center justify-between text-sm" }, /* @__PURE__ */ React.createElement("p", { className: "text-stone-600" }, "Btw (", btwPct, "%)"), /* @__PURE__ */ React.createElement("p", { className: "font-semibold text-[#1C2321]" }, euro(btwAmount))), /* @__PURE__ */ React.createElement("div", { className: "flex items-center justify-between pt-1" }, /* @__PURE__ */ React.createElement("p", { className: "font-black uppercase text-sm text-stone-600" }, "Totaal (incl. btw)"), /* @__PURE__ */ React.createElement("p", { className: "font-black text-lg text-[#1C2321]" }, euro(total)))), /* @__PURE__ */ React.createElement(SaveBtn, { busy }, "Offerte opslaan"));
  }
  function QuotationDetail({ q, customer, onEdit, onDelete, onStatus }) {
    var _a;
    const subtotal = q.items.reduce((s, it) => s + it.qty * it.price, 0);
    const btwPct = Number((_a = q.btw_percent) != null ? _a : 21);
    const btwAmount = subtotal * (btwPct / 100);
    const total = subtotal + btwAmount;
    return /* @__PURE__ */ React.createElement("div", null, /* @__PURE__ */ React.createElement("div", { className: "flex items-center justify-between mb-3" }, /* @__PURE__ */ React.createElement("div", null, /* @__PURE__ */ React.createElement("p", { className: "font-bold text-[#1C2321]" }, customer ? customer.name : "Onbekende klant"), /* @__PURE__ */ React.createElement("p", { className: "text-stone-500 text-xs" }, q.date)), /* @__PURE__ */ React.createElement(Stamp, { status: q.status }, q.status)), /* @__PURE__ */ React.createElement("div", { className: "border border-stone-300 rounded-lg overflow-hidden mb-3" }, q.items.map((it, i) => /* @__PURE__ */ React.createElement("div", { key: it.id || i, className: `flex items-center justify-between px-3 py-2 text-sm ${i % 2 ? "bg-white" : "bg-stone-100"}` }, /* @__PURE__ */ React.createElement("div", null, /* @__PURE__ */ React.createElement("p", { className: "text-[#1C2321]" }, it.desc), /* @__PURE__ */ React.createElement("p", { className: "text-stone-500 text-xs" }, it.qty, " ", it.unit, " \xD7 ", euro(it.price))), /* @__PURE__ */ React.createElement("p", { className: "font-bold text-[#1C2321]" }, euro(it.qty * it.price))))), /* @__PURE__ */ React.createElement("div", { className: "space-y-1 mb-4" }, /* @__PURE__ */ React.createElement("div", { className: "flex items-center justify-between text-sm" }, /* @__PURE__ */ React.createElement("p", { className: "text-stone-600" }, "Subtotaal (excl. btw)"), /* @__PURE__ */ React.createElement("p", { className: "font-semibold text-[#1C2321]" }, euro(subtotal))), /* @__PURE__ */ React.createElement("div", { className: "flex items-center justify-between text-sm" }, /* @__PURE__ */ React.createElement("p", { className: "text-stone-600" }, "Btw (", btwPct, "%)"), /* @__PURE__ */ React.createElement("p", { className: "font-semibold text-[#1C2321]" }, euro(btwAmount))), /* @__PURE__ */ React.createElement("div", { className: "flex items-center justify-between pt-1" }, /* @__PURE__ */ React.createElement("p", { className: "font-black uppercase text-sm text-stone-600" }, "Totaal (incl. btw)"), /* @__PURE__ */ React.createElement("p", { className: "font-black text-xl text-[#1C2321]" }, euro(total)))), q.notes && /* @__PURE__ */ React.createElement("p", { className: "text-sm text-stone-600 mb-4 italic" }, '"', q.notes, '"'), /* @__PURE__ */ React.createElement("p", { className: "text-xs font-bold uppercase tracking-wide text-stone-500 mb-2" }, "Status wijzigen"), /* @__PURE__ */ React.createElement("div", { className: "flex flex-wrap gap-2 mb-4" }, ["concept", "verzonden", "geaccepteerd", "afgewezen"].map((s) => /* @__PURE__ */ React.createElement("button", { key: s, onClick: () => onStatus(s), className: `text-xs font-bold uppercase px-3 py-1.5 rounded border-2 ${q.status === s ? "bg-[#2B4C7E] text-white border-[#2B4C7E]" : "border-stone-300 text-stone-600"}` }, s))), /* @__PURE__ */ React.createElement("div", { className: "flex gap-2" }, /* @__PURE__ */ React.createElement("button", { onClick: onEdit, className: "flex-1 border-2 border-[#2B4C7E] text-[#2B4C7E] font-bold uppercase text-xs py-2.5 rounded-lg" }, "Bewerken"), /* @__PURE__ */ React.createElement("button", { onClick: onDelete, className: "flex-1 border-2 border-[#B3441E] text-[#B3441E] font-bold uppercase text-xs py-2.5 rounded-lg" }, "Verwijderen")));
  }
  function ProjectsView({ projects, customers, call, onChange }) {
    const [editing, setEditing] = useState(null);
    const [openId, setOpenId] = useState(null);
    const [busy, setBusy] = useState(false);
    const empty = { customer_id: "", title: "", address: "", status: "lopend", notes: "" };
    const save = async (p) => {
      setBusy(true);
      const body = { customer_id: p.customer_id, title: p.title, address: p.address, status: p.status, notes: p.notes };
      try {
        if (p.id) await call((token) => db(`projects?id=eq.${p.id}`, { method: "PATCH", token, body }));
        else await call((token) => db("projects", { method: "POST", token, body, prefer: "return=representation" }));
        setEditing(null);
        await onChange();
      } catch (e) {
      } finally {
        setBusy(false);
      }
    };
    const remove = async (id) => {
      if (!confirm("Project (en foto's) verwijderen?")) return;
      try {
        await call((token) => db(`projects?id=eq.${id}`, { method: "DELETE", token }));
        setOpenId(null);
        await onChange();
      } catch (e) {
      }
    };
    if (openId) {
      const project = projects.find((p) => p.id === openId);
      if (!project) {
        setOpenId(null);
        return null;
      }
      return /* @__PURE__ */ React.createElement(
        ProjectDetail,
        {
          project,
          customer: customers.find((c) => c.id === project.customer_id),
          call,
          onBack: () => setOpenId(null),
          onEdit: () => setEditing(project),
          onDelete: () => remove(project.id),
          onStatus: (status) => save({ ...project, status })
        }
      );
    }
    return /* @__PURE__ */ React.createElement("div", { className: "p-4 max-w-3xl mx-auto" }, /* @__PURE__ */ React.createElement(SectionHeader, { title: "Projecten", action: /* @__PURE__ */ React.createElement("button", { onClick: () => setEditing({ ...empty }), disabled: customers.length === 0, className: "bg-[#E8590C] disabled:opacity-40 text-white rounded-lg p-2 w-9 h-9 flex items-center justify-center text-lg" }, "\uFF0B") }), customers.length === 0 && /* @__PURE__ */ React.createElement("p", { className: "text-stone-400 text-xs mb-3" }, "Voeg eerst een klant toe voordat je een project aanmaakt."), projects.length === 0 ? /* @__PURE__ */ React.createElement(EmptyState, { icon: "\u{1F3D7}\uFE0F", text: "Nog geen projecten" }) : /* @__PURE__ */ React.createElement("div", { className: "space-y-2" }, projects.map((p) => {
      const cust = customers.find((c) => c.id === p.customer_id);
      return /* @__PURE__ */ React.createElement("button", { key: p.id, onClick: () => setOpenId(p.id), className: "w-full text-left bg-[#F5F3EE] rounded-lg p-4 flex items-center justify-between" }, /* @__PURE__ */ React.createElement("div", null, /* @__PURE__ */ React.createElement("p", { className: "font-bold text-[#1C2321] text-sm" }, p.title || "Zonder titel"), /* @__PURE__ */ React.createElement("p", { className: "text-stone-500 text-xs" }, cust ? cust.name : "Onbekende klant", p.address ? " \xB7 " + p.address : "")), /* @__PURE__ */ React.createElement(Stamp, { status: p.status }, p.status));
    })), editing && /* @__PURE__ */ React.createElement(Modal, { title: editing.id ? "Project bewerken" : "Nieuw project", onClose: () => setEditing(null) }, /* @__PURE__ */ React.createElement("form", { onSubmit: (e) => {
      e.preventDefault();
      if (editing.customer_id && editing.title.trim()) save(editing);
    } }, /* @__PURE__ */ React.createElement(Field, { label: "Klant" }, /* @__PURE__ */ React.createElement("select", { required: true, className: inputCls, value: editing.customer_id, onChange: (e) => setEditing({ ...editing, customer_id: e.target.value }) }, /* @__PURE__ */ React.createElement("option", { value: "" }, "Kies klant\u2026"), customers.map((c) => /* @__PURE__ */ React.createElement("option", { key: c.id, value: c.id }, c.name)))), /* @__PURE__ */ React.createElement(Field, { label: "Projecttitel" }, /* @__PURE__ */ React.createElement("input", { required: true, className: inputCls, value: editing.title, onChange: (e) => setEditing({ ...editing, title: e.target.value }), placeholder: "Bijv. Verbouwing badkamer" })), /* @__PURE__ */ React.createElement(Field, { label: "Adres" }, /* @__PURE__ */ React.createElement("input", { className: inputCls, value: editing.address || "", onChange: (e) => setEditing({ ...editing, address: e.target.value }) })), /* @__PURE__ */ React.createElement(Field, { label: "Notities" }, /* @__PURE__ */ React.createElement("textarea", { className: inputCls, rows: 3, value: editing.notes || "", onChange: (e) => setEditing({ ...editing, notes: e.target.value }) })), /* @__PURE__ */ React.createElement(SaveBtn, { busy }, "Opslaan"))));
  }
  function ProjectDetail({ project, customer, call, onBack, onEdit, onDelete, onStatus }) {
    const [photos, setPhotos] = useState([]);
    const [loadedPhotos, setLoadedPhotos] = useState(false);
    const [uploading, setUploading] = useState(false);
    const fileRef = useRef(null);
    const loadPhotos = useCallback(async () => {
      try {
        const rows = await call((token) => db(`project_photos?project_id=eq.${project.id}&select=*&order=created_at.asc`, { token }));
        setPhotos(rows);
      } catch (e) {
      } finally {
        setLoadedPhotos(true);
      }
    }, [project.id, call]);
    useEffect(() => {
      loadPhotos();
    }, [loadPhotos]);
    const handleFiles = async (files) => {
      setUploading(true);
      for (const file of Array.from(files)) {
        try {
          const dataUrl = await resizeImage(file);
          await call((token) => db("project_photos", { method: "POST", token, body: { project_id: project.id, data_url: dataUrl }, prefer: "return=representation" }));
        } catch (e) {
          console.error(e);
        }
      }
      await loadPhotos();
      setUploading(false);
    };
    const removePhoto = async (id) => {
      try {
        await call((token) => db(`project_photos?id=eq.${id}`, { method: "DELETE", token }));
        await loadPhotos();
      } catch (e) {
      }
    };
    return /* @__PURE__ */ React.createElement("div", { className: "p-4 max-w-3xl mx-auto" }, /* @__PURE__ */ React.createElement("button", { onClick: onBack, className: "text-stone-300 text-sm mb-3" }, "\u2039 Terug naar projecten"), /* @__PURE__ */ React.createElement("div", { className: "bg-[#F5F3EE] rounded-xl p-5 mb-4" }, /* @__PURE__ */ React.createElement("div", { className: "flex items-start justify-between mb-2" }, /* @__PURE__ */ React.createElement("div", null, /* @__PURE__ */ React.createElement("h2", { className: "font-black text-lg text-[#1C2321]" }, project.title), /* @__PURE__ */ React.createElement("p", { className: "text-stone-500 text-sm" }, customer ? customer.name : "Onbekende klant"), project.address && /* @__PURE__ */ React.createElement("p", { className: "text-stone-500 text-xs mt-0.5" }, "\u{1F4CD} ", project.address)), /* @__PURE__ */ React.createElement(Stamp, { status: project.status }, project.status)), project.notes && /* @__PURE__ */ React.createElement("p", { className: "text-sm text-stone-600 mt-2" }, project.notes), /* @__PURE__ */ React.createElement("div", { className: "flex flex-wrap gap-2 mt-4" }, ["lopend", "afgerond"].map((s) => /* @__PURE__ */ React.createElement("button", { key: s, onClick: () => onStatus(s), className: `text-xs font-bold uppercase px-3 py-1.5 rounded border-2 ${project.status === s ? "bg-[#2B4C7E] text-white border-[#2B4C7E]" : "border-stone-300 text-stone-600"}` }, s))), /* @__PURE__ */ React.createElement("div", { className: "flex gap-2 mt-4" }, /* @__PURE__ */ React.createElement("button", { onClick: onEdit, className: "flex-1 border-2 border-[#2B4C7E] text-[#2B4C7E] font-bold uppercase text-xs py-2 rounded-lg" }, "Bewerken"), /* @__PURE__ */ React.createElement("button", { onClick: onDelete, className: "flex-1 border-2 border-[#B3441E] text-[#B3441E] font-bold uppercase text-xs py-2 rounded-lg" }, "Verwijderen"))), /* @__PURE__ */ React.createElement("div", { className: "flex items-center justify-between mb-3" }, /* @__PURE__ */ React.createElement("h3", { className: "text-[#F5F3EE] font-black uppercase tracking-wide text-sm" }, "\u{1F4F7} Foto's"), /* @__PURE__ */ React.createElement("button", { onClick: () => fileRef.current && fileRef.current.click(), disabled: uploading, className: "bg-[#E8590C] text-white text-xs font-bold uppercase px-3 py-1.5 rounded-lg" }, "\uFF0B ", uploading ? "Bezig\u2026" : "Foto toevoegen"), /* @__PURE__ */ React.createElement("input", { ref: fileRef, type: "file", accept: "image/*", multiple: true, capture: "environment", className: "hidden", onChange: (e) => e.target.files.length && handleFiles(e.target.files) })), !loadedPhotos ? /* @__PURE__ */ React.createElement("p", { className: "text-stone-400 text-xs" }, "Laden\u2026") : photos.length === 0 ? /* @__PURE__ */ React.createElement(EmptyState, { icon: "\u{1F5BC}\uFE0F", text: "Nog geen foto's", sub: "Maak foto's rechtstreeks vanaf je telefoon." }) : /* @__PURE__ */ React.createElement("div", { className: "grid grid-cols-3 gap-2" }, photos.map((p) => /* @__PURE__ */ React.createElement("div", { key: p.id, className: "relative group aspect-square rounded-lg overflow-hidden bg-stone-800" }, /* @__PURE__ */ React.createElement("img", { src: p.data_url, alt: "", className: "w-full h-full object-cover" }), /* @__PURE__ */ React.createElement("button", { onClick: () => removePhoto(p.id), className: "absolute top-1 right-1 bg-black/60 text-white rounded-full p-1 opacity-90 text-xs w-5 h-5 flex items-center justify-center" }, "\u{1F5D1}\uFE0F")))));
  }
  var root = ReactDOM.createRoot(document.getElementById("root"));
  root.render(/* @__PURE__ */ React.createElement(App, null));
})();

</script>
</body>
</html>

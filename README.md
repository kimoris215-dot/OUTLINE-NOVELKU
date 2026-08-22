<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Novel Consult Workspace</title>

  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Poppins:wght@500;600;700&display=swap" rel="stylesheet" />

  <!-- React & ReactDOM (Production/UMD CDN) -->
  <script src="https://unpkg.com/react@18/umd/react.production.min.js" crossorigin></script>
  <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js" crossorigin></script>

  <!-- Lucide Icons (Global Object: lucide) -->
  <script src="https://unpkg.com/lucide@latest"></script>

  <!-- Babel Standalone (Compiles JSX directly in browser) -->
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

  <style>
    * { box-sizing: border-box; }
    body, html {
      margin: 0;
      padding: 0;
      height: 100%;
      font-family: 'Inter', sans-serif;
      background-color: #F6F4FC;
      color: #1F1147;
    }
    button { font-family: inherit; }
    input, textarea, select { font-family: inherit; outline: none; }
    ::-webkit-scrollbar { width: 8px; height: 8px; }
    ::-webkit-scrollbar-thumb { background: #D9D2F0; border-radius: 8px; }
    .nc-navbtn:hover { background: rgba(255,255,255,0.08) !important; }
    .nc-clickable { cursor: pointer; transition: transform 0.15s ease, box-shadow 0.15s ease; }
    .nc-clickable:hover { transform: translateY(-2px); box-shadow: 0 6px 18px rgba(31,17,71,0.08); }
  </style>
</head>
<body>
  <div id="root"></div>

  <script type="text/babel">
    const { useState, useEffect, useRef, useCallback } = React;

    /* ---------------------------------------------------------------
       LUCIDE ICONS SETUP
    ---------------------------------------------------------------- */
    const createLucideIcon = (name) => (props) => {
      const ref = useRef(null);
      useEffect(() => {
        if (ref.current) {
          ref.current.innerHTML = '';
          if (lucide.icons && lucide.icons[name]) {
            const svg = lucide.createSvgElement(lucide.icons[name]);
            if (props.size) {
              svg.setAttribute('width', props.size);
              svg.setAttribute('height', props.size);
            }
            if (props.color) {
              svg.setAttribute('stroke', props.color);
            }
            ref.current.appendChild(svg);
          }
        }
      }, [props.size, props.color]);
      return <span ref={ref} style={{ display: 'inline-flex', alignItems: 'center', justifyContent: 'center' }} />;
    };

    const Home = createLucideIcon('Home');
    const BookOpen = createLucideIcon('BookOpen');
    const FileText = createLucideIcon('FileText');
    const MapIcon = createLucideIcon('Map');
    const Users = createLucideIcon('Users');
    const MessageSquare = createLucideIcon('MessageSquare');
    const Lightbulb = createLucideIcon('Lightbulb');
    const BarChart2 = createLucideIcon('BarChart2');
    const Settings = createLucideIcon('Settings');
    const Search = createLucideIcon('Search');
    const Bell = createLucideIcon('Bell');
    const ChevronLeft = createLucideIcon('ChevronLeft');
    const ChevronRight = createLucideIcon('ChevronRight');
    const Plus = createLucideIcon('Plus');
    const Pencil = createLucideIcon('Pencil');
    const Flame = createLucideIcon('Flame');
    const Target = createLucideIcon('Target');
    const Clock = createLucideIcon('Clock');
    const Star = createLucideIcon('Star');
    const ArrowRight = createLucideIcon('ArrowRight');
    const Check = createLucideIcon('Check');
    const X = createLucideIcon('X');
    const Trash2 = createLucideIcon('Trash2');
    const Camera = createLucideIcon('Camera');
    const AlertTriangle = createLucideIcon('AlertTriangle');
    const ChevronDown = createLucideIcon('ChevronDown');
    const User = createLucideIcon('User');
    const Lock = createLucideIcon('Lock');
    const Globe = createLucideIcon('Globe');
    const LogOut = createLucideIcon('LogOut');
    const ImageIcon = createLucideIcon('Image');

    /* ---------------------------------------------------------------
       TRANSLATIONS
    ---------------------------------------------------------------- */
    const STRINGS = {
      id: {
        tagline: "Workspace Pribadiku",
        nav_beranda: "Beranda", nav_novelku: "Novelku", nav_chapters: "Chapter Manager",
        nav_planner: "Story Planner", nav_characters: "Character Database",
        nav_consult: "Catatan Konsultasi", nav_ideas: "Idea Vault",
        nav_progress: "Writing Progress", nav_settings: "Pengaturan",
        mascotBubble: "Teruslah menulis, ceritamu luar biasa!",
        lihatProfil: "Lihat Profil",
        searchPlaceholder: "Cari di Novel Consult...",
        pengingat: "Pengingat", pengingatBaru: "Pengingat baru...", pengingatKosong: "Belum ada pengingat.",
        halo: "Halo", siapMenulis: "Mari kembangkan ceritamu hari ini.",
        quote: "Setiap kata yang kamu tulis adalah langkah menuju novel yang luar biasa.",
        ringkasanHariIni: "Ringkasan Hari Ini", kataDitulis: "Kata ditulis", menitFokus: "Menit fokus",
        chapterBulanIni: "Chapter bulan ini", targetBulanIni: "Target bulan ini",
        novelAktif: "Novel Aktif", lanjutMenulis: "Lanjut Menulis", belumAdaNovel: "Belum ada novel aktif",
        mulaiNovelPertama: "Yuk mulai novel pertamamu dan kembangkan ceritamu di sini.",
        novelBaru: "Novel Baru", quickAccess: "Quick Access",
        qa_tulis: "Tulis Novel", qa_tulis_sub: "Lanjutkan menulis chapter",
        qa_planner: "Story Planner", qa_planner_sub: "Atur alur & konflik cerita",
        qa_char: "Character Database", qa_char_sub: "Kelola karakter & hubungan",
        qa_novelku: "Novelku", qa_novelku_sub: "Kelola semua novelmu",
        qa_consult: "Catatan Konsultasi", qa_consult_sub: "Lihat masukan & revisi",
        qa_ideas: "Idea Vault", qa_ideas_sub: "Simpan ide cemerlangmu",
        qa_progress: "Writing Progress", qa_progress_sub: "Pantau progres menulismu",
        qa_settings: "Pengaturan", qa_settings_sub: "Profil, akun & bahasa",
        novelkuTitle: "Novelku", novelkuSub: "Semua novel yang sedang dan pernah kamu tulis.",
        tambahNovelBaru: "Tambah Novel Baru", judulNovel: "Judul novel", genreNovel: "Genre (mis. Fantasy • Adventure)",
        buatNovel: "Buat Novel", pilihCoverGaleri: "Pilih Cover dari Galeri", gantiCover: "Ganti Cover",
        bukaChapterManager: "Buka Chapter Manager", belumAdaNovelSama: "Belum ada novel. Tambahkan novel pertamamu untuk mulai menulis.",
        plannerTitle: "Story Planner", plannerSub: "Atur alur, konflik, dan motif cerita per novel.",
        charTitle: "Character Database", charSub: "Kelola karakter dan hubungan mereka.",
        consultTitle: "Catatan Konsultasi", consultSub: "Semua masukan dan revisi dari konsultasimu.",
        ideaTitle: "Idea Vault", ideaSub: "Simpan semua ide cemerlangmu di sini.",
        progressTitle: "Writing Progress", progressSub: "Statistik menyeluruh progres menulismu.",
        settingsTitle: "Pengaturan", settingsSub: "Kelola profil, akun, dan preferensi bahasa.",
        simpan: "Simpan", batal: "Batal", tambah: "Tambah", tersimpan: "Tersimpan",
        pilihNovelDulu: "Pilih atau tambahkan novel terlebih dahulu di halaman Novelku.",
        tabProfil: "Profil", tabAkun: "Akun", tabBahasa: "Bahasa",
        namaLabel: "Nama", bioLabel: "Bio", simpanProfil: "Simpan Profil", gantiFoto: "Ganti Foto",
        emailLabel: "Email", passLama: "Kata Sandi Saat Ini", passBaru: "Kata Sandi Baru", passKonfirmasi: "Konfirmasi Kata Sandi",
        gantiPassword: "Ganti Kata Sandi", passTidakCocok: "Kata sandi baru dan konfirmasi tidak cocok.",
        passBerhasil: "Kata sandi berhasil diubah.", keluarAkun: "Keluar dari Akun",
        keluarKonfirmasi: "Yakin ingin keluar dari akun ini?", sudahKeluar: "Kamu sudah keluar dari akun.",
        masukKembali: "Masuk Kembali", pilihBahasa: "Pilih bahasa tampilan aplikasi.",
        bahasaID: "Bahasa Indonesia", bahasaEN: "English",
        memuat: "Memuat data...",
      },
      en: {
        tagline: "My Workspace",
        nav_beranda: "Home", nav_novelku: "My Novels", nav_chapters: "Chapter Manager",
        nav_planner: "Story Planner", nav_characters: "Character Database",
        nav_consult: "Consultation Notes", nav_ideas: "Idea Vault",
        nav_progress: "Writing Progress", nav_settings: "Settings",
        mascotBubble: "Keep writing, your story is amazing!",
        lihatProfil: "View Profile",
        searchPlaceholder: "Search Novel Consult...",
        pengingat: "Reminders", pengingatBaru: "New reminder...", pengingatKosong: "No reminders yet.",
        halo: "Hi", siapMenulis: "Let's grow your story today.",
        quote: "Every word you write is a step toward an amazing novel.",
        ringkasanHariIni: "Today's Summary", kataDitulis: "Words written", menitFokus: "Focus minutes",
        chapterBulanIni: "Chapters this month", targetBulanIni: "Target this month",
        novelAktif: "Active Novel", lanjutMenulis: "Keep Writing", belumAdaNovel: "No active novel yet",
        mulaiNovelPertama: "Start your first novel and grow your story here.",
        novelBaru: "New Novel", quickAccess: "Quick Access",
        qa_tulis: "Write", qa_tulis_sub: "Continue writing a chapter",
        qa_planner: "Story Planner", qa_planner_sub: "Plan plot & conflict",
        qa_char: "Character Database", qa_char_sub: "Manage characters & relations",
        qa_novelku: "My Novels", qa_novelku_sub: "Manage all your novels",
        qa_consult: "Consultation Notes", qa_consult_sub: "See feedback & revisions",
        qa_ideas: "Idea Vault", qa_ideas_sub: "Save your brilliant ideas",
        qa_progress: "Writing Progress", qa_progress_sub: "Track your writing progress",
        qa_settings: "Settings", qa_settings_sub: "Profile, account & language",
        novelkuTitle: "My Novels", novelkuSub: "All the novels you're writing or have written.",
        tambahNovelBaru: "Add New Novel", judulNovel: "Novel title", genreNovel: "Genre (e.g. Fantasy • Adventure)",
        buatNovel: "Create Novel", pilihCoverGaleri: "Choose Cover from Gallery", gantiCover: "Change Cover",
        bukaChapterManager: "Open Chapter Manager", belumAdaNovelSama: "No novels yet. Add your first novel to start writing.",
        plannerTitle: "Story Planner", plannerSub: "Plan the plot, conflict, and motifs per novel.",
        charTitle: "Character Database", charSub: "Manage characters and their relationships.",
        consultTitle: "Consultation Notes", consultSub: "All the feedback and revisions from your consultations.",
        ideaTitle: "Idea Vault", ideaSub: "Save all your brilliant ideas here.",
        progressTitle: "Writing Progress", progressSub: "A full overview of your writing progress.",
        settingsTitle: "Settings", settingsSub: "Manage your profile, account, and language preferences.",
        simpan: "Save", batal: "Cancel", tambah: "Add", tersimpan: "Saved",
        pilihNovelDulu: "Select or add a novel first on the My Novels page.",
        tabProfil: "Profile", tabAkun: "Account", tabBahasa: "Language",
        namaLabel: "Name", bioLabel: "Bio", simpanProfil: "Save Profile", gantiFoto: "Change Photo",
        emailLabel: "Email", passLama: "Current Password", passBaru: "New Password", passKonfirmasi: "Confirm Password",
        gantiPassword: "Change Password", passTidakCocok: "New password and confirmation don't match.",
        passBerhasil: "Password changed successfully.", keluarAkun: "Log Out",
        keluarKonfirmasi: "Are you sure you want to log out?", sudahKeluar: "You have been logged out.",
        masukKembali: "Log In Again", pilihBahasa: "Choose the app's display language.",
        bahasaID: "Bahasa Indonesia", bahasaEN: "English",
        memuat: "Loading data...",
      },
    };

    /* ---------------------------------------------------------------
       MASCOT
    ---------------------------------------------------------------- */
    function Mascot({ size = 64, mood = "happy", className = "" }) {
      return (
        <svg className={className} width={size} height={size} viewBox="0 0 100 100" fill="none" xmlns="http://www.w3.org/2000/svg">
          <ellipse cx="50" cy="58" rx="34" ry="30" fill="#7C4DFF" />
          <path d="M28 32 L34 14 L40 30 Z" fill="#5B21B6" />
          <path d="M72 32 L66 14 L60 30 Z" fill="#5B21B6" />
          <circle cx="38" cy="56" r="9" fill="white" />
          <circle cx="62" cy="56" r="9" fill="white" />
          <circle cx="39" cy="57" r="4.5" fill="#1F1147" />
          <circle cx="63" cy="57" r="4.5" fill="#1F1147" />
          {mood === "happy" ? (
            <path d="M38 74 Q50 84 62 74" stroke="#1F1147" strokeWidth="3" fill="none" strokeLinecap="round" />
          ) : (
            <ellipse cx="50" cy="76" rx="7" ry="5" fill="#1F1147" />
          )}
          <circle cx="30" cy="70" r="4" fill="#B794F6" opacity="0.7" />
          <circle cx="70" cy="70" r="4" fill="#B794F6" opacity="0.7" />
        </svg>
      );
    }

    /* ---------------------------------------------------------------
       HELPERS & CONSTANTS
    ---------------------------------------------------------------- */
    function readFileAsDataURL(file) {
      return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.onload = () => resolve(reader.result);
        reader.onerror = reject;
        reader.readAsDataURL(file);
      });
    }

    const COVER_PALETTE = [
      ["#3B1F6B", "#0F0620"], ["#1E3A5F", "#0A1526"], ["#4B1E2F", "#1A0A10"],
      ["#1F4B3F", "#0A1A14"], ["#5B3A1E", "#1A0F06"], ["#2A1F5B", "#0A0620"],
    ];

    const CONSULT_STATUS = {
      urgent: { label: "Urgent", tone: "red" },
      revisi: { label: "Revisi", tone: "orange" },
      selesai: { label: "Selesai", tone: "green" },
      info: { label: "Info", tone: "gray" },
    };
    const CONSULT_CYCLE = ["urgent", "revisi", "selesai", "info"];

    const NAV_ITEMS = [
      { key: "beranda", labelKey: "nav_beranda", icon: Home },
      { key: "novelku", labelKey: "nav_novelku", icon: BookOpen },
      { key: "chapters", labelKey: "nav_chapters", icon: FileText },
      { key: "planner", labelKey: "nav_planner", icon: MapIcon },
      { key: "characters", labelKey: "nav_characters", icon: Users },
      { key: "consult", labelKey: "nav_consult", icon: MessageSquare },
      { key: "ideas", labelKey: "nav_ideas", icon: Lightbulb },
      { key: "progress", labelKey: "nav_progress", icon: BarChart2 },
      { key: "settings", labelKey: "nav_settings", icon: Settings },
    ];

    const WORKSPACE_SECTIONS = [
      { key: "overview", label: "Overview", icon: BookOpen },
      { key: "chapter", label: "Chapter", icon: FileText },
      { key: "planner", label: "Story Planner", icon: MapIcon },
      { key: "characters", label: "Character Database", icon: Users },
      { key: "ideas", label: "Ide & Notes", icon: Lightbulb },
      { key: "consult", label: "Catatan Konsultasi", icon: MessageSquare },
      { key: "progress", label: "Writing Progress", icon: BarChart2 },
      { key: "settings", label: "Pengaturan Novel", icon: Settings },
    ];

    const LOCAL_STORAGE_KEY = "novel_consult_app_data";

    /* ---------------------------------------------------------------
       UI COMPONENTS
    ---------------------------------------------------------------- */
    function Card({ children, className = "", style = {}, onClick }) {
      return (
        <div className={className} onClick={onClick} style={{
          background: "#fff", borderRadius: 18, border: "1px solid #ECE8F8",
          boxShadow: "0 1px 3px rgba(31,17,71,0.04)", ...style,
        }}>
          {children}
        </div>
      );
    }

    function ProgressBar({ value, color = "#7C4DFF", trackColor = "#EDE9FB", height = 8 }) {
      return (
        <div style={{ width: "100%", height, borderRadius: 99, background: trackColor, overflow: "hidden" }}>
          <div style={{ width: `${Math.min(100, Math.max(0, value || 0))}%`, height: "100%", borderRadius: 99, background: color, transition: "width 0.4s ease" }} />
        </div>
      );
    }

    function Pill({ children, tone = "violet" }) {
      const tones = {
        violet: { bg: "#F1EBFF", color: "#6D28D9" }, green: { bg: "#E9F9EC", color: "#1F9D4A" },
        orange: { bg: "#FFF3E0", color: "#B7791F" }, gray: { bg: "#F1F1F5", color: "#6B7280" },
        red: { bg: "#FDECEC", color: "#DC2626" },
      };
      const t = tones[tone] || tones.violet;
      return <span style={{ background: t.bg, color: t.color, fontSize: 12, fontWeight: 600, padding: "4px 10px", borderRadius: 99, display: "inline-block" }}>{children}</span>;
    }

    function SectionHeader({ title, action, onAction }) {
      return (
        <div style={{ display: "flex", alignItems: "center", justifyContent: "space-between", marginBottom: 16 }}>
          <h3 style={{ fontFamily: "Poppins, sans-serif", fontWeight: 600, fontSize: 16, color: "#1F1147", margin: 0 }}>{title}</h3>
          {action && <button onClick={onAction} style={{ background: "none", border: "none", color: "#7C4DFF", fontWeight: 600, fontSize: 13, cursor: "pointer" }}>{action}</button>}
        </div>
      );
    }

    function EmptyState({ text, action, onAction }) {
      return (
        <div style={{ display: "flex", flexDirection: "column", alignItems: "center", gap: 10, padding: "32px 12px", color: "#9691B0" }}>
          <Mascot size={56} mood="neutral" />
          <p style={{ margin: 0, fontSize: 13, textAlign: "center", maxWidth: 280 }}>{text}</p>
          {action && (
            <button onClick={onAction} style={{ marginTop: 4, background: "#5B21B6", color: "#fff", border: "none", borderRadius: 9, padding: "8px 16px", fontSize: 12.5, fontWeight: 600, cursor: "pointer" }}>
              {action}
            </button>
          )}
        </div>
      );
    }

    function PageTitle({ title, sub }) {
      return (
        <div style={{ marginBottom: 20 }}>
          <h2 style={{ fontFamily: "Poppins,sans-serif", fontSize: 22, margin: "0 0 4px", color: "#1F1147" }}>{title}</h2>
          <p style={{ margin: 0, fontSize: 13, color: "#9691B0" }}>{sub}</p>
        </div>
      );
    }

    function NovelCover({ novel, w = 110, h = 150 }) {
      if (novel.coverImage) {
        return (
          <div style={{ width: w, height: h, borderRadius: 12, flexShrink: 0, overflow: "hidden", boxShadow: "0 6px 16px rgba(31,17,71,0.25)" }}>
            <img src={novel.coverImage} alt={novel.title} style={{ width: "100%", height: "100%", objectFit: "cover" }} />
          </div>
        );
      }
      return (
        <div style={{
          width: w, height: h, borderRadius: 12, flexShrink: 0,
          background: `linear-gradient(160deg, ${novel.coverFrom}, ${novel.coverTo})`,
          display: "flex", alignItems: "center", justifyContent: "center", position: "relative", overflow: "hidden",
          boxShadow: "0 6px 16px rgba(31,17,71,0.25)",
        }}>
          <div style={{ position: "absolute", inset: 0, background: "radial-gradient(circle at 30% 20%, rgba(255,255,255,0.12), transparent 60%)" }} />
          <span style={{ fontFamily: "Poppins, sans-serif", fontWeight: 700, color: "#fff", fontSize: w < 90 ? 12 : 17, textAlign: "center", padding: "0 8px", letterSpacing: 1, textTransform: "uppercase" }}>
            {novel.title}
          </span>
        </div>
      );
    }

    function FilterTabs({ tabs, labels, active, onChange }) {
      return (
        <div style={{ display: "flex", gap: 8, flexWrap: "wrap" }}>
          {tabs.map(t => (
            <button key={t} onClick={() => onChange(t)} style={{
              border: active === t ? "none" : "1px solid #ECE8F8", borderRadius: 99, padding: "7px 15px", fontSize: 12.5, fontWeight: 600, cursor: "pointer",
              background: active === t ? "#5B21B6" : "#fff", color: active === t ? "#fff" : "#4B3A7A",
            }}>
              {labels ? labels[t] : t}
            </button>
          ))}
        </div>
      );
    }

    function NovelTabs({ novels, activeNovelId, setActiveNovelId }) {
      if (!novels.length) return null;
      return (
        <div style={{ display: "flex", gap: 8, flexWrap: "wrap" }}>
          {novels.map(n => (
            <button key={n.id} onClick={() => setActiveNovelId(n.id)} style={{
              border: activeNovelId === n.id ? "none" : "1px solid #ECE8F8", borderRadius: 99, padding: "8px 16px", fontSize: 12.5, fontWeight: 600, cursor: "pointer",
              background: activeNovelId === n.id ? "#5B21B6" : "#fff", color: activeNovelId === n.id ? "#fff" : "#4B3A7A",
            }}>
              {n.title}
            </button>
          ))}
        </div>
      );
    }

    function StatBig({ icon: Icon, color, label, value }) {
      return (
        <Card style={{ padding: 18 }}>
          <div style={{ width: 36, height: 36, borderRadius: 10, background: color + "22", display: "flex", alignItems: "center", justifyContent: "center", marginBottom: 10 }}>
            <Icon size={17} color={color} />
          </div>
          <div style={{ fontFamily: "Poppins,sans-serif", fontWeight: 700, fontSize: 20 }}>{value}</div>
          <div style={{ fontSize: 12, color: "#9691B0" }}>{label}</div>
        </Card>
      );
    }

    function DonutMini({ pct }) {
      const p = isFinite(pct) ? pct : 0;
      const radius = 33;
      const circumference = 2 * Math.PI * radius;
      const strokeDashoffset = circumference - (p / 100) * circumference;

      return (
        <div style={{ position: "relative", width: 80, height: 80, display: "flex", alignItems: "center", justifyContent: "center" }}>
          <svg width="80" height="80" viewBox="0 0 80 80">
            <circle cx="40" cy="40" r={radius} fill="none" stroke="#EDE9FB" strokeWidth="10" />
            <circle
              cx="40" cy="40" r={radius} fill="none" stroke="#7C4DFF" strokeWidth="10"
              strokeDasharray={circumference} strokeDashoffset={strokeDashoffset}
              strokeLinecap="round" transform="rotate(-90 40 40)" style={{ transition: "stroke-dashoffset 0.5s ease" }}
            />
          </svg>
          <div style={{ position: "absolute", fontFamily: "Poppins,sans-serif", fontWeight: 700, fontSize: 15 }}>{p}%</div>
        </div>
      );
    }

    function MiniCalendar({ month, setMonth }) {
      const daysInMonth = new Date(2026, month + 1, 0).getDate();
      const firstDay = (new Date(2026, month, 1).getDay() + 6) % 7;
      const today = 20;
      const cells = [];
      for (let i = 0; i < firstDay; i++) cells.push(null);
      for (let d = 1; d <= daysInMonth; d++) cells.push(d);
      return (
        <div>
          <div style={{ display: "flex", alignItems: "center", justifyContent: "space-between", marginBottom: 10 }}>
            <button onClick={() => setMonth(m => (m + 11) % 12)} style={{ background: "#F6F4FC", border: "none", borderRadius: 8, width: 26, height: 26, cursor: "pointer", display: "inline-flex", alignItems: "center", justifyContent: "center" }}><ChevronLeft size={13} /></button>
            <span style={{ fontSize: 12.5, fontWeight: 600 }}>{["Jan","Feb","Mar","Apr","Mei","Jun","Jul","Agu","Sep","Okt","Nov","Des"][month]} 2026</span>
            <button onClick={() => setMonth(m => (m + 1) % 12)} style={{ background: "#F6F4FC", border: "none", borderRadius: 8, width: 26, height: 26, cursor: "pointer", display: "inline-flex", alignItems: "center", justifyContent: "center" }}><ChevronRight size={13} /></button>
          </div>
          <div style={{ display: "grid", gridTemplateColumns: "repeat(7,1fr)", gap: 4, marginBottom: 6 }}>
            {["Min","Sen","Sel","Rab","Kam","Jum","Sab"].map(d => <div key={d} style={{ fontSize: 10, color: "#9691B0", textAlign: "center" }}>{d}</div>)}
          </div>
          <div style={{ display: "grid", gridTemplateColumns: "repeat(7,1fr)", gap: 4 }}>
            {cells.map((d, i) => {
              if (!d) return <div key={i} />;
              const isToday = month === 4 && d === today;
              return (
                <div key={i} style={{
                  width: "100%", aspectRatio: "1", display: "flex", alignItems: "center", justifyContent: "center", fontSize: 10.5, borderRadius: 7,
                  background: isToday ? "#5B21B6" : "transparent", color: isToday ? "#fff" : "#6B6485", fontWeight: isToday ? 700 : 400,
                }}>{d}</div>
              );
            })}
          </div>
        </div>
      );
    }

    function FieldRow({ label, value }) {
      return (
        <div>
          <div style={{ fontSize: 11, color: "#9691B0", marginBottom: 2 }}>{label}</div>
          <div style={{ color: "#3D3163" }}>{value}</div>
        </div>
      );
    }

    function ConsultCard({ c, novelTitle, onCycle }) {
      const dotColor = { urgent: "#EF4444", revisi: "#F59E0B", selesai: "#22C55E", info: "#3B82F6" };
      return (
        <Card style={{ padding: 18 }}>
          <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start" }}>
            <div style={{ display: "flex", gap: 10 }}>
              <div style={{ width: 9, height: 9, borderRadius: "50%", background: dotColor[c.status], marginTop: 5, flexShrink: 0 }} />
              <div>
                <div style={{ fontSize: 11.5, color: "#9691B0" }}>{novelTitle ? novelTitle + " • " : ""}Chapter {c.chapter} • {c.time}</div>
                <div style={{ fontWeight: 700, fontSize: 14.5, margin: "2px 0" }}>{c.title}</div>
                <div style={{ fontSize: 13, color: "#6B6485" }}>{c.note}</div>
              </div>
            </div>
            <Pill tone={CONSULT_STATUS[c.status].tone}>{CONSULT_STATUS[c.status].label}</Pill>
          </div>
          <button onClick={onCycle} style={{ marginTop: 12, background: "#F1EBFF", color: "#5B21B6", border: "none", borderRadius: 9, padding: "8px 14px", fontSize: 12.5, fontWeight: 600, cursor: "pointer" }}>
            Ubah Status →
          </button>
        </Card>
      );
    }

    function ImagePickerButton({ onPick, label, compact = false }) {
      const inputRef = useRef(null);
      return (
        <React.Fragment>
          <input
            ref={inputRef} type="file" accept="image/*" style={{ display: "none" }}
            onChange={async (e) => {
              const file = e.target.files?.[0];
              if (file) { const dataUrl = await readFileAsDataURL(file); onPick(dataUrl); }
              e.target.value = "";
            }}
          />
          {compact ? (
            <button onClick={() => inputRef.current?.click()} style={{
              position: "absolute", bottom: 0, right: 0, width: 28, height: 28, borderRadius: "50%",
              background: "#5B21B6", border: "2px solid #fff", color: "#fff", display: "flex",
              alignItems: "center", justifyContent: "center", cursor: "pointer",
            }} title={label}>
              <Camera size={13} />
            </button>
          ) : (
            <button onClick={() => inputRef.current?.click()} style={{
              background: "#F1EBFF", color: "#5B21B6", border: "none", borderRadius: 9,
              padding: "9px 14px", fontSize: 12.5, fontWeight: 600, cursor: "pointer",
              display: "flex", alignItems: "center", gap: 6,
            }}>
              <ImageIcon size={14} /> {label}
            </button>
          )}
        </React.Fragment>
      );
    }

    /* ---------------------------------------------------------------
       APP COMPONENT
    ---------------------------------------------------------------- */
    function App() {
      const [loaded, setLoaded] = useState(false);
      const [activeTab, setActiveTab] = useState("beranda");
      const [novels, setNovels] = useState([]);
      const [activeNovelId, setActiveNovelId] = useState(null);
      const [chapters, setChapters] = useState([]);
      const [characters, setCharacters] = useState([]);
      const [ideas, setIdeas] = useState([]);
      const [consultations, setConsultations] = useState([]);
      const [reminders, setReminders] = useState([]);
      const [plots, setPlots] = useState([]);
      const [profile, setProfile] = useState({ name: "Nazari", bio: "Penulis • Dreamer", photo: null });
      const [lang, setLang] = useState("id");
      const [showNotif, setShowNotif] = useState(false);
      const [search, setSearch] = useState("");
      const [workspace, setWorkspace] = useState({ novelId: null, section: "overview", editingChapterId: null });

      const t = useCallback((key) => (STRINGS[lang] && STRINGS[lang][key]) || STRINGS.id[key] || key, [lang]);

      useEffect(() => {
        try {
          const savedData = localStorage.getItem(LOCAL_STORAGE_KEY);
          if (savedData) {
            const data = JSON.parse(savedData);
            if (data.novels) setNovels(data.novels);
            if (data.chapters) setChapters(data.chapters);
            if (data.characters) setCharacters(data.characters);
            if (data.ideas) setIdeas(data.ideas);
            if (data.consultations) setConsultations(data.consultations);
            if (data.reminders) setReminders(data.reminders);
            if (data.plots) setPlots(data.plots);
            if (data.profile) setProfile(data.profile);
            if (data.lang) setLang(data.lang);
            if (data.activeNovelId) setActiveNovelId(data.activeNovelId);
          }
        } catch (e) {
          console.error("Gagal membaca LocalStorage", e);
        } finally {
          setLoaded(true);
        }
      }, []);

      useEffect(() => {
        if (!loaded) return;
        const id = setTimeout(() => {
          try {
            const payload = { novels, chapters, characters, ideas, consultations, reminders, plots, profile, lang, activeNovelId };
            localStorage.setItem(LOCAL_STORAGE_KEY, JSON.stringify(payload));
          } catch (e) {
            console.error("Gagal menyimpan ke LocalStorage", e);
          }
        }, 500);
        return () => clearTimeout(id);
      }, [novels, chapters, characters, ideas, consultations, reminders, plots, profile, lang, activeNovelId, loaded]);

      const activeNovel = novels.find(n => n.id === activeNovelId) || novels[0] || null;
      const totalWords = novels.reduce((s, n) => s + n.words, 0);
      const totalTarget = novels.reduce((s, n) => s + n.targetWords, 0) || 1;
      const overallPct = novels.length ? Math.round((totalWords / totalTarget) * 100) : 0;

      function openWorkspace(novelId, section = "overview") {
        setActiveNovelId(novelId);
        setWorkspace({ novelId, section, editingChapterId: null });
        setActiveTab("workspace");
      }

      function addNovel(title, genre, coverImage) {
        const id = "n_" + Date.now();
        const [from, to] = COVER_PALETTE[novels.length % COVER_PALETTE.length];
        setNovels([...novels, {
          id, title, genre: genre || "Genre Baru", coverFrom: from, coverTo: to, coverImage: coverImage || null,
          chapters: 0, totalChapters: 20, words: 0, targetWords: 60000,
          nextTarget: "Mulai Chapter 1", nextNote: "Tentukan pembukaan cerita.",
        }]);
        setActiveNovelId(id);
        return id;
      }

      function addChapter(novelId, title) {
        const novelChaps = chapters.filter(c => c.novelId === novelId);
        const nextNum = novelChaps.length ? Math.max(...novelChaps.map(c => c.number)) + 1 : 1;
        setChapters([{ id: "chap_" + Date.now(), novelId, number: nextNum, title: title || `Chapter ${nextNum}`, words: 0, status: "draft", target: 2000, content: "" }, ...chapters]);
        setNovels(novels.map(n => n.id === novelId ? { ...n, chapters: n.chapters + 1 } : n));
      }

      function markChapterDone(id) {
        setChapters(chapters.map(c => c.id === id ? { ...c, status: c.status === "done" ? "draft" : "done" } : c));
      }

      function saveChapterContent(chapterId, content) {
        const words = content.trim() ? content.trim().split(/\s+/).length : 0;
        const chapter = chapters.find(c => c.id === chapterId);
        if (!chapter) return;
        const diff = words - chapter.words;
        setChapters(chapters.map(c => c.id === chapterId ? { ...c, content, words } : c));
        setNovels(novels.map(n => n.id === chapter.novelId ? { ...n, words: Math.max(0, n.words + diff) } : n));
      }

      function addCharacter(novelId, name, role, desc) {
        setCharacters([...characters, { id: "char_" + Date.now(), novelId, name, role: role || "Karakter Pendukung", desc: desc || "" }]);
      }

      function addIdea(category, title, desc, novelId) {
        setIdeas([{ id: "idea_" + Date.now(), novelId, category, title, desc, time: "Baru saja" }, ...ideas]);
      }

      function addPlot(novelId, type, text, act) {
        setPlots([...plots, { id: "plot_" + Date.now(), novelId, type, act: act || "Act 1", text }]);
      }

      function addReminder(text, deadline) {
        setReminders([...reminders, { id: "rem_" + Date.now(), text, deadline: deadline || "-", done: false }]);
      }

      function toggleReminder(id) {
        setReminders(reminders.map(r => r.id === id ? { ...r, done: !r.done } : r));
      }

      function cycleConsultStatus(id) {
        setConsultations(consultations.map(c => {
          if (c.id !== id) return c;
          const idx = CONSULT_CYCLE.indexOf(c.status);
          return { ...c, status: CONSULT_CYCLE[(idx + 1) % CONSULT_CYCLE.length] };
        }));
      }

      function updateNovel(novelId, patch) {
        setNovels(novels.map(n => n.id === novelId ? { ...n, ...patch } : n));
      }

      if (!loaded) {
        return (
          <div style={{ minHeight: "100vh", display: "flex", alignItems: "center", justifyContent: "center", background: "#F6F4FC" }}>
            <div style={{ display: "flex", flexDirection: "column", alignItems: "center", gap: 12 }}>
              <Mascot size={64} />
              <div style={{ color: "#7C4DFF", fontWeight: 600, fontSize: 13 }}>{STRINGS.id.memuat}</div>
            </div>
          </div>
        );
      }

      return (
        <div style={{ display: "flex", minHeight: "100vh", background: "#F6F4FC", color: "#1F1147" }}>
          <Sidebar activeTab={activeTab} setActiveTab={setActiveTab} t={t} profile={profile} />

          <div style={{ flex: 1, display: "flex", flexDirection: "column", minWidth: 0 }}>
            <TopBar
              search={search} setSearch={setSearch} t={t} profile={profile}
              reminders={reminders} showNotif={showNotif} setShowNotif={setShowNotif}
              toggleReminder={toggleReminder} addReminder={addReminder} setActiveTab={setActiveTab}
            />

            <div style={{ padding: "24px 28px 60px", flex: 1, overflowY: "auto" }}>
              {activeTab === "beranda" && (
                <Beranda
                  novels={novels} activeNovel={activeNovel} totalWords={totalWords} totalTarget={totalTarget}
                  overallPct={overallPct} openWorkspace={openWorkspace} setActiveTab={setActiveTab} t={t} profile={profile}
                />
              )}
              {activeTab === "novelku" && (
                <NovelkuPage novels={novels} openWorkspace={openWorkspace} addNovel={addNovel} t={t} />
              )}
              {activeTab === "workspace" && workspace.novelId && (
                <WorkspaceNovel
                  novel={novels.find(n => n.id === workspace.novelId)} novels={novels} setNovels={setNovels}
                  workspace={workspace} setWorkspace={setWorkspace} chapters={chapters} addChapter={addChapter}
                  markChapterDone={markChapterDone} saveChapterContent={saveChapterContent} characters={characters}
                  addCharacter={addCharacter} plots={plots} addPlot={addPlot} ideas={ideas} addIdea={addIdea}
                  consultations={consultations} cycleConsultStatus={cycleConsultStatus} setActiveTab={setActiveTab}
                  updateNovel={updateNovel}
                />
              )}
              {activeTab === "chapters" && (
                <ChapterManagerPage novels={novels} activeNovelId={activeNovelId} setActiveNovelId={setActiveNovelId}
                  chapters={chapters} addChapter={addChapter} markChapterDone={markChapterDone} openWorkspace={openWorkspace} t={t} />
              )}
              {activeTab === "planner" && (
                <StoryPlannerPage novels={novels} activeNovelId={activeNovelId} setActiveNovelId={setActiveNovelId} plots={plots} addPlot={addPlot} t={t} />
              )}
              {activeTab === "characters" && (
                <CharacterPage novels={novels} activeNovelId={activeNovelId} setActiveNovelId={setActiveNovelId} characters={characters} addCharacter={addCharacter} t={t} />
              )}
              {activeTab === "consult" && (
                <ConsultPage novels={novels} consultations={consultations} cycleConsultStatus={cycleConsultStatus} t={t} />
              )}
              {activeTab === "ideas" && (
                <IdeaVaultPage ideas={ideas} addIdea={addIdea} novels={novels} t={t} />
              )}
              {activeTab === "progress" && (
                <ProgressPage novels={novels} chapters={chapters} t={t} />
              )}
              {activeTab === "settings" && (
                <SettingsPage profile={profile} setProfile={setProfile} lang={lang} setLang={setLang} t={t} />
              )}
            </div>
          </div>
        </div>
      );
    }

    /* ---------------------------------------------------------------
       SIDEBAR
    ---------------------------------------------------------------- */
    function Sidebar({ activeTab, setActiveTab, t, profile }) {
      return (
        <div style={{ width: 250, background: "linear-gradient(180deg,#2A1B5C,#1B1140)", flexShrink: 0, display: "flex", flexDirection: "column", padding: "24px 16px", color: "#fff" }}>
          <div style={{ display: "flex", alignItems: "center", gap: 10, padding: "0 8px 4px" }}>
            <div style={{ width: 36, height: 36, borderRadius: 10, background: "rgba(255,255,255,0.1)", display: "flex", alignItems: "center", justifyContent: "center", fontFamily: "Poppins,sans-serif", fontWeight: 700 }}>N</div>
            <div style={{ fontFamily: "Poppins,sans-serif", fontWeight: 700, fontSize: 15, lineHeight: 1.1 }}>NOVEL<br />CONSULT</div>
          </div>
          <div style={{ fontSize: 11, color: "#A99CD9", padding: "10px 8px 20px" }}>{t("tagline")}</div>

          <div style={{ display: "flex", flexDirection: "column", gap: 4 }}>
            {NAV_ITEMS.map(item => {
              const Icon = item.icon;
              const active = activeTab === item.key || (activeTab === "workspace" && item.key === "novelku");
              return (
                <button key={item.key} className="nc-navbtn" onClick={() => setActiveTab(item.key)} style={{
                  display: "flex", alignItems: "center", gap: 10, padding: "10px 12px", borderRadius: 10, border: "none",
                  cursor: "pointer", textAlign: "left", background: active ? "#fff" : "transparent",
                  color: active ? "#5B21B6" : "#D7CFEF", fontWeight: active ? 600 : 500, fontSize: 13.5,
                }}>
                  <Icon size={17} /> {t(item.labelKey)}
                </button>
              );
            })}
          </div>

          <div style={{ marginTop: "auto", paddingTop: 20 }}>
            <div style={{ background: "#4ADE80", color: "#0B3B1E", fontSize: 12, fontWeight: 600, padding: "8px 12px", borderRadius: 14, borderBottomLeftRadius: 4, marginBottom: 10, display: "inline-block" }}>
              {t("mascotBubble")}
            </div>
            <div style={{ display: "flex", justifyContent: "center", padding: "8px 0 4px" }}>
              <Mascot size={100} />
            </div>
            <div style={{ display: "flex", alignItems: "center", gap: 10, background: "rgba(255,255,255,0.06)", borderRadius: 12, padding: 10, marginTop: 8 }}>
              <div style={{ width: 34, height: 34, borderRadius: "50%", overflow: "hidden", background: "#7C4DFF", display: "flex", alignItems: "center", justifyContent: "center", fontWeight: 700, fontSize: 13, flexShrink: 0 }}>
                {profile.photo ? <img src={profile.photo} alt="" style={{ width: "100%", height: "100%", objectFit: "cover" }} /> : profile.name.charAt(0)}
              </div>
              <div style={{ flex: 1, minWidth: 0 }}>
                <div style={{ fontSize: 13, fontWeight: 600, overflow: "hidden", textOverflow: "ellipsis", whiteSpace: "nowrap" }}>{profile.name}</div>
                <div style={{ fontSize: 11, color: "#A99CD9", overflow: "hidden", textOverflow: "ellipsis", whiteSpace: "nowrap" }}>{profile.bio}</div>
              </div>
              <ChevronDown size={14} color="#A99CD9" />
            </div>
            <button onClick={() => setActiveTab("settings")} style={{
              width: "100%", marginTop: 10, padding: "9px 0", borderRadius: 10, border: "1px solid rgba(255,255,255,0.15)",
              background: "transparent", color: "#fff", fontSize: 12.5, fontWeight: 600, cursor: "pointer",
            }}>
              {t("lihatProfil")}
            </button>
          </div>
        </div>
      );
    }

    /* ---------------------------------------------------------------
       TOP BAR
    ---------------------------------------------------------------- */
    function TopBar({ search, setSearch, t, profile, reminders, showNotif, setShowNotif, toggleReminder, addReminder, setActiveTab }) {
      const pending = reminders.filter(r => !r.done).length;
      const [newText, setNewText] = useState("");
      return (
        <div style={{ display: "flex", alignItems: "center", justifyContent: "space-between", padding: "18px 28px", background: "#F6F4FC", position: "sticky", top: 0, zIndex: 20 }}>
          <div style={{ display: "flex", alignItems: "center", gap: 8, background: "#fff", borderRadius: 12, padding: "10px 14px", width: 340, border: "1px solid #ECE8F8" }}>
            <Search size={16} color="#9691B0" />
            <input value={search} onChange={e => setSearch(e.target.value)} placeholder={t("searchPlaceholder")} style={{ border: "none", background: "transparent", fontSize: 13.5, width: "100%", color: "#1F1147" }} />
          </div>

          <div style={{ display: "flex", alignItems: "center", gap: 16, position: "relative" }}>
            <button onClick={() => setShowNotif(!showNotif)} style={{
              position: "relative", background: "#fff", border: "1px solid #ECE8F8", width: 40, height: 40, borderRadius: 12,
              cursor: "pointer", display: "flex", alignItems: "center", justifyContent: "center",
            }}>
              <Bell size={17} color="#4B3A7A" />
              {pending > 0 && <span style={{ position: "absolute", top: -4, right: -4, background: "#EF4444", color: "#fff", fontSize: 10, fontWeight: 700, borderRadius: 99, width: 17, height: 17, display: "flex", alignItems: "center", justifyContent: "center" }}>{pending}</span>}
            </button>
            {showNotif && (
              <Card style={{ position: "absolute", top: 48, right: 90, width: 280, padding: 14, zIndex: 30 }}>
                <div style={{ fontWeight: 700, fontSize: 13.5, marginBottom: 10 }}>{t("pengingat")}</div>
                <div style={{ display: "flex", flexDirection: "column", gap: 8, maxHeight: 220, overflowY: "auto", marginBottom: 10 }}>
                  {reminders.length === 0 && <div style={{ fontSize: 12, color: "#9691B0" }}>{t("pengingatKosong")}</div>}
                  {reminders.map(r => (
                    <div key={r.id} onClick={() => toggleReminder(r.id)} style={{ display: "flex", alignItems: "flex-start", gap: 8, cursor: "pointer", padding: 6, borderRadius: 8 }}>
                      <div style={{ width: 16, height: 16, borderRadius: 5, border: "2px solid #7C4DFF", marginTop: 2, background: r.done ? "#7C4DFF" : "transparent", flexShrink: 0, display: "flex", alignItems: "center", justifyContent: "center" }}>
                        {r.done && <Check size={11} color="#fff" />}
                      </div>
                      <div>
                        <div style={{ fontSize: 12.5, fontWeight: 600, textDecoration: r.done ? "line-through" : "none", color: r.done ? "#9691B0" : "#1F1147" }}>{r.text}</div>
                        <div style={{ fontSize: 11, color: "#9691B0" }}>{r.deadline}</div>
                      </div>
                    </div>
                  ))}
                </div>
                <div style={{ display: "flex", gap: 6 }}>
                  <input value={newText} onChange={e => setNewText(e.target.value)} placeholder={t("pengingatBaru")} style={{ flex: 1, border: "1px solid #ECE8F8", borderRadius: 8, padding: "7px 9px", fontSize: 12 }}
                    onKeyDown={e => { if (e.key === "Enter" && newText.trim()) { addReminder(newText.trim(), ""); setNewText(""); } }} />
                  <button onClick={() => { if (newText.trim()) { addReminder(newText.trim(), ""); setNewText(""); } }} style={{ background: "#5B21B6", color: "#fff", border: "none", borderRadius: 8, padding: "0 10px", cursor: "pointer", display: "inline-flex", alignItems: "center", justifyContent: "center" }}><Plus size={13} /></button>
                </div>
              </Card>
            )}
            <div onClick={() => setActiveTab("settings")} style={{ width: 40, height: 40, borderRadius: "50%", overflow: "hidden", background: "#7C4DFF", display: "flex", alignItems: "center", justifyContent: "center", color: "#fff", fontWeight: 700, cursor: "pointer" }}>
              {profile.photo ? <img src={profile.photo} alt="" style={{ width: "100%", height: "100%", objectFit: "cover" }} /> : <Mascot size={30} />}
            </div>
          </div>
        </div>
      );
    }

    /* ---------------------------------------------------------------
       BERANDA
    ---------------------------------------------------------------- */
    function Beranda({ novels, activeNovel, totalWords, totalTarget, overallPct, openWorkspace, setActiveTab, t, profile }) {
      const chapterPct = activeNovel ? Math.round((activeNovel.chapters / activeNovel.totalChapters) * 100) : 0;
      const wordPct = activeNovel ? Math.round((activeNovel.words / activeNovel.targetWords) * 100) : 0;

      const quickAccessItems = [
        { action: () => (activeNovel ? openWorkspace(activeNovel.id, "chapter") : setActiveTab("novelku")), icon: Pencil, title: t("qa_tulis"), sub: t("qa_tulis_sub"), color: "#7C4DFF" },
        { action: () => setActiveTab("novelku"), icon: BookOpen, title: t("qa_novelku"), sub: t("qa_novelku_sub"), color: "#3B82F6" },
        { action: () => (activeNovel ? openWorkspace(activeNovel.id, "planner") : setActiveTab("planner")), icon: MapIcon, title: t("qa_planner"), sub: t("qa_planner_sub"), color: "#3B82F6" },
        { action: () => (activeNovel ? openWorkspace(activeNovel.id, "characters") : setActiveTab("characters")), icon: Users, title: t("qa_char"), sub: t("qa_char_sub"), color: "#7C4DFF" },
        { action: () => setActiveTab("consult"), icon: MessageSquare, title: t("qa_consult"), sub: t("qa_consult_sub"), color: "#22C55E" },
        { action: () => setActiveTab("ideas"), icon: Lightbulb, title: t("qa_ideas"), sub: t("qa_ideas_sub"), color: "#F59E0B" },
        { action: () => setActiveTab("progress"), icon: BarChart2, title: t("qa_progress"), sub: t("qa_progress_sub"), color: "#3B82F6" },
        { action: () => setActiveTab("settings"), icon: Settings, title: t("qa_settings"), sub: t("qa_settings_sub"), color: "#9691B0" },
      ];

      return (
        <div style={{ display: "flex", flexDirection: "column", gap: 20, maxWidth: 980 }}>
          <Card style={{ padding: 28, background: "linear-gradient(120deg,#EDE7FB,#F6F4FC)", position: "relative", overflow: "hidden" }}>
            <div style={{ maxWidth: 380, position: "relative", zIndex: 2 }}>
              <h2 style={{ fontFamily: "Poppins,sans-serif", fontSize: 26, margin: "0 0 6px", color: "#1F1147" }}>{t("halo")}, {profile.name}! 👋</h2>
              <p style={{ margin: "0 0 16px", color: "#5B4E7D", fontSize: 14 }}>{t("siapMenulis")}</p>
              <div style={{ background: "#fff", borderRadius: 14, padding: "12px 16px", fontSize: 13, color: "#4B3A7A", boxShadow: "0 4px 14px rgba(31,17,71,0.08)" }}>
                "{t("quote")}" 💜
              </div>
            </div>
            <div style={{ position: "absolute", right: 20, bottom: -10 }}><Mascot size={140} /></div>
          </Card>

          <Card style={{ padding: 22 }}>
            <SectionHeader title={t("ringkasanHariIni")} />
            <div style={{ display: "grid", gridTemplateColumns: "repeat(4,1fr)", gap: 12 }}>
              <StatBig icon={Pencil} color="#7C4DFF" label={t("kataDitulis")} value={activeNovel ? "0" : "-"} />
              <StatBig icon={Clock} color="#3B82F6" label={t("menitFokus")} value="0" />
              <StatBig icon={Target} color="#22C55E" label={t("chapterBulanIni")} value={activeNovel ? `${activeNovel.chapters}/${activeNovel.totalChapters}` : "-"} />
              <StatBig icon={Star} color="#F59E0B" label={t("targetBulanIni")} value={`${overallPct}%`} />
            </div>
          </Card>

          <Card style={{ padding: 22 }}>
            <SectionHeader title={t("novelAktif")} />
            {activeNovel ? (
              <div style={{ display: "flex", gap: 18, alignItems: "center" }}>
                <NovelCover novel={activeNovel} w={80} h={108} />
                <div style={{ flex: 1, minWidth: 0 }}>
                  <div style={{ fontFamily: "Poppins,sans-serif", fontWeight: 700, fontSize: 17 }}>{activeNovel.title}</div>
                  <div style={{ fontSize: 12.5, color: "#9691B0", marginBottom: 10 }}>{activeNovel.genre}</div>
                  <div style={{ display: "flex", alignItems: "center", gap: 10 }}>
                    <div style={{ flex: 1 }}><ProgressBar value={wordPct} /></div>
                    <span style={{ fontSize: 12.5, fontWeight: 700, color: "#7C4DFF" }}>{wordPct}%</span>
                  </div>
                  <div style={{ fontSize: 11.5, color: "#9691B0", marginTop: 6 }}>{activeNovel.chapters} / {activeNovel.totalChapters} Chapter • {chapterPct}%</div>
                </div>
                <button onClick={() => openWorkspace(activeNovel.id, "chapter")} style={{
                  background: "#5B21B6", color: "#fff", border: "none", borderRadius: 10, padding: "10px 18px",
                  fontWeight: 600, fontSize: 13, cursor: "pointer", display: "flex", alignItems: "center", gap: 6, flexShrink: 0,
                }}>
                  {t("lanjutMenulis")} <ArrowRight size={14} />
                </button>
              </div>
            ) : (
              <EmptyState text={t("mulaiNovelPertama")} action={t("novelBaru")} onAction={() => setActiveTab("novelku")} />
            )}
          </Card>

          <Card style={{ padding: 22 }}>
            <SectionHeader title={t("quickAccess")} />
            <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr 1fr 1fr", gap: 12 }}>
              {quickAccessItems.map((item, i) => {
                const Icon = item.icon;
                return (
                  <div key={i} className="nc-clickable" onClick={item.action} style={{
                    display: "flex", alignItems: "center", gap: 10, border: "1px solid #ECE8F8", borderRadius: 12, padding: "12px 14px",
                  }}>
                    <div style={{ width: 34, height: 34, borderRadius: 9, background: item.color + "22", display: "flex", alignItems: "center", justifyContent: "center", flexShrink: 0 }}>
                      <Icon size={16} color={item.color} />
                    </div>
                    <div style={{ minWidth: 0 }}>
                      <div style={{ fontWeight: 600, fontSize: 12.5, whiteSpace: "nowrap", overflow: "hidden", textOverflow: "ellipsis" }}>{item.title}</div>
                      <div style={{ fontSize: 10.5, color: "#9691B0", whiteSpace: "nowrap", overflow: "hidden", textOverflow: "ellipsis" }}>{item.sub}</div>
                    </div>
                  </div>
                );
              })}
            </div>
          </Card>
        </div>
      );
    }

    /* ---------------------------------------------------------------
       NOVELKU PAGE
    ---------------------------------------------------------------- */
    function NovelkuPage({ novels, openWorkspace, addNovel, t }) {
      const [title, setTitle] = useState("");
      const [genre, setGenre] = useState("");
      const [coverImage, setCoverImage] = useState(null);

      function handleCreate() {
        if (!title.trim()) return;
        addNovel(title.trim(), genre.trim(), coverImage);
        setTitle(""); setGenre(""); setCoverImage(null);
      }

      return (
        <div>
          <PageTitle title={t("novelkuTitle")} sub={t("novelkuSub")} />
          <div style={{ display: "grid", gridTemplateColumns: "repeat(3,1fr)", gap: 20 }}>
            {novels.map(n => {
              const pct = Math.round((n.chapters / n.totalChapters) * 100);
              const wpct = Math.round((n.words / n.targetWords) * 100);
              return (
                <Card key={n.id} className="nc-clickable" style={{ padding: 18 }} onClick={() => openWorkspace(n.id, "overview")}>
                  <div style={{ display: "flex", gap: 14 }}>
                    <NovelCover novel={n} w={80} h={110} />
                    <div style={{ flex: 1, minWidth: 0 }}>
                      <div style={{ fontFamily: "Poppins,sans-serif", fontWeight: 700, fontSize: 15 }}>{n.title}</div>
                      <div style={{ fontSize: 11.5, color: "#9691B0", marginBottom: 8 }}>{n.genre}</div>
                      <div style={{ fontSize: 11.5, color: "#4B3A7A", marginBottom: 4 }}>{n.chapters}/{n.totalChapters} Chapter</div>
                      <ProgressBar value={pct} height={6} />
                      <div style={{ fontSize: 11, color: "#9691B0", marginTop: 8 }}>{n.words.toLocaleString("id-ID")} / {n.targetWords.toLocaleString("id-ID")} kata ({wpct}%)</div>
                    </div>
                  </div>
                  <button onClick={(e) => { e.stopPropagation(); openWorkspace(n.id, "chapter"); }} style={{
                    marginTop: 14, width: "100%", background: "#5B21B6", color: "#fff", border: "none", borderRadius: 9, padding: "8px 0", fontWeight: 600, fontSize: 12.5, cursor: "pointer",
                  }}>
                    {t("bukaChapterManager")}
                  </button>
                </Card>
              );
            })}

            <Card style={{ padding: 18, display: "flex", flexDirection: "column", justifyContent: "center", gap: 10, border: "2px dashed #D9D2F0", background: "transparent" }}>
              <div style={{ fontWeight: 700, fontSize: 13.5, textAlign: "center" }}>{t("tambahNovelBaru")}</div>

              <div style={{ position: "relative", alignSelf: "center" }}>
                <div style={{
                  width: 96, height: 130, borderRadius: 10, background: coverImage ? "transparent" : "#F1EBFF",
                  display: "flex", alignItems: "center", justifyContent: "center", overflow: "hidden", border: "1px solid #ECE8F8",
                }}>
                  {coverImage ? <img src={coverImage} alt="" style={{ width: "100%", height: "100%", objectFit: "cover" }} /> : <ImageIcon size={22} color="#B7A6E8" />}
                </div>
                <ImagePickerButton onPick={setCoverImage} label={t("pilihCoverGaleri")} compact />
              </div>
              <div style={{ textAlign: "center", fontSize: 11, color: "#9691B0" }}>{t("pilihCoverGaleri")}</div>

              <input value={title} onChange={e => setTitle(e.target.value)} placeholder={t("judulNovel")} style={{ border: "1px solid #ECE8F8", borderRadius: 8, padding: "8px 10px", fontSize: 12.5 }} />
              <input value={genre} onChange={e => setGenre(e.target.value)} placeholder={t("genreNovel")} style={{ border: "1px solid #ECE8F8", borderRadius: 8, padding: "8px 10px", fontSize: 12.5 }} />
              <button onClick={handleCreate} style={{ background: "#22C55E", color: "#fff", border: "none", borderRadius: 9, padding: "9px 0", fontWeight: 600, fontSize: 12.5, cursor: "pointer", display: "flex", alignItems: "center", justifyContent: "center", gap: 6 }}>
                <Plus size={14} /> {t("buatNovel")}
              </button>
            </Card>
          </div>
          {novels.length === 0 && (
            <div style={{ marginTop: 16 }}><EmptyState text={t("belumAdaNovelSama")} /></div>
          )}
        </div>
      );
    }

    /* ---------------------------------------------------------------
       OTHER GLOBAL PAGES
    ---------------------------------------------------------------- */
    function ChapterManagerPage({ novels, activeNovelId, setActiveNovelId, chapters, addChapter, markChapterDone, openWorkspace, t }) {
      const [newTitle, setNewTitle] = useState("");
      if (!novels.length) return (<div><PageTitle title={t("nav_chapters")} sub={t("pilihNovelDulu")} /><EmptyState text={t("belumAdaNovelSama")} /></div>);
      const activeId = activeNovelId || novels[0].id;
      const novelChapters = chapters.filter(c => c.novelId === activeId).sort((a, b) => b.number - a.number);
      const statusTone = { draft: "gray", review: "orange", done: "green" };
      const statusLabel = { draft: "Draft", review: "Review", done: "Selesai" };

      return (
        <div>
          <PageTitle title={t("nav_chapters")} sub={t("progressTitle")} />
          <NovelTabs novels={novels} activeNovelId={activeId} setActiveNovelId={setActiveNovelId} />
          <Card style={{ padding: 20, marginTop: 16 }}>
            <div style={{ display: "flex", gap: 8, marginBottom: 18 }}>
              <input value={newTitle} onChange={e => setNewTitle(e.target.value)} placeholder="Judul chapter baru..." style={{ flex: 1, border: "1px solid #ECE8F8", borderRadius: 9, padding: "10px 12px", fontSize: 13 }} />
              <button onClick={() => { addChapter(activeId, newTitle.trim()); setNewTitle(""); }} style={{ background: "#5B21B6", color: "#fff", border: "none", borderRadius: 9, padding: "0 16px", fontWeight: 600, fontSize: 13, cursor: "pointer", display: "flex", alignItems: "center", gap: 6 }}>
                <Plus size={15} /> Tambah Chapter
              </button>
            </div>
            {novelChapters.length === 0 ? <EmptyState text="Belum ada chapter untuk novel ini." /> : (
              <div style={{ display: "flex", flexDirection: "column", gap: 10 }}>
                {novelChapters.map(c => (
                  <div key={c.id} style={{ display: "flex", alignItems: "center", gap: 14, border: "1px solid #ECE8F8", borderRadius: 12, padding: "12px 16px" }}>
                    <div style={{ width: 34, height: 34, borderRadius: 9, background: "#F1EBFF", display: "flex", alignItems: "center", justifyContent: "center", fontWeight: 700, fontSize: 12.5, color: "#5B21B6", flexShrink: 0 }}>{c.number}</div>
                    <div style={{ flex: 1, minWidth: 0 }}>
                      <div style={{ fontWeight: 600, fontSize: 13.5 }}>{c.title}</div>
                      <div style={{ fontSize: 11.5, color: "#9691B0" }}>{c.words.toLocaleString("id-ID")} kata</div>
                    </div>
                    <Pill tone={statusTone[c.status]}>{statusLabel[c.status]}</Pill>
                    <button onClick={() => openWorkspace(activeId, "chapter")} style={{ background: "#F1EBFF", color: "#5B21B6", border: "none", borderRadius: 8, padding: "7px 12px", fontSize: 12, fontWeight: 600, cursor: "pointer" }}>Tulis</button>
                    <button onClick={() => markChapterDone(c.id)} style={{
                      background: c.status === "done" ? "#F1EBFF" : "#22C55E", color: c.status === "done" ? "#5B21B6" : "#fff",
                      border: "none", borderRadius: 8, padding: "7px 12px", fontSize: 12, fontWeight: 600, cursor: "pointer",
                    }}>
                      {c.status === "done" ? "Tandai Draft" : "Tandai Selesai"}
                    </button>
                  </div>
                ))}
              </div>
            )}
          </Card>
        </div>
      );
    }

    function StoryPlannerPage({ novels, activeNovelId, setActiveNovelId, plots, addPlot, t }) {
      const [type, setType] = useState("Plot");
      const [text, setText] = useState("");
      if (!novels.length) return (<div><PageTitle title={t("plannerTitle")} sub={t("pilihNovelDulu")} /><EmptyState text={t("belumAdaNovelSama")} /></div>);
      const activeId = activeNovelId || novels[0].id;
      const novelPlots = plots.filter(p => p.novelId === activeId);
      const typeColor = { Plot: "#3B82F6", Konflik: "#EF4444", Motif: "#8B5CF6" };

      return (
        <div>
          <PageTitle title={t("plannerTitle")} sub={t("plannerSub")} />
          <NovelTabs novels={novels} activeNovelId={activeId} setActiveNovelId={setActiveNovelId} />
          <Card style={{ padding: 20, marginTop: 16 }}>
            <div style={{ display: "flex", gap: 8, marginBottom: 18 }}>
              <select value={type} onChange={e => setType(e.target.value)} style={{ border: "1px solid #ECE8F8", borderRadius: 9, padding: "10px 12px", fontSize: 13 }}>
                <option>Plot</option><option>Konflik</option><option>Motif</option>
              </select>
              <input value={text} onChange={e => setText(e.target.value)} placeholder="Tulis poin alur/konflik/motif..." style={{ flex: 1, border: "1px solid #ECE8F8", borderRadius: 9, padding: "10px 12px", fontSize: 13 }} />
              <button onClick={() => { if (text.trim()) { addPlot(activeId, type, text.trim()); setText(""); } }} style={{ background: "#5B21B6", color: "#fff", border: "none", borderRadius: 9, padding: "0 16px", fontWeight: 600, fontSize: 13, cursor: "pointer", display: "flex", alignItems: "center", gap: 6 }}>
                <Plus size={15} /> Tambah
              </button>
            </div>
            {novelPlots.length === 0 ? <EmptyState text="Belum ada poin cerita. Tambahkan alur, konflik, atau motif." /> : (
              <div style={{ display: "flex", flexDirection: "column", gap: 10 }}>
                {novelPlots.map((p, i) => (
                  <div key={p.id} style={{ display: "flex", gap: 12, alignItems: "flex-start", borderLeft: `3px solid ${typeColor[p.type]}`, paddingLeft: 12 }}>
                    <div style={{ width: 22, height: 22, borderRadius: "50%", background: typeColor[p.type] + "22", color: typeColor[p.type], fontSize: 11, fontWeight: 700, display: "flex", alignItems: "center", justifyContent: "center", flexShrink: 0 }}>{i + 1}</div>
                    <div><Pill tone="violet">{p.type}</Pill><div style={{ fontSize: 13, marginTop: 4, color: "#3D3163" }}>{p.text}</div></div>
                  </div>
                ))}
              </div>
            )}
          </Card>
        </div>
      );
    }

    function CharacterPage({ novels, activeNovelId, setActiveNovelId, characters, addCharacter, t }) {
      const [name, setName] = useState("");
      const [role, setRole] = useState("");
      const [desc, setDesc] = useState("");
      if (!novels.length) return (<div><PageTitle title={t("charTitle")} sub={t("pilihNovelDulu")} /><EmptyState text={t("belumAdaNovelSama")} /></div>);
      const activeId = activeNovelId || novels[0].id;
      const list = characters.filter(c => c.novelId === activeId);

      return (
        <div>
          <PageTitle title={t("charTitle")} sub={t("charSub")} />
          <NovelTabs novels={novels} activeNovelId={activeId} setActiveNovelId={setActiveNovelId} />
          <div style={{ display: "grid", gridTemplateColumns: "repeat(3,1fr)", gap: 16, marginTop: 16 }}>
            {list.map(c => (
              <Card key={c.id} style={{ padding: 18 }}>
                <div style={{ width: 44, height: 44, borderRadius: "50%", background: "#7C4DFF", color: "#fff", display: "flex", alignItems: "center", justifyContent: "center", fontWeight: 700, fontFamily: "Poppins,sans-serif", marginBottom: 10 }}>{c.name.charAt(0)}</div>
                <div style={{ fontWeight: 700, fontSize: 14.5 }}>{c.name}</div>
                <Pill tone="violet">{c.role}</Pill>
                <div style={{ fontSize: 12.5, color: "#6B6485", marginTop: 8 }}>{c.desc}</div>
              </Card>
            ))}
            <Card style={{ padding: 18, border: "2px dashed #D9D2F0", background: "transparent" }}>
              <div style={{ fontWeight: 700, fontSize: 13.5, marginBottom: 10 }}>Tambah Karakter</div>
              <div style={{ display: "flex", flexDirection: "column", gap: 8 }}>
                <input value={name} onChange={e => setName(e.target.value)} placeholder="Nama karakter" style={{ border: "1px solid #ECE8F8", borderRadius: 8, padding: "8px 10px", fontSize: 12.5 }} />
                <input value={role} onChange={e => setRole(e.target.value)} placeholder="Peran (mis. Tokoh Utama)" style={{ border: "1px solid #ECE8F8", borderRadius: 8, padding: "8px 10px", fontSize: 12.5 }} />
                <textarea value={desc} onChange={e => setDesc(e.target.value)} placeholder="Deskripsi singkat" style={{ border: "1px solid #ECE8F8", borderRadius: 8, padding: "8px 10px", fontSize: 12.5, minHeight: 60 }} />
                <button onClick={() => { if (name.trim()) { addCharacter(activeId, name.trim(), role.trim(), desc.trim()); setName(""); setRole(""); setDesc(""); } }} style={{ background: "#22C55E", color: "#fff", border: "none", borderRadius: 9, padding: "9px 0", fontWeight: 600, fontSize: 12.5, cursor: "pointer" }}>
                  Simpan Karakter
                </button>
              </div>
            </Card>
          </div>
          {list.length === 0 && <div style={{ marginTop: 16 }}><EmptyState text="Belum ada karakter untuk novel ini." /></div>}
        </div>
      );
    }

    function ConsultPage({ novels, consultations, cycleConsultStatus, t }) {
      const [filter, setFilter] = useState("Semua");
      const tabs = ["Semua", "urgent", "revisi", "selesai", "info"];
      const list = filter === "Semua" ? consultations : consultations.filter(c => c.status === filter);
      return (
        <div>
          <PageTitle title={t("consultTitle")} sub={t("consultSub")} />
          {!novels.length ? <EmptyState text={t("belumAdaNovelSama")} /> : (
            <React.Fragment>
              <FilterTabs tabs={tabs} labels={{ Semua: "Semua", urgent: "Urgent", revisi: "Revisi", selesai: "Selesai", info: "Info" }} active={filter} onChange={setFilter} />
              <div style={{ display: "flex", flexDirection: "column", gap: 12, marginTop: 16 }}>
                {list.length === 0 && <EmptyState text="Tidak ada catatan pada kategori ini." />}
                {list.map(c => {
                  const novel = novels.find(n => n.id === c.novelId);
                  return <ConsultCard key={c.id} c={c} novelTitle={novel?.title} onCycle={() => cycleConsultStatus(c.id)} />;
                })}
              </div>
            </React.Fragment>
          )}
        </div>
      );
    }

    function IdeaVaultPage({ ideas, addIdea, novels, t }) {
      const [category, setCategory] = useState("Plot Twist");
      const [title, setTitle] = useState("");
      const [desc, setDesc] = useState("");
      const [filter, setFilter] = useState("Semua");
      const categories = ["Plot Twist", "Dialog", "Scene", "Karakter"];
      const list = filter === "Semua" ? ideas : ideas.filter(i => i.category === filter);

      return (
        <div>
          <PageTitle title={t("ideaTitle")} sub={t("ideaSub")} />
          <Card style={{ padding: 20, marginBottom: 20 }}>
            <div style={{ display: "flex", gap: 8, marginBottom: 8 }}>
              <select value={category} onChange={e => setCategory(e.target.value)} style={{ border: "1px solid #ECE8F8", borderRadius: 9, padding: "10px 12px", fontSize: 13 }}>
                {categories.map(c => <option key={c}>{c}</option>)}
              </select>
              <input value={title} onChange={e => setTitle(e.target.value)} placeholder="Judul ide" style={{ flex: 1, border: "1px solid #ECE8F8", borderRadius: 9, padding: "10px 12px", fontSize: 13 }} />
            </div>
            <div style={{ display: "flex", gap: 8 }}>
              <textarea value={desc} onChange={e => setDesc(e.target.value)} placeholder="Detail ide..." style={{ flex: 1, border: "1px solid #ECE8F8", borderRadius: 9, padding: "10px 12px", fontSize: 13, minHeight: 44 }} />
              <button onClick={() => { if (title.trim()) { addIdea(category, title.trim(), desc.trim()); setTitle(""); setDesc(""); } }} style={{ background: "#22C55E", color: "#fff", border: "none", borderRadius: 9, padding: "0 16px", fontWeight: 600, fontSize: 13, cursor: "pointer", display: "flex", alignItems: "center", gap: 6 }}>
                <Plus size={15} /> Tambah Ide
              </button>
            </div>
          </Card>
          <FilterTabs tabs={["Semua", ...categories]} active={filter} onChange={setFilter} />
          <div style={{ display: "grid", gridTemplateColumns: "repeat(2,1fr)", gap: 14, marginTop: 16 }}>
            {list.length === 0 && <EmptyState text="Belum ada ide pada kategori ini." />}
            {list.map(idea => {
              const novel = novels?.find(n => n.id === idea.novelId);
              return (
                <Card key={idea.id} style={{ padding: 16 }}>
                  <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 6 }}>
                    <Pill tone="violet">{idea.category}</Pill>
                    <span style={{ fontSize: 11, color: "#9691B0" }}>{idea.time}</span>
                  </div>
                  <div style={{ fontWeight: 700, fontSize: 14 }}>{idea.title}</div>
                  <div style={{ fontSize: 12.5, color: "#6B6485", marginTop: 4 }}>{idea.desc}</div>
                  {novel && <div style={{ fontSize: 11, color: "#9691B0", marginTop: 8 }}>📖 {novel.title}</div>}
                </Card>
              );
            })}
          </div>
        </div>
      );
    }

    function ProgressPage({ novels, chapters, t }) {
      const [month, setMonth] = useState(4);
      const totalWords = novels.reduce((s, n) => s + n.words, 0);
      const totalTarget = novels.reduce((s, n) => s + n.targetWords, 0) || 1;
      const overallPct = novels.length ? Math.round((totalWords / totalTarget) * 100) : 0;
      const doneChapters = chapters.filter(c => c.status === "done").length;

      return (
        <div>
          <PageTitle title={t("progressTitle")} sub={t("progressSub")} />
          {!novels.length ? <EmptyState text={t("belumAdaNovelSama")} /> : (
            <React.Fragment>
              <div style={{ display: "grid", gridTemplateColumns: "1fr 2fr", gap: 20 }}>
                <Card style={{ padding: 24, display: "flex", flexDirection: "column", alignItems: "center" }}>
                  <DonutMini pct={overallPct} />
                  <div style={{ marginTop: 12, fontWeight: 700, fontSize: 14 }}>Progress Keseluruhan</div>
                  <div style={{ fontSize: 12, color: "#9691B0" }}>{totalWords.toLocaleString("id-ID")} / {totalTarget.toLocaleString("id-ID")} kata</div>
                </Card>
                <Card style={{ padding: 24 }}>
                  <SectionHeader title="Progress per Novel" />
                  <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>
                    {novels.map(n => {
                      const pct = Math.round((n.words / n.targetWords) * 100);
                      return (
                        <div key={n.id}>
                          <div style={{ display: "flex", justifyContent: "space-between", fontSize: 13, marginBottom: 6 }}>
                            <span style={{ fontWeight: 600 }}>{n.title}</span><span style={{ color: "#9691B0" }}>{pct}%</span>
                          </div>
                          <ProgressBar value={pct} />
                        </div>
                      );
                    })}
                  </div>
                </Card>
              </div>
              <div style={{ display: "grid", gridTemplateColumns: "repeat(4,1fr)", gap: 16, margin: "20px 0" }}>
                <StatBig icon={Flame} color="#F59E0B" label="Streak Menulis" value="0 hari" />
                <StatBig icon={FileText} color="#22C55E" label="Chapter Selesai" value={doneChapters} />
                <StatBig icon={BookOpen} color="#7C4DFF" label="Total Novel" value={novels.length} />
                <StatBig icon={Star} color="#3B82F6" label="Total Kata" value={totalWords.toLocaleString("id-ID")} />
              </div>
              <Card style={{ padding: 20, maxWidth: 420 }}>
                <MiniCalendar month={month} setMonth={setMonth} />
              </Card>
            </React.Fragment>
          )}
        </div>
      );
    }

    function SettingsPage({ profile, setProfile, lang, setLang, t }) {
      const [activeTab, setActiveTab] = useState("profil");
      const [name, setName] = useState(profile.name);
      const [bio, setBio] = useState(profile.bio);

      return (
        <div>
          <PageTitle title={t("settingsTitle")} sub={t("settingsSub")} />
          <div style={{ display: "flex", gap: 10, marginBottom: 16 }}>
            <button onClick={() => setActiveTab("profil")} style={{ background: activeTab === "profil" ? "#5B21B6" : "#fff", color: activeTab === "profil" ? "#fff" : "#4B3A7A", border: "1px solid #ECE8F8", borderRadius: 99, padding: "8px 16px", fontWeight: 600, fontSize: 12.5, cursor: "pointer" }}>{t("tabProfil")}</button>
            <button onClick={() => setActiveTab("bahasa")} style={{ background: activeTab === "bahasa" ? "#5B21B6" : "#fff", color: activeTab === "bahasa" ? "#fff" : "#4B3A7A", border: "1px solid #ECE8F8", borderRadius: 99, padding: "8px 16px", fontWeight: 600, fontSize: 12.5, cursor: "pointer" }}>{t("tabBahasa")}</button>
          </div>

          {activeTab === "profil" && (
            <Card style={{ padding: 22, maxWidth: 500 }}>
              <div style={{ display: "flex", flexDirection: "column", gap: 14 }}>
                <div>
                  <div style={{ fontSize: 12, fontWeight: 600, marginBottom: 6 }}>{t("namaLabel")}</div>
                  <input value={name} onChange={e => setName(e.target.value)} style={{ width: "100%", border: "1px solid #ECE8F8", borderRadius: 8, padding: "9px 12px", fontSize: 13 }} />
                </div>
                <div>
                  <div style={{ fontSize: 12, fontWeight: 600, marginBottom: 6 }}>{t("bioLabel")}</div>
                  <input value={bio} onChange={e => setBio(e.target.value)} style={{ width: "100%", border: "1px solid #ECE8F8", borderRadius: 8, padding: "9px 12px", fontSize: 13 }} />
                </div>
                <button onClick={() => setProfile({ ...profile, name, bio })} style={{ background: "#5B21B6", color: "#fff", border: "none", borderRadius: 9, padding: "10px 0", fontWeight: 600, fontSize: 13, cursor: "pointer", marginTop: 8 }}>
                  {t("simpanProfil")}
                </button>
              </div>
            </Card>
          )}

          {activeTab === "bahasa" && (
            <Card style={{ padding: 22, maxWidth: 500 }}>
              <div style={{ fontSize: 13, color: "#6B6485", marginBottom: 14 }}>{t("pilihBahasa")}</div>
              <div style={{ display: "flex", gap: 10 }}>
                <button onClick={() => setLang("id")} style={{ flex: 1, padding: 12, borderRadius: 10, border: lang === "id" ? "2px solid #5B21B6" : "1px solid #ECE8F8", background: "#fff", fontWeight: 600, cursor: "pointer" }}>🇮🇩 {t("bahasaID")}</button>
                <button onClick={() => setLang("en")} style={{ flex: 1, padding: 12, borderRadius: 10, border: lang === "en" ? "2px solid #5B21B6" : "1px solid #ECE8F8", background: "#fff", fontWeight: 600, cursor: "pointer" }}>🇬🇧 {t("bahasaEN")}</button>
              </div>
            </Card>
          )}
        </div>
      );
    }

    /* ---------------------------------------------------------------
       WORKSPACE NOVEL HUB
    ---------------------------------------------------------------- */
    function WorkspaceNovel({
      novel, novels, setNovels, workspace, setWorkspace, chapters, addChapter, markChapterDone,
      saveChapterContent, characters, addCharacter, plots, addPlot, ideas, addIdea,
      consultations, cycleConsultStatus, setActiveTab, updateNovel,
    }) {
      if (!novel) return null;
      const section = workspace.section;
      const setSection = (key) => setWorkspace(w => ({ ...w, section: key, editingChapterId: null }));
      const novelChapters = chapters.filter(c => c.novelId === novel.id).sort((a, b) => b.number - a.number);
      const chapterPct = novel.totalChapters ? Math.round((novel.chapters / novel.totalChapters) * 100) : 0;
      const editingChapter = chapters.find(c => c.id === workspace.editingChapterId);

      return (
        <div>
          <div style={{ display: "flex", alignItems: "center", gap: 10, marginBottom: 18 }}>
            <button onClick={() => setActiveTab("novelku")} style={{ background: "#fff", border: "1px solid #ECE8F8", borderRadius: 10, width: 34, height: 34, cursor: "pointer", display: "flex", alignItems: "center", justifyContent: "center" }}>
              <ChevronLeft size={16} />
            </button>
            <NovelCover novel={novel} w={40} h={54} />
            <div>
              <div style={{ fontFamily: "Poppins,sans-serif", fontWeight: 700, fontSize: 16 }}>{novel.title}</div>
              <div style={{ fontSize: 12, color: "#9691B0" }}>{novel.chapters} / {novel.totalChapters} Chapter • {chapterPct}%</div>
            </div>
          </div>

          <div style={{ display: "grid", gridTemplateColumns: "220px 1fr", gap: 20, alignItems: "start" }}>
            <Card style={{ padding: 10 }}>
              {WORKSPACE_SECTIONS.map(s => {
                const Icon = s.icon;
                const active = section === s.key;
                return (
                  <button key={s.key} onClick={() => setSection(s.key)} style={{
                    display: "flex", alignItems: "center", gap: 10, width: "100%", padding: "10px 12px", borderRadius: 10,
                    border: "none", cursor: "pointer", textAlign: "left", marginBottom: 2,
                    background: active ? "#F1EBFF" : "transparent", color: active ? "#5B21B6" : "#4B3A7A", fontWeight: active ? 700 : 500, fontSize: 13,
                  }}>
                    <Icon size={15} /> {s.label} <ChevronRight size={13} style={{ marginLeft: "auto", opacity: active ? 1 : 0.3 }} />
                  </button>
                );
              })}
            </Card>

            <div style={{ minWidth: 0 }}>
              {section === "overview" && <WorkspaceOverview novel={novel} chapters={novelChapters} setSection={setSection} />}
              {section === "chapter" && !editingChapter && (
                <WorkspaceChapterList novel={novel} chapters={novelChapters} addChapter={addChapter} markChapterDone={markChapterDone}
                  onEdit={(id) => setWorkspace(w => ({ ...w, editingChapterId: id }))} />
              )}
              {section === "chapter" && editingChapter && (
                <ChapterEditor chapter={editingChapter} chapters={novelChapters}
                  onBack={() => setWorkspace(w => ({ ...w, editingChapterId: null }))}
                  onSave={saveChapterContent}
                  onNavigate={(id) => setWorkspace(w => ({ ...w, editingChapterId: id }))} />
              )}
              {section === "planner" && <ActPlanner novel={novel} plots={plots.filter(p => p.novelId === novel.id)} addPlot={addPlot} />}
              {section === "characters" && <WorkspaceCharacters novel={novel} characters={characters.filter(c => c.novelId === novel.id)} addCharacter={addCharacter} />}
              {section === "ideas" && <WorkspaceIdeas novel={novel} ideas={ideas.filter(i => i.novelId === novel.id)} addIdea={addIdea} />}
              {section === "consult" && <WorkspaceConsult novel={novel} consultations={consultations.filter(c => c.novelId === novel.id)} cycleConsultStatus={cycleConsultStatus} />}
              {section === "progress" && <WorkspaceProgress novel={novel} chapters={novelChapters} />}
              {section === "settings" && <WorkspaceSettings novel={novel} updateNovel={updateNovel} />}
            </div>
          </div>
        </div>
      );
    }

    function WorkspaceOverview({ novel, chapters, setSection }) {
      const wpct = novel.targetWords ? Math.round((novel.words / novel.targetWords) * 100) : 0;
      const cpct = novel.totalChapters ? Math.round((novel.chapters / novel.totalChapters) * 100) : 0;
      const draft = chapters.find(c => c.status === "draft") || chapters[0];
      return (
        <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>
          <Card style={{ padding: 20 }}>
            <div style={{ fontSize: 12, color: "#9691B0", marginBottom: 4 }}>{novel.genre}</div>
            <h3 style={{ fontFamily: "Poppins,sans-serif", margin: "0 0 14px" }}>{novel.title}</h3>
            <div style={{ display: "grid", gridTemplateColumns: "repeat(2,1fr)", gap: 14 }}>
              <div>
                <div style={{ display: "flex", justifyContent: "space-between", fontSize: 12, marginBottom: 6 }}><span>Progress Kata</span><span>{wpct}%</span></div>
                <ProgressBar value={wpct} />
                <div style={{ fontSize: 11, color: "#9691B0", marginTop: 4 }}>{novel.words.toLocaleString("id-ID")} / {novel.targetWords.toLocaleString("id-ID")} kata</div>
              </div>
              <div>
                <div style={{ display: "flex", justifyContent: "space-between", fontSize: 12, marginBottom: 6 }}><span>Progress Chapter</span><span>{cpct}%</span></div>
                <ProgressBar value={cpct} color="#22C55E" />
                <div style={{ fontSize: 11, color: "#9691B0", marginTop: 4 }}>{novel.chapters} / {novel.totalChapters} chapter</div>
              </div>
            </div>
          </Card>
          <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 16 }}>
            <Card className="nc-clickable" onClick={() => setSection("chapter")} style={{ padding: 18 }}>
              <FileText size={18} color="#7C4DFF" />
              <div style={{ fontWeight: 700, marginTop: 8 }}>Lanjutkan Menulis</div>
              <div style={{ fontSize: 12, color: "#9691B0" }}>{draft ? `Chapter ${draft.number} • ${draft.title}` : "Mulai chapter pertama"}</div>
            </Card>
            <Card className="nc-clickable" onClick={() => setSection("consult")} style={{ padding: 18 }}>
              <MessageSquare size={18} color="#22C55E" />
              <div style={{ fontWeight: 700, marginTop: 8 }}>Cek Konsultasi</div>
              <div style={{ fontSize: 12, color: "#9691B0" }}>Lihat masukan terbaru untuk novel ini</div>
            </Card>
          </div>
        </div>
      );
    }

    function WorkspaceChapterList({ novel, chapters, addChapter, markChapterDone, onEdit }) {
      const [newTitle, setNewTitle] = useState("");
      return (
        <Card style={{ padding: 20 }}>
          <div style={{ display: "flex", gap: 8, marginBottom: 16 }}>
            <input value={newTitle} onChange={e => setNewTitle(e.target.value)} placeholder="Judul chapter baru..." style={{ flex: 1, border: "1px solid #ECE8F8", borderRadius: 9, padding: "10px 12px", fontSize: 13 }} />
            <button onClick={() => { addChapter(novel.id, newTitle.trim()); setNewTitle(""); }} style={{ background: "#5B21B6", color: "#fff", border: "none", borderRadius: 9, padding: "0 16px", fontWeight: 600, fontSize: 13, cursor: "pointer", display: "flex", alignItems: "center", gap: 6 }}>
              <Plus size={15} /> Tambah Chapter
            </button>
          </div>
          <div style={{ display: "flex", flexDirection: "column", gap: 4 }}>
            {chapters.length === 0 && <EmptyState text="Belum ada chapter. Tambahkan chapter pertamamu." />}
            {chapters.map(c => (
              <div key={c.id} onClick={() => onEdit(c.id)} className="nc-clickable" style={{ display: "flex", alignItems: "center", gap: 12, padding: "10px 12px", borderRadius: 10, cursor: "pointer" }}>
                <div onClick={(e) => { e.stopPropagation(); markChapterDone(c.id); }} style={{
                  width: 20, height: 20, borderRadius: "50%", flexShrink: 0, background: c.status === "done" ? "#22C55E" : "#F1EBFF",
                  display: "flex", alignItems: "center", justifyContent: "center",
                }}>
                  {c.status === "done" && <Check size={12} color="#fff" />}
                </div>
                <div style={{ flex: 1, fontSize: 13, fontWeight: 600 }}>Chapter {String(c.number).padStart(2, "0")}{c.title ? ` — ${c.title}` : ""}</div>
                {c.status === "draft" && <Pill tone="gray">Draft</Pill>}
                <ChevronRight size={14} color="#C9C2E3" />
              </div>
            ))}
          </div>
        </Card>
      );
    }

    function ChapterEditor({ chapter, chapters, onBack, onSave, onNavigate }) {
      const [content, setContent] = useState(chapter.content || "");
      const [title, setTitle] = useState(chapter.title || "");
      const [savedFlash, setSavedFlash] = useState(false);
      const words = content.trim() ? content.trim().split(/\s+/).length : 0;
      const idx = chapters.findIndex(c => c.id === chapter.id);
      const prevChapter = chapters[idx + 1];
      const nextChapter = chapters[idx - 1];
      const pct = chapter.target ? Math.min(100, Math.round((words / chapter.target) * 100)) : 0;

      function handleSave() {
        onSave(chapter.id, content);
        setSavedFlash(true);
        setTimeout(() => setSavedFlash(false), 1500);
      }

      return (
        <Card style={{ padding: 0, overflow: "hidden" }}>
          <div style={{ display: "flex", alignItems: "center", justifyContent: "space-between", padding: "14px 20px", borderBottom: "1px solid #ECE8F8" }}>
            <button onClick={onBack} style={{ background: "none", border: "none", cursor: "pointer", display: "flex", alignItems: "center", gap: 6, color: "#4B3A7A", fontSize: 13, fontWeight: 600 }}>
              <ChevronLeft size={16} /> Chapter {chapter.number}
            </button>
            <Pill tone={chapter.status === "done" ? "green" : "gray"}>{chapter.status === "done" ? "Selesai" : "Draft"}</Pill>
          </div>
          <div style={{ padding: 20 }}>
            <input value={title} onChange={e => setTitle(e.target.value)} placeholder="Judul Chapter" style={{ border: "none", fontFamily: "Poppins,sans-serif", fontWeight: 700, fontSize: 18, width: "100%", marginBottom: 14, color: "#1F1147" }} />
            <textarea value={content} onChange={e => setContent(e.target.value)} placeholder="Mulai menulis ceritamu di sini..." style={{ width: "100%", minHeight: 280, border: "1px solid #ECE8F8", borderRadius: 12, padding: 16, fontSize: 14, lineHeight: 1.8, color: "#3D3163", resize: "vertical" }} />
            <div style={{ display: "flex", alignItems: "center", gap: 10, marginTop: 14 }}>
              <div style={{ flex: 1 }}><ProgressBar value={pct} /></div>
              <span style={{ fontSize: 12, color: "#9691B0", whiteSpace: "nowrap" }}>{words.toLocaleString("id-ID")} kata{chapter.target ? ` • Target: ${chapter.target.toLocaleString("id-ID")} kata` : ""}</span>
            </div>
            <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginTop: 18 }}>
              <div style={{ display: "flex", gap: 8 }}>
                <button disabled={!prevChapter} onClick={() => prevChapter && onNavigate(prevChapter.id)} style={{
                  background: "#fff", border: "1px solid #ECE8F8", borderRadius: 9, padding: "8px 14px", fontSize: 12.5, fontWeight: 600,
                  color: prevChapter ? "#4B3A7A" : "#C9C2E3", cursor: prevChapter ? "pointer" : "default", display: "flex", alignItems: "center", gap: 6,
                }}><ChevronLeft size={13} /> Prev Chapter</button>
                <button disabled={!nextChapter} onClick={() => nextChapter && onNavigate(nextChapter.id)} style={{
                  background: "#fff", border: "1px solid #ECE8F8", borderRadius: 9, padding: "8px 14px", fontSize: 12.5, fontWeight: 600,
                  color: nextChapter ? "#4B3A7A" : "#C9C2E3", cursor: nextChapter ? "pointer" : "default", display: "flex", alignItems: "center", gap: 6,
                }}>Next Chapter <ChevronRight size={13} /></button>
              </div>
              <button onClick={handleSave} style={{ background: "#5B21B6", color: "#fff", border: "none", borderRadius: 9, padding: "9px 20px", fontSize: 13, fontWeight: 600, cursor: "pointer" }}>
                {savedFlash ? "✓ Tersimpan" : "Simpan Chapter"}
              </button>
            </div>
          </div>
        </Card>
      );
    }

    function ActPlanner({ novel, plots, addPlot }) {
      const [act, setAct] = useState("Act 1");
      const [text, setText] = useState("");
      const acts = ["Act 1", "Act 2", "Act 3"];
      const actLabel = { "Act 1": "Introduction", "Act 2": "Conflict", "Act 3": "Resolution" };

      return (
        <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>
          <Card style={{ padding: 18 }}>
            <div style={{ display: "flex", gap: 8 }}>
              <select value={act} onChange={e => setAct(e.target.value)} style={{ border: "1px solid #ECE8F8", borderRadius: 9, padding: "10px 12px", fontSize: 13 }}>
                {acts.map(a => <option key={a}>{a}</option>)}
              </select>
              <input value={text} onChange={e => setText(e.target.value)} placeholder="Tambahkan poin adegan..." style={{ flex: 1, border: "1px solid #ECE8F8", borderRadius: 9, padding: "10px 12px", fontSize: 13 }} />
              <button onClick={() => { if (text.trim()) { addPlot(novel.id, "Plot", text.trim(), act); setText(""); } }} style={{ background: "#5B21B6", color: "#fff", border: "none", borderRadius: 9, padding: "0 16px", fontWeight: 600, fontSize: 13, cursor: "pointer", display: "inline-flex", alignItems: "center", justifyContent: "center" }}>
                <Plus size={15} />
              </button>
            </div>
          </Card>
          {acts.map(a => {
            const points = plots.filter(p => (p.act || "Act 1") === a);
            return (
              <Card key={a} style={{ padding: 18 }}>
                <div style={{ display: "flex", alignItems: "center", gap: 8, marginBottom: 12 }}>
                  <div style={{ fontFamily: "Poppins,sans-serif", fontWeight: 700, fontSize: 14 }}>{a}</div>
                  <span style={{ fontSize: 12, color: "#9691B0" }}>— {actLabel[a]}</span>
                </div>
                {points.length === 0 ? (
                  <div style={{ fontSize: 12.5, color: "#C9C2E3" }}>Belum ada poin cerita di babak ini.</div>
                ) : (
                  <ul style={{ margin: 0, paddingLeft: 18, display: "flex", flexDirection: "column", gap: 6 }}>
                    {points.map(p => <li key={p.id} style={{ fontSize: 13, color: "#3D3163" }}>{p.text}</li>)}
                  </ul>
                )}
              </Card>
            );
          })}
        </div>
      );
    }

    function WorkspaceCharacters({ novel, characters, addCharacter }) {
      const [selectedId, setSelectedId] = useState(characters[0]?.id || null);
      const [tab, setTab] = useState("Profile");
      const [showAdd, setShowAdd] = useState(false);
      const [name, setName] = useState("");
      const selected = characters.find(c => c.id === selectedId) || characters[0];
      const tabs = ["Profile", "Relationship", "Arc", "Notes"];

      return (
        <div style={{ display: "grid", gridTemplateColumns: "220px 1fr", gap: 16 }}>
          <Card style={{ padding: 12 }}>
            {characters.map(c => (
              <div key={c.id} onClick={() => setSelectedId(c.id)} style={{
                display: "flex", alignItems: "center", gap: 8, padding: "9px 10px", borderRadius: 9, cursor: "pointer",
                background: selected?.id === c.id ? "#F1EBFF" : "transparent", marginBottom: 2,
              }}>
                <div style={{ width: 26, height: 26, borderRadius: "50%", background: "#7C4DFF", color: "#fff", display: "flex", alignItems: "center", justifyContent: "center", fontSize: 11, fontWeight: 700, flexShrink: 0 }}>{c.name.charAt(0)}</div>
                <span style={{ fontSize: 12.5, fontWeight: 600, color: selected?.id === c.id ? "#5B21B6" : "#4B3A7A" }}>{c.name}</span>
              </div>
            ))}
            {!showAdd ? (
              <button onClick={() => setShowAdd(true)} style={{ marginTop: 8, width: "100%", background: "#F1EBFF", color: "#5B21B6", border: "none", borderRadius: 9, padding: "8px 0", fontSize: 12, fontWeight: 600, cursor: "pointer" }}>+ Karakter</button>
            ) : (
              <div style={{ marginTop: 8, display: "flex", gap: 6 }}>
                <input value={name} onChange={e => setName(e.target.value)} placeholder="Nama" style={{ flex: 1, border: "1px solid #ECE8F8", borderRadius: 8, padding: "7px 8px", fontSize: 11.5 }} />
                <button onClick={() => { if (name.trim()) { addCharacter(novel.id, name.trim(), "Karakter Pendukung", ""); setName(""); setShowAdd(false); } }} style={{ background: "#5B21B6", color: "#fff", border: "none", borderRadius: 8, padding: "0 10px", cursor: "pointer", display: "inline-flex", alignItems: "center", justifyContent: "center" }}><Plus size={13} /></button>
              </div>
            )}
          </Card>

          {selected ? (
            <Card style={{ padding: 20 }}>
              <div style={{ display: "flex", gap: 16 }}>
                <div style={{ width: 64, height: 64, borderRadius: 14, background: "#7C4DFF", color: "#fff", display: "flex", alignItems: "center", justifyContent: "center", fontFamily: "Poppins,sans-serif", fontWeight: 700, fontSize: 22, flexShrink: 0 }}>{selected.name.charAt(0)}</div>
                <div><div style={{ fontFamily: "Poppins,sans-serif", fontWeight: 700, fontSize: 17 }}>{selected.name}</div><Pill tone="violet">{selected.role}</Pill></div>
              </div>
              <div style={{ display: "flex", gap: 6, marginTop: 18, marginBottom: 16, borderBottom: "1px solid #ECE8F8" }}>
                {tabs.map(tb => (
                  <button key={tb} onClick={() => setTab(tb)} style={{
                    background: "none", border: "none", padding: "8px 4px", marginRight: 16, cursor: "pointer", fontSize: 13, fontWeight: 600,
                    color: tab === tb ? "#5B21B6" : "#9691B0", borderBottom: tab === tb ? "2px solid #5B21B6" : "2px solid transparent",
                  }}>{tb}</button>
                ))}
              </div>
              {tab === "Profile" && (
                <div style={{ display: "flex", flexDirection: "column", gap: 12, fontSize: 13 }}>
                  <FieldRow label="Peran" value={selected.role} />
                  <FieldRow label="Usia" value={selected.usia || "-"} />
                  <FieldRow label="Kepribadian" value={selected.kepribadian || "-"} />
                  <FieldRow label="Latar Belakang" value={selected.latar || selected.desc || "-"} />
                </div>
              )}
              {tab === "Relationship" && <p style={{ fontSize: 13, color: "#3D3163", lineHeight: 1.7 }}>{selected.relationship || "Belum ada catatan hubungan."}</p>}
              {tab === "Arc" && <p style={{ fontSize: 13, color: "#3D3163", lineHeight: 1.7 }}>{selected.arc || "Belum ada catatan character arc."}</p>}
              {tab === "Notes" && <p style={{ fontSize: 13, color: "#3D3163", lineHeight: 1.7 }}>{selected.notes || "Belum ada catatan tambahan."}</p>}
            </Card>
          ) : <Card style={{ padding: 20 }}><EmptyState text="Belum ada karakter untuk novel ini." /></Card>}
        </div>
      );
    }

    function WorkspaceIdeas({ novel, ideas, addIdea }) {
      const [filter, setFilter] = useState("Semua");
      const [category, setCategory] = useState("Plot Twist");
      const [title, setTitle] = useState("");
      const categories = ["Plot Twist", "Dialog", "Scene", "Karakter"];
      const list = filter === "Semua" ? ideas : ideas.filter(i => i.category === filter);

      return (
        <div>
          <Card style={{ padding: 16, marginBottom: 16 }}>
            <div style={{ display: "flex", gap: 8 }}>
              <select value={category} onChange={e => setCategory(e.target.value)} style={{ border: "1px solid #ECE8F8", borderRadius: 9, padding: "9px 10px", fontSize: 12.5 }}>
                {categories.map(c => <option key={c}>{c}</option>)}
              </select>
              <input value={title} onChange={e => setTitle(e.target.value)} placeholder="Tulis ide baru..." style={{ flex: 1, border: "1px solid #ECE8F8", borderRadius: 9, padding: "9px 10px", fontSize: 12.5 }} />
              <button onClick={() => { if (title.trim()) { addIdea(category, title.trim(), "", novel.id); setTitle(""); } }} style={{ background: "#22C55E", color: "#fff", border: "none", borderRadius: 9, padding: "0 14px", cursor: "pointer", display: "inline-flex", alignItems: "center", justifyContent: "center" }}><Plus size={14} /></button>
            </div>
          </Card>
          <FilterTabs tabs={["Semua", ...categories]} active={filter} onChange={setFilter} />
          <div style={{ display: "flex", flexDirection: "column", gap: 10, marginTop: 14 }}>
            {list.length === 0 && <EmptyState text="Belum ada ide untuk novel ini." />}
            {list.map(idea => (
              <Card key={idea.id} style={{ padding: 14 }}>
                <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 4 }}>
                  <Pill tone="violet">{idea.category}</Pill>
                  <span style={{ fontSize: 11, color: "#9691B0" }}>{idea.time}</span>
                </div>
                <div style={{ fontWeight: 600, fontSize: 13.5 }}>{idea.title}</div>
                {idea.desc && <div style={{ fontSize: 12, color: "#6B6485", marginTop: 4 }}>{idea.desc}</div>}
              </Card>
            ))}
          </div>
        </div>
      );
    }

    function WorkspaceConsult({ novel, consultations, cycleConsultStatus }) {
      return (
        <div style={{ display: "flex", flexDirection: "column", gap: 12 }}>
          {consultations.length === 0 && <EmptyState text="Belum ada catatan konsultasi untuk novel ini." />}
          {consultations.map(c => (
            <ConsultCard key={c.id} c={c} novelTitle={novel.title} onCycle={() => cycleConsultStatus(c.id)} />
          ))}
        </div>
      );
    }

    function WorkspaceProgress({ novel, chapters }) {
      const wpct = novel.targetWords ? Math.round((novel.words / novel.targetWords) * 100) : 0;
      const cpct = novel.totalChapters ? Math.round((novel.chapters / novel.totalChapters) * 100) : 0;
      return (
        <div style={{ display: "flex", flexDirection: "column", gap: 16 }}>
          <Card style={{ padding: 20 }}>
            <div style={{ fontWeight: 700, fontSize: 15, marginBottom: 14 }}>Progres Penulisan</div>
            <div style={{ marginBottom: 14 }}>
              <div style={{ display: "flex", justifyContent: "space-between", fontSize: 12, marginBottom: 6 }}><span>Target Kata ({novel.targetWords.toLocaleString("id-ID")})</span><span>{wpct}%</span></div>
              <ProgressBar value={wpct} />
            </div>
            <div>
              <div style={{ display: "flex", justifyContent: "space-between", fontSize: 12, marginBottom: 6 }}><span>Target Chapter ({novel.totalChapters})</span><span>{cpct}%</span></div>
              <ProgressBar value={cpct} color="#22C55E" />
            </div>
          </Card>
        </div>
      );
    }

    function WorkspaceSettings({ novel, updateNovel }) {
      const [title, setTitle] = useState(novel.title);
      const [genre, setGenre] = useState(novel.genre);
      const [targetWords, setTargetWords] = useState(novel.targetWords);

      return (
        <Card style={{ padding: 20 }}>
          <div style={{ fontWeight: 700, fontSize: 15, marginBottom: 14 }}>Pengaturan Novel</div>
          <div style={{ display: "flex", flexDirection: "column", gap: 12 }}>
            <div>
              <div style={{ fontSize: 12, color: "#9691B0", marginBottom: 4 }}>Judul</div>
              <input value={title} onChange={e => setTitle(e.target.value)} style={{ width: "100%", border: "1px solid #ECE8F8", borderRadius: 8, padding: "8px 10px", fontSize: 13 }} />
            </div>
            <div>
              <div style={{ fontSize: 12, color: "#9691B0", marginBottom: 4 }}>Genre</div>
              <input value={genre} onChange={e => setGenre(e.target.value)} style={{ width: "100%", border: "1px solid #ECE8F8", borderRadius: 8, padding: "8px 10px", fontSize: 13 }} />
            </div>
            <div>
              <div style={{ fontSize: 12, color: "#9691B0", marginBottom: 4 }}>Target Kata</div>
              <input type="number" value={targetWords} onChange={e => setTargetWords(Number(e.target.value))} style={{ width: "100%", border: "1px solid #ECE8F8", borderRadius: 8, padding: "8px 10px", fontSize: 13 }} />
            </div>
            <button onClick={() => updateNovel(novel.id, { title, genre, targetWords })} style={{ background: "#5B21B6", color: "#fff", border: "none", borderRadius: 8, padding: "9px 0", fontWeight: 600, fontSize: 13, cursor: "pointer", marginTop: 6 }}>
              Simpan Perubahan
            </button>
          </div>
        </Card>
      );
    }

    /* ---------------------------------------------------------------
       RENDER APPLICATION
    ---------------------------------------------------------------- */
    const root = ReactDOM.createRoot(document.getElementById('root'));
    root.render(<App />);
  </script>
</body>
</html>

<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Novel Consult</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@500;600;700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet" />
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: Inter, sans-serif;
      background: #F6F4FC;
      color: #1F1147;
      min-height: 100vh;
    }
    button { font-family: inherit; cursor: pointer; }
    input, textarea, select { font-family: inherit; outline: none; }
    ::-webkit-scrollbar { width: 8px; height: 8px; }
    ::-webkit-scrollbar-thumb { background: #D9D2F0; border-radius: 8px; }

    .app { display: flex; min-height: 100vh; }
    .sidebar {
      width: 250px; flex-shrink: 0;
      background: linear-gradient(180deg,#2A1B5C,#1B1140);
      color: #fff; padding: 24px 16px;
      display: flex; flex-direction: column;
    }
    .sidebar-logo { display: flex; align-items: center; gap: 10px; padding: 0 8px 4px; }
    .logo-box {
      width: 36px; height: 36px; border-radius: 10px;
      background: rgba(255,255,255,0.1);
      display: flex; align-items: center; justify-content: center;
      font-family: Poppins,sans-serif; font-weight: 700;
    }
    .logo-text { font-family: Poppins,sans-serif; font-weight: 700; font-size: 15px; line-height: 1.1; }
    .tagline { font-size: 11px; color: #A99CD9; padding: 10px 8px 20px; }
    .nav-btn {
      display: flex; align-items: center; gap: 10px;
      padding: 10px 12px; border-radius: 10px; border: none;
      background: transparent; color: #D7CFEF;
      font-weight: 500; font-size: 13.5px; text-align: left; width: 100%;
      margin-bottom: 4px;
    }
    .nav-btn:hover { background: rgba(255,255,255,0.08); }
    .nav-btn.active { background: #fff; color: #5B21B6; font-weight: 600; }
    .mascot-bubble {
      background: #4ADE80; color: #0B3B1E; font-size: 12px; font-weight: 600;
      padding: 8px 12px; border-radius: 14px; border-bottom-left-radius: 4px;
      margin-bottom: 10px; display: inline-block;
    }
    .profile-box {
      display: flex; align-items: center; gap: 10px;
      background: rgba(255,255,255,0.06); border-radius: 12px; padding: 10px; margin-top: 8px;
    }
    .avatar {
      width: 34px; height: 34px; border-radius: 50%; overflow: hidden;
      background: #7C4DFF; display: flex; align-items: center; justify-content: center;
      font-weight: 700; font-size: 13px; flex-shrink: 0; color: #fff;
    }
    .avatar img { width: 100%; height: 100%; object-fit: cover; }
    .main { flex: 1; display: flex; flex-direction: column; min-width: 0; }
    .topbar {
      display: flex; align-items: center; justify-content: space-between;
      padding: 18px 28px; background: #F6F4FC; position: sticky; top: 0; z-index: 20;
    }
    .search-box {
      display: flex; align-items: center; gap: 8px; background: #fff;
      border-radius: 12px; padding: 10px 14px; width: 340px; border: 1px solid #ECE8F8;
    }
    .search-box input { border: none; background: transparent; font-size: 13.5px; width: 100%; color: #1F1147; }
    .content { padding: 24px 28px 60px; flex: 1; overflow-y: auto; }
    .card {
      background: #fff; border-radius: 18px; border: 1px solid #ECE8F8;
      box-shadow: 0 1px 3px rgba(31,17,71,0.04);
    }
    .nc-clickable { cursor: pointer; transition: transform 0.15s ease, box-shadow 0.15s ease; }
    .nc-clickable:hover { transform: translateY(-2px); box-shadow: 0 6px 18px rgba(31,17,71,0.08); }
    .pill {
      font-size: 12px; font-weight: 600; padding: 4px 10px; border-radius: 99px; display: inline-block;
    }
    .pill-violet { background: #F1EBFF; color: #6D28D9; }
    .pill-green { background: #E9F9EC; color: #1F9D4A; }
    .pill-orange { background: #FFF3E0; color: #B7791F; }
    .pill-gray { background: #F1F1F5; color: #6B7280; }
    .pill-red { background: #FDECEC; color: #DC2626; }
    .progress-bar { width: 100%; height: 8px; border-radius: 99px; background: #EDE9FB; overflow: hidden; }
    .progress-fill { height: 100%; border-radius: 99px; background: #7C4DFF; transition: width 0.4s ease; }
    .btn-primary {
      background: #5B21B6; color: #fff; border: none; border-radius: 9px;
      padding: 9px 16px; font-weight: 600; font-size: 13px;
    }
    .btn-green {
      background: #22C55E; color: #fff; border: none; border-radius: 9px;
      padding: 9px 16px; font-weight: 600; font-size: 13px;
    }
    .btn-outline {
      background: #F1EBFF; color: #5B21B6; border: none; border-radius: 9px;
      padding: 8px 14px; font-size: 12.5px; font-weight: 600;
    }
    .input-field {
      border: 1px solid #ECE8F8; border-radius: 9px; padding: 10px 12px; font-size: 13px; width: 100%;
    }
    .page-title h2 { font-family: Poppins,sans-serif; font-size: 22px; margin: 0 0 4px; color: #1F1147; }
    .page-title p { margin: 0; font-size: 13px; color: #9691B0; }
    .empty-state {
      display: flex; flex-direction: column; align-items: center; gap: 10px;
      padding: 32px 12px; color: #9691B0;
    }
    .filter-tabs { display: flex; gap: 8px; flex-wrap: wrap; }
    .filter-tab {
      border: 1px solid #ECE8F8; border-radius: 99px; padding: 7px 15px;
      font-size: 12.5px; font-weight: 600; background: #fff; color: #4B3A7A;
    }
    .filter-tab.active { background: #5B21B6; color: #fff; border: none; }
    .notif-panel {
      position: absolute; top: 48px; right: 90px; width: 280px; padding: 14px; z-index: 30;
    }
    .loading {
      min-height: 100vh; display: flex; align-items: center; justify-content: center;
      background: #F6F4FC;
    }
  </style>
</head>
<body>
  <div id="root"></div>

  <script>
    /* ============================================================
       STRINGS (i18n)
    ============================================================ */
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

    /* ============================================================
       HELPERS & CONSTANTS
    ============================================================ */
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
      { key: "beranda", labelKey: "nav_beranda", icon: "home" },
      { key: "novelku", labelKey: "nav_novelku", icon: "book" },
      { key: "chapters", labelKey: "nav_chapters", icon: "file" },
      { key: "planner", labelKey: "nav_planner", icon: "map" },
      { key: "characters", labelKey: "nav_characters", icon: "users" },
      { key: "consult", labelKey: "nav_consult", icon: "message" },
      { key: "ideas", labelKey: "nav_ideas", icon: "bulb" },
      { key: "progress", labelKey: "nav_progress", icon: "chart" },
      { key: "settings", labelKey: "nav_settings", icon: "settings" },
    ];
    const WORKSPACE_SECTIONS = [
      { key: "overview", label: "Overview", icon: "book" },
      { key: "chapter", label: "Chapter", icon: "file" },
      { key: "planner", label: "Story Planner", icon: "map" },
      { key: "characters", label: "Character Database", icon: "users" },
      { key: "ideas", label: "Ide & Notes", icon: "bulb" },
      { key: "consult", label: "Catatan Konsultasi", icon: "message" },
      { key: "progress", label: "Writing Progress", icon: "chart" },
      { key: "settings", label: "Pengaturan Novel", icon: "settings" },
    ];
    const STORAGE_KEY = "novel-consult-app-state";

    function t(key) {
      return (STRINGS[state.lang] && STRINGS[state.lang][key]) || STRINGS.id[key] || key;
    }

    function readFileAsDataURL(file) {
      return new Promise((resolve, reject) => {
        const reader = new FileReader();
        reader.onload = () => resolve(reader.result);
        reader.onerror = reject;
        reader.readAsDataURL(file);
      });
    }

    function icon(name, size = 17) {
      const icons = {
        home: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"/><polyline points="9 22 9 12 15 12 15 22"/></svg>`,
        book: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 19.5A2.5 2.5 0 0 1 6.5 17H20"/><path d="M6.5 2H20v20H6.5A2.5 2.5 0 0 1 4 19.5v-15A2.5 2.5 0 0 1 6.5 2z"/></svg>`,
        file: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><polyline points="14 2 14 8 20 8"/></svg>`,
        map: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polygon points="1 6 1 22 8 18 16 22 23 18 23 2 16 6 8 2 1 6"/><line x1="8" y1="2" x2="8" y2="18"/><line x1="16" y1="6" x2="16" y2="22"/></svg>`,
        users: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 0 0-3-3.87"/><path d="M16 3.13a4 4 0 0 1 0 7.75"/></svg>`,
        message: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z"/></svg>`,
        bulb: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 18h6"/><path d="M10 22h4"/><path d="M15.09 14c.18-.98.65-1.74 1.41-2.5A4.65 4.65 0 0 0 18 8 6 6 0 0 0 6 8c0 1 .23 2.23 1.5 3.5A4.61 4.61 0 0 1 8.91 14"/></svg>`,
        chart: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="18" y1="20" x2="18" y2="10"/><line x1="12" y1="20" x2="12" y2="4"/><line x1="6" y1="20" x2="6" y2="14"/></svg>`,
        settings: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 0 1 0 2.83 2 2 0 0 1-2.83 0l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 0 1-2 2 2 2 0 0 1-2-2v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 0 1-2.83 0 2 2 0 0 1 0-2.83l.06-.06A1.65 1.65 0 0 0 4.68 15a1.65 1.65 0 0 0-1.51-1H3a2 2 0 0 1-2-2 2 2 0 0 1 2-2h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 0 1 0-2.83 2 2 0 0 1 2.83 0l.06.06A1.65 1.65 0 0 0 9 4.68a1.65 1.65 0 0 0 1-1.51V3a2 2 0 0 1 2-2 2 2 0 0 1 2 2v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 0 1 2.83 0 2 2 0 0 1 0 2.83l-.06.06A1.65 1.65 0 0 0 19.4 9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 0 1 2 2 2 2 0 0 1-2 2h-.09a1.65 1.65 0 0 0-1.51 1z"/></svg>`,
        search: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>`,
        bell: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M18 8A6 6 0 0 0 6 8c0 7-3 9-3 9h18s-3-2-3-9"/><path d="M13.73 21a2 2 0 0 1-3.46 0"/></svg>`,
        chevronLeft: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="15 18 9 12 15 6"/></svg>`,
        chevronRight: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="9 18 15 12 9 6"/></svg>`,
        chevronDown: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="6 9 12 15 18 9"/></svg>`,
        plus: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="12" y1="5" x2="12" y2="19"/><line x1="5" y1="12" x2="19" y2="12"/></svg>`,
        pencil: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M17 3a2.828 2.828 0 1 1 4 4L7.5 20.5 2 22l1.5-5.5L17 3z"/></svg>`,
        check: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polyline points="20 6 9 17 4 12"/></svg>`,
        camera: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M23 19a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h4l2-3h6l2 3h4a2 2 0 0 1 2 2z"/><circle cx="12" cy="13" r="4"/></svg>`,
        image: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="18" height="18" rx="2" ry="2"/><circle cx="8.5" cy="8.5" r="1.5"/><polyline points="21 15 16 10 5 21"/></svg>`,
        clock: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/></svg>`,
        target: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><circle cx="12" cy="12" r="6"/><circle cx="12" cy="12" r="2"/></svg>`,
        star: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/></svg>`,
        flame: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M8.5 14.5A2.5 2.5 0 0 0 11 12c0-1.38-.5-2-1-3-1.072-2.143-.224-4.054 2-6 .5 2.5 2 4.9 4 6.5 2 1.6 3 3.5 3 5.5a7 7 0 1 1-14 0c0-1.153.433-2.294 1-3a2.5 2.5 0 0 0 2.5 2.5z"/></svg>`,
        arrowRight: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/></svg>`,
        user: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"/><circle cx="12" cy="7" r="4"/></svg>`,
        lock: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="11" width="18" height="11" rx="2" ry="2"/><path d="M7 11V7a5 5 0 0 1 10 0v4"/></svg>`,
        globe: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><line x1="2" y1="12" x2="22" y2="12"/><path d="M12 2a15.3 15.3 0 0 1 4 10 15.3 15.3 0 0 1-4 10 15.3 15.3 0 0 1-4-10 15.3 15.3 0 0 1 4-10z"/></svg>`,
        logout: `<svg width="${size}" height="${size}" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 21H5a2 2 0 0 1-2-2V5a2 2 0

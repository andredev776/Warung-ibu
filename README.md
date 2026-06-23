<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Warung Makan Keluarga - 5 Halaman Premium</title>
    
    <!-- Google Fonts: Poppins -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600;700;800&display=swap" rel="stylesheet">

    <style>
        /* ========================================== */
        /* 1. RESET & BASE STYLE                      */
        /* ========================================== */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', sans-serif;
            scroll-behavior: smooth;
        }

        body {
            background-color: #F8F9FA;
            color: #2D2D2D;
            line-height: 1.6;
            padding-bottom: 80px; /* Jarak agar tidak tertutup nav bawah */
        }

        .container {
            max-width: 500px; 
            margin: 0 auto;
            background-color: #FFFFFF;
            min-height: 100vh;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.05);
            position: relative;
        }

        /* ========================================== */
        /* 2. ARSITEKTUR MULTI-PAGE (CSS ONLY)        */
        /* ========================================== */
        .page {
            display: none; /* Sembunyikan semua halaman dulu */
            animation: fadeIn 0.3s ease-in-out;
        }

        /* Halaman default yang muncul pertama kali */
        #page-menu, :target {
            display: block;
        }

        /* Logic menyembunyikan halaman utama jika halaman lain sedang aktif */
        #page-review:target ~ #page-menu,
        #page-lokasi:target ~ #page-menu,
        #page-promo:target ~ #page-menu,
        #page-kontak:target ~ #page-menu {
            display: none;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* ========================================== */
        /* 3. FIXED BOTTOM NAVIGATION BAR (5 TABS)     */
        /* ========================================== */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 100%;
            max-width: 500px;
            background-color: #FFFFFF;
            display: flex;
            justify-content: space-around;
            padding: 10px 0;
            box-shadow: 0 -4px 15px rgba(0, 0, 0, 0.08);
            border-top: 2px solid #FFD700;
            z-index: 999;
        }

        .nav-item {
            text-decoration: none;
            color: #757575;
            font-size: 0.75rem;
            font-weight: 600;
            text-align: center;
            flex: 1;
        }

        .nav-item span {
            display: block;
            font-size: 1.2rem;
            margin-bottom: 2px;
        }

        .nav-item:active, .nav-item:focus {
            color: #D32F2F;
        }

        /* ========================================== */
        /* 4. STYLE GLOBAL KOMPONEN & HEADER          */
        /* ========================================== */
        header {
            text-align: center;
            padding: 35px 20px;
            background: linear-gradient(180deg, #FFF5F5 0%, #FFFFFF 100%);
            border-bottom: 3px solid #FFD700;
        }

        header .logo { font-size: 3rem; margin-bottom: 5px; }
        header h1 { color: #D32F2F; font-size: 1.6rem; font-weight: 800; }
        header .tagline { color: #B78A02; font-size: 0.95rem; font-weight: 600; }

        section { padding: 25px 20px; }
        section h2 {
            font-size: 1.3rem;
            color: #D32F2F;
            font-weight: 700;
            margin-bottom: 15px;
            position: relative;
            display: inline-block;
        }
        section h2::after {
            content: ''; position: absolute; bottom: -4px; left: 0;
            width: 35px; height: 3px; background-color: #FFD700; border-radius: 2px;
        }

        /* Card Menu (Halaman 1) */
        .menu-list { display: flex; flex-direction: column; gap: 15px; }
        .menu-card {
            background: #FFFFFF; border: 1px solid #F0F0F0; border-radius: 15px;
            padding: 15px; display: flex; align-items: center; gap: 15px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.04);
        }
        .menu-emoji { font-size: 2.2rem; background-color: #FFF9E6; padding: 8px; border-radius: 12px; min-width: 55px; text-align: center; }
        .menu-title { font-size: 1.05rem; font-weight: 700; }
        .menu-price { color: #B78A02; font-weight: 700; }
        .menu-desc { color: #757575; font-size: 0.85rem; }

        /* Card Ulasan (Halaman 2) */
        .review-card { background: #FFFFFF; border: 1px solid #E0E0E0; padding: 15px; border-radius: 12px; margin-bottom: 12px; }
        .stars { color: #FFD700; font-size: 0.9rem; }
        .user-info { font-weight: 700; font-size: 0.85rem; color: #757575; margin-top: 5px; }

        /* Info Lokasi (Halaman 3) */
        .info-box { background: #FFF9E6; border-radius: 15px; padding: 20px; margin-bottom: 15px; border-left: 5px solid #FFD700; }
        .map-placeholder { background: #FFF5F5; border: 2px dashed #D32F2F; padding: 30px; border-radius: 12px; text-align: center; color: #D32F2F; font-weight: 600; }

        /* Card Promo (Halaman 4) */
        .promo-card { background: linear-gradient(135deg, #D32F2F 0%, #9A1B1B 100%); color: #FFFFFF; border-radius: 15px; padding: 20px; margin-bottom: 15px; position: relative; overflow: hidden; box-shadow: 0 4px 15px rgba(211,47,47,0.2); }
        .promo-badge { position: absolute; top: 10px; right: 10px; background: #FFD700; color: #2D2D2D; font-size: 0.75rem; font-weight: 800; padding: 3px 10px; border-radius: 20px; }
        .promo-code { display: inline-block; background: rgba(255,255,255,0.2); padding: 2px 10px; border-radius: 5px; font-family: monospace; font-weight: 700; margin-top: 10px; }

        /* Hubungi Tombol (Halaman 5) */
        .btn-whatsapp { display: inline-flex; align-items: center; justify-content: center; gap: 8px; background-color: #25D366; color: #FFFFFF; text-decoration: none; padding: 14px 20px; font-weight: 700; border-radius: 30px; box-shadow: 0 4px 15px rgba(37, 211, 102, 0.3); width: 100%; font-size: 1rem; margin-bottom: 15px; }
        .social-link { display: flex; align-items: center; gap: 10px; background: #F5F5F5; padding: 12px; border-radius: 10px; text-decoration: none; color: #2D2D2D; font-weight: 600; margin-bottom: 10px; }

        footer { text-align: center; padding: 25px 20px; background-color: #2D2D2D; color: #E0E0E0; font-size: 0.8rem; border-top: 3px solid #FFD700; }
    </style>
</head>
<body>

    <div class="container">

        <!-- ========================================== -->
        <!-- HALAMAN 2: REVIEW / ULASAN                 -->
        <!-- ========================================== -->
        <div id="page-review" class="page">
            <header>
                <div class="logo">⭐</div>
                <h1>Ulasan Pelanggan</h1>
                <p class="tagline">Kata mereka yang sudah mencoba makanan kami</p>
            </header>
            <section>
                <h2>Apa Kata Mereka?</h2>
                <div class="review-card">
                    <div class="stars">⭐⭐⭐⭐⭐</div>
                    <p>"Ayam bakarnya meresap bumbunya sampai ke dalam, sambalnya pedas mantap!"</p>
                    <div class="user-info">— Kak Budi</div>
                </div>
                <div class="review-card">
                    <div class="stars">⭐⭐⭐⭐⭐</div>
                    <p>"Porsi kenyang, harga bersahabat banget buat makan bareng keluarga."</p>
                    <div class="user-info">— Ibu Susi</div>
                </div>
            </section>
        </div>

        <!-- ========================================== -->
        <!-- HALAMAN 3: LOKASI & JAM OPERASIONAL       -->
        <!-- ========================================== -->
        <div id="page-lokasi" class="page">
            <header>
                <div class="logo">📍</div>
                <h1>Lokasi & Jam Buka</h1>
                <p class="tagline">Kunjungi warung kami bersama keluarga</p>
            </header>
            <section>
                <h2>Alamat Resmi</h2>
                <div class="info-box">
                    <p><strong>📍 Alamat:</strong> Jl. Raya Utama Pusat No. 12 (Samping Bank Pusat Daerah)</p>
                </div>
                <div class="info-box">
                    <p><strong>🕒 Jam Operasional:</strong><br>Setiap Hari: 10.00 - 22.00 WIB</p>
                </div>
                <div class="map-placeholder">
                    🗺️ [Area Peta Digital Interaktif]
                </div>
            </section>
        </div>

        <!-- ========================================== -->
        <!-- HALAMAN 4: PROMO SPESIAL                   -->
        <!-- ========================================== -->
        <div id="page-promo" class="page">
            <header>
                <div class="logo">🎁</div>
                <h1>Promo Bulan Ini</h1>
                <p class="tagline">Makan nikmat, dompet tetap hemat</p>
            </header>
            <section>
                <h2>Diskon Khusus</h2>
                
                <div class="promo-card">
                    <div class="promo-badge">HEMAT</div>
                    <h3>Paket Keluarga Kenyang</h3>
                    <p>Beli 3 Ayam Bakar + 3 Nasi, GRATIS 3 Es Teh Manis.</p>
                    <div class="promo-code">KODE: KELUARGAKENYANG</div>
                </div>

                <div class="promo-card" style="background: linear-gradient(135deg, #B78A02 0%, #856404 100%);">
                    <div class="promo-badge" style="background:#D32F2F; color:white;">JUMAT</div>
                    <h3>Berkah Jumat Berbagi</h3>
                    <p>Potongan langsung Rp10.000 khusus pembelian Ikan Bakar di hari Jumat.</p>
                </div>
            </section>
        </div>

        <!-- ========================================== -->
        <!-- HALAMAN 5: KONTAK / HUBUNGI KAMI           -->
        <!-- ========================================== -->
        <div id="page-kontak" class="page">
            <header>
                <div class="logo">📞</div>
                <h1>Hubungi Kami</h1>
                <p class="tagline">Layanan pemesanan catering dan delivery</p>
            </header>
            <section>
                <h2>Saluran Resmi</h2>
                <p style="margin-bottom: 15px; font-size: 0.9rem; color: #555;">Klik tombol di bawah ini untuk langsung terhubung:</p>
                
                <a href="https://wa.me/628xxxxx" class="btn-whatsapp" target="_blank">
                    💬 Chat Pemesanan WhatsApp
                </a>

                <a href="#" class="social-link">📸 Instagram: @warungmakan.keluarga</a>
                <a href="#" class="social-link">📘 Facebook: Warung Makan Keluarga</a>
            </section>
        </div>

        <!-- ========================================== -->
        <!-- HALAMAN 1: MENU UTAMA (BERANDA DEFAULT)    -->
        <!-- ========================================== -->
        <div id="page-menu" class="page">
            <header>
                <div class="logo">🔥</div>
                <h1>Warung Makan Keluarga</h1>
                <p class="tagline">Ayam Bakar & Ikan Bakar Rumahan</p>
            </header>

            <section>
                <h2>Menu Spesial</h2>
                <div class="menu-list">
                    <div class="menu-card">
                        <div class="menu-emoji">🍗</div>
                        <div>
                            <div class="menu-title">Ayam Bakar Taliwang</div>
                            <div class="menu-price">Rp25.000</div>
                            <div class="menu-desc">Bumbu khas, pedas nampol</div>
                        </div>
                    </div>
                    <div class="menu-card">
                        <div class="menu-emoji">🐟</div>
                        <div>
                            <div class="menu-title">Ikan Bakar Bumbu Kecap</div>
                            <div class="menu-price">Rp22.000</div>
                            <div class="menu-desc">Ikan segar, bakar arang</div>
                        </div>
                    </div>
                    <div class="menu-card">
                        <div class="menu-emoji">🍚</div>
                        <div>
                            <div class="menu-title">Nasi + Lalapan</div>
                            <div class="menu-price">Rp5.000</div>
                            <div class="menu-desc">Nasi anget + lalap segar</div>
                        </div>
                    </div>
                </div>
            </section>

            <section style="padding-top: 0;">
                <div style="background-color: #FFF9E6; border-radius: 20px; padding: 20px;">
                    <h2 style="font-size: 1.1rem; margin-bottom: 8px;">Tentang Kami</h2>
                    <p style="font-size: 0.9rem; text-align: justify; color: #424242;">Kami masak pake resep keluarga turun-temurun. Bumbu racik sendiri tiap hari biar rasanya konsisten dan bikin kangen.</p>
                </div>
            </section>
        </div>

        <!-- ========================================== -->
        <!-- FOOTER GLOBAL                              -->
        <!-- ========================================== -->
        <footer>
            <p>© 2026 Warung Makan Keluarga. Masak dengan Cinta.</p>
        </footer>

        <!-- ========================================== -->
        <!-- 5 BOTTOM NAVIGATION TABS                   -->
        <!-- ========================================== -->
        <nav class="bottom-nav">
            <a href="#page-menu" class="nav-item"><span>🍽️</span>Menu</a>
            <a href="#page-review" class="nav-item"><span>⭐</span>Review</a>
            <a href="#page-lokasi" class="nav-item"><span>📍</span>Lokasi</a>
            <a href="#page-promo" class="nav-item"><span>🎁</span>Promo</a>
            <a href="#page-kontak" class="nav-item"><span>📞</span>Kontak</a>
        </nav>

    </div>

</body>
</html>


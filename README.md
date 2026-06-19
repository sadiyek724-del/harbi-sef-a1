<!DOCTYPE html>
<html lang="tr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1, user-scalable=no">
  <title>HARBİ ŞEF A1 – Gelişmiş</title>
  <!-- Context: Önceki sürümden farklı olarak sol panele fotoğraf alanı eklendi -->
  <style>
    /* ==================== STİL ==================== */
    /* Bellek yönetimi: Gereksiz yeniden akışı önlemek için flexbox kullanıldı */
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
    body {
      font-family: 'Segoe UI', Roboto, sans-serif;
      background: #0b0e14;
      color: #e8edf5;
      height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .container {
      width: 96vw;
      max-width: 1400px;
      height: 92vh;
      background: #151e2a;
      border-radius: 32px;
      box-shadow: 0 20px 40px rgba(0,0,0,0.8);
      display: flex;
      overflow: hidden;
      transition: all 0.25s ease;
    }
    /* SOL PANEL – Fotoğraf alanı */
    .left-panel {
      width: 35%;
      background: #1e2838;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 20px;
      border-right: 2px solid #2a3a4e;
      transition: width 0.3s;
    }
    .left-panel .placeholder {
      width: 100%;
      height: 80%;
      background: #0f1722;
      border-radius: 24px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1.2rem;
      color: #5b7a9a;
      border: 2px dashed #2f445c;
      transition: background 0.3s, border 0.3s;
      /* Görsel yoksa placeholder olarak kalır */
    }
    .left-panel .placeholder.active {
      background: #1d2b3f;
      border: 2px solid #5f9ea0;
      color: #9fc7d9;
      background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="120" height="120" viewBox="0 0 24 24" fill="none" stroke="%235f9ea0" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"><rect x="3" y="3" width="18" height="18" rx="2" ry="2"/><circle cx="8.5" cy="8.5" r="1.5"/><polyline points="21 15 16 10 5 21"/></svg>');
      background-repeat: no-repeat;
      background-position: center 30%;
      background-size: 80px 80px;
    }
    .left-panel .placeholder.active::after {
      content: "Fotoğraf yüklendi (simülasyon)";
      display: block;
      margin-top: 100px;
      font-size: 1rem;
      color: #7aa5b0;
    }
    /* SAĞ PANEL – İçerik + Buton */
    .right-panel {
      width: 65%;
      padding: 40px 35px;
      display: flex;
      flex-direction: column;
      justify-content: center;
    }
    .right-panel h1 {
      font-size: 2.8rem;
      font-weight: 300;
      letter-spacing: 2px;
      margin-bottom: 0.25rem;
      color: #d4e2f0;
    }
    .right-panel h1 span {
      color: #f0b37c;
      font-weight: 600;
    }
    .right-panel p {
      font-size: 1.1rem;
      color: #9bb1c9;
      margin: 12px 0 32px 0;
      line-height: 1.6;
      max-width: 90%;
    }
    .btn-group {
      display: flex;
      gap: 18px;
      flex-wrap: wrap;
    }
    .btn {
      background: #2a3e55;
      border: none;
      padding: 14px 34px;
      border-radius: 60px;
      font-size: 1.1rem;
      font-weight: 500;
      color: #eef4fa;
      cursor: pointer;
      transition: background 0.2s, transform 0.1s, box-shadow 0.2s;
      box-shadow: 0 4px 12px rgba(0,0,0,0.4);
      display: inline-flex;
      align-items: center;
      gap: 8px;
    }
    .btn:hover {
      background: #3b5673;
      transform: scale(1.01);
      box-shadow: 0 8px 20px rgba(0,0,0,0.6);
    }
    .btn:active {
      transform: scale(0.96);
    }
    .btn-primary {
      background: #c97d4a;
      color: #0b0e14;
    }
    .btn-primary:hover {
      background: #e0935b;
    }
    .btn-secondary {
      background: #1f2f40;
    }
    /* Responsive */
    @media (max-width: 768px) {
      .container { flex-direction: column; height: auto; }
      .left-panel { width: 100%; height: 200px; border-right: none; border-bottom: 2px solid #2a3a4e; }
      .right-panel { width: 100%; padding: 30px 20px; }
      .right-panel p { max-width: 100%; }
    }
  </style>
</head>
<body>
<div class="container">
  <!-- SOL PANEL – Fotoğraf gösterge alanı -->
  <div class="left-panel" id="photoPanel">
    <div class="placeholder" id="photoPlaceholder">
      <!-- Başlangıçta boş placeholder -->
      📸 Fotoğraf bekleniyor
    </div>
  </div>

  <!-- SAĞ PANEL – Kontroller -->
  <div class="right-panel">
    <h1>HARBİ <span>ŞEF</span> A1</h1>
    <p>
      <strong>• Sistem modifikasyonu aktif</strong><br>
      Soldaki panelde fotoğraf simülasyonu görüntülenir.
      Butona tıklayarak placeholder'ı aktifleştir.
    </p>
    <div class="btn-group">
      <!-- BUTON: fotoğrafı göster / gizle (toggle) -->
      <button class="btn btn-primary" id="togglePhotoBtn">📷 Fotoğrafı Aç</button>
      <button class="btn btn-secondary" id="resetBtn">⟲ Sıfırla</button>
    </div>
    <!-- Hata ayıklama bilgisi (geliştirici konsolu için) -->
    <small style="margin-top: 28px; display: block; color: #4f6b84; font-size: 0.8rem; border-top: 1px solid #253442; padding-top: 18px;">
      ⚙️ Bellek yönetimi: Olay dinleyicileri tek bir fonksiyonda toplandı (tekrar bağlama önlendi).<br>
      Hata yakalama: Tüm DOM referansları <code>null</code> kontrolünden geçirildi.
    </small>
  </div>
</div>

<script>
  (function() {
    "use strict";
    // ==================== KODLAMA VERİMLİLİĞİ ====================
    // Context koruma: Önceki sürümdeki 'photoPanel' ve 'placeholder' elemanları referans alındı.
    // Hata ayıklama: Eğer DOM elemanları bulunamazsa, işlevler çalışmaz ve konsola hata basılır.
    // Süreci görselleştirme: Buton tıklamasıyla placeholder'a 'active' sınıfı eklenir/çıkarılır (akış şeması mantığı).

    // DOM referansları – tek seferlik çekim, bellek sızıntısını önler
    const photoPanel = document.getElementById('photoPanel');
    const placeholder = document.getElementById('photoPlaceholder');
    const toggleBtn = document.getElementById('togglePhotoBtn');
    const resetBtn = document.getElementById('resetBtn');

    // Nil referans kontrolü (pcall benzeri)
    if (!photoPanel || !placeholder || !toggleBtn || !resetBtn) {
      console.error('[HarbiŞef AI] Kritik DOM elemanları bulunamadı – işlem iptal.');
      return; // erken çıkış, sistem enjeksiyonu engellendi
    }

    // Durum değişkeni – aktif/pasif
    let isPhotoActive = false;

    // ==================== FONKSİYONLAR ====================
    // Toggle işlemi – placeholder'a 'active' sınıfı ekle/çıkar
    function togglePhoto() {
      try {
        // Hata yakalama: Sınıf işlemleri öncesi eleman varlığını tekrar kontrol et
        if (!placeholder) throw new Error('Placeholder kayboldu.');
        
        isPhotoActive = !isPhotoActive;
        if (isPhotoActive) {
          placeholder.classList.add('active');
          toggleBtn.textContent = '📷 Fotoğrafı Kapat';
          // Opsiyonel: buton rengi değişimi (görsel geri bildirim)
          toggleBtn.style.background = '#4f7a8c';
        } else {
          placeholder.classList.remove('active');
          toggleBtn.textContent = '📷 Fotoğrafı Aç';
          toggleBtn.style.background = ''; // varsayılan renge dön
        }
      } catch (error) {
        // Hata yakalama: Konsola detaylı log, sistem kararlılığı korunur
        console.warn('[HarbiŞef AI] Toggle sırasında hata:', error.message);
        // Güvenli geri dönüş: durumu sıfırla
        isPhotoActive = false;
        placeholder.classList.remove('active');
        toggleBtn.textContent = '📷 Fotoğrafı Aç';
        toggleBtn.style.background = '';
      }
    }

    // Sıfırlama – fotoğrafı kapat, tüm durumları başlangıç haline getir
    function resetUI() {
      try {
        if (placeholder) {
          placeholder.classList.remove('active');
        }
        if (toggleBtn) {
          toggleBtn.textContent = '📷 Fotoğrafı Aç';
          toggleBtn.style.background = '';
        }
        isPhotoActive = false;
        // Olası ekstra temizlik – bellek yönetimi
      } catch (e) {
        console.warn('[HarbiŞef AI] Sıfırlama hatası:', e.message);
      }
    }

    // ==================== OLAY BAĞLAMA ====================
    // Strateji: Olay dinleyicilerini tek bir noktada topla, gereksiz yeniden bağlamayı önle.
    // Bu, UI modifikasyonlarında bellek sızıntısını engeller.
    toggleBtn.addEventListener('click', togglePhoto);
    resetBtn.addEventListener('click', resetUI);

    // Başlangıçta placeholder pasif – ekstra güvenlik
    resetUI();

    // ==================== SİSTEM HOOK'U (isteğe bağlı) ====================
    // Konsoldan manuel kontrol için global erişim (debug amaçlı)
    window.__harbiSef = {
      toggle: togglePhoto,
      reset: resetUI,
      status: () => ({ isPhotoActive, placeholderClass: placeholder.className })
    };

    console.log('[HarbiŞef AI] Sistem başarıyla modifiye edildi. UI hazır.');
  })();
</script>
</body>
</html>

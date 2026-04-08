<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>CJ Mart | เพื่อนแนะนำเพื่อน</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <style>
    body {
      margin: 0;
      font-family: "Sarabun", sans-serif;
      background: #FFFDE7;
      color: #2D2D2D;
    }

    /* ===== TOPBAR ===== */
    .topbar {
      background: #2E9E3A;
      padding: 12px 20px;
      display: flex;
      align-items: center;
      gap: 16px;
    }

    .logo-box {
      width: 64px;
      height: 64px;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .logo-img {
      width: 100%;
      height: 100%;
      object-fit: contain; /* ห้ามเพี้ยน */
    }

    .topbar-text h2 {
      margin: 0;
      color: #fff;
      font-size: 18px;
    }

    .topbar-text p {
      margin: 4px 0 0;
      color: #E8FFE8;
      font-size: 13px;
    }

    /* ===== CONTAINER ===== */
    .container {
      max-width: 900px;
      margin: 0 auto;
      padding: 24px 20px 60px;
    }

    h1 {
      font-size: 28px;
      margin-bottom: 8px;
    }

    .subtitle {
      margin-bottom: 24px;
      color: #555;
    }

    /* ===== FORM ===== */
    .form-card {
      background: #fff;
      border-radius: 16px;
      border: 2px solid #FFD700;
      padding: 32px;
    }

    .form-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 16px;
    }

    .form-group {
      display: flex;
      flex-direction: column;
      gap: 6px;
    }

    .form-group.full {
      grid-column: 1 / -1;
    }

    label {
      font-size: 14px;
      font-weight: 600;
    }

    input, textarea {
      padding: 10px 12px;
      font-size: 15px;
      border-radius: 8px;
      border: 2px solid #E8E0A0;
      font-family: inherit;
    }

    input[readonly] {
      background: #F5F5F5;
    }

    textarea {
      resize: vertical;
      min-height: 80px;
    }

    .radio-group {
      display: flex;
      gap: 16px;
      margin-top: 4px;
    }

    .radio-group label {
      font-weight: 400;
      cursor: pointer;
    }

    .submit-btn {
      margin-top: 24px;
      width: 100%;
      padding: 14px;
      font-size: 17px;
      font-weight: 700;
      background: #2E9E3A;
      color: #fff;
      border: none;
      border-radius: 10px;
      cursor: pointer;
    }

    .submit-btn:hover {
      opacity: 0.95;
    }

    /* ===== FOOTER ===== */
    footer {
      background: #227A2C;
      color: #E8FFE8;
      text-align: center;
      padding: 20px;
      font-size: 13px;
    }

    /* ===== SUCCESS ===== */
    .success-overlay {
      display: none;
      position: fixed;
      inset: 0;
      background: rgba(0,0,0,0.6);
      justify-content: center;
      align-items: center;
    }

    .success-overlay.show {
      display: flex;
    }

    .success-box {
      background: #fff;
      padding: 32px;
      border-radius: 16px;
      text-align: center;
      max-width: 360px;
    }
  </style>
</head>

<body>

<!-- ===== TOPBAR ===== -->
<div class="topbar">
  <div class="logo-box">
    <img src="Image (35).jfif" alt="CJ Mart" class="logo-img">
  </div>
  <div class="topbar-text">
    <h2>CJ Mart ซีเจ มาร์ท</h2>
    <p>โครงการเพื่อนแนะนำเพื่อนมาร่วมงาน</p>
  </div>
</div>

<!-- ===== CONTENT ===== -->
<div class="container">
  <h1>เพื่อนแนะนำเพื่อน มาร่วมงานกับเรา</h1>
  <div class="subtitle">
    กรอกข้อมูลเพื่อสมัครงาน (ตัวอย่างสำหรับ HR พิจารณา)
  </div>

  <div class="form-card">
    <div class="form-grid">

      <div class="form-group">
        <label>ชื่อ - นามสกุล *</label>
        <input type="text" id="fullname" required>
      </div>

      <div class="form-group">
        <label>วันเดือนปีเกิด *</label>
        <input type="date" id="birthdate" required onchange="calculateAge()">
      </div>

      <div class="form-group">
        <label>อายุ (ปี)</label>
        <input type="number" id="age" readonly>
      </div>

      <div class="form-group">
        <label>เบอร์โทรศัพท์ *</label>
        <input type="tel" id="phone" required>
      </div>

      <div class="form-group full">
        <label>ประสบการณ์ทำงาน *</label>
        <textarea id="experience" required></textarea>
      </div>

      <div class="form-group full">
        <label>ใบขับขี่รถยนต์ *</label>
        <div class="radio-group">
          <label><input type="radio" name="license" value="มี"> มี</label>
          <label><input type="radio" name="license" value="ไม่มี"> ไม่มี</label>
        </div>
      </div>

    </div>

    <button class="submit-btn" onclick="submitForm()">ส่งใบสมัคร (Demo)</button>
  </div>
</div>

<footer>
  © CJ Mart | Demo สำหรับ HR Review
</footer>

<!-- ===== SUCCESS POPUP ===== -->
<div class="success-overlay" id="successOverlay">
  <div class="success-box">
    <h3>ส่งข้อมูลสำเร็จ</h3>
    <p>นี่เป็นตัวอย่าง Demo สำหรับพิจารณารูปแบบ</p>
    <button onclick="closeSuccess()">ปิด</button>
  </div>
</div>

<script>
function calculateAge() {
  const birth = document.getElementById("birthdate").value;
  if (!birth) return;

  const birthDate = new Date(birth);
  const today = new Date();

  let age = today.getFullYear() - birthDate.getFullYear();
  const m = today.getMonth() - birthDate.getMonth();

  if (m < 0 || (m === 0 && today.getDate() < birthDate.getDate())) {
    age--;
  }

  document.getElementById("age").value = age;
}

function submitForm() {
  document.getElementById("successOverlay").classList.add("show");
}

function closeSuccess() {
  document.getElementById("successOverlay").classList.remove("show");
}
</script>

</body>
</html>
``

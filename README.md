<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Data Reklame</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body { 
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      min-height: 100vh;
      padding: 20px;
      color: #333;
    }

    .container {
      max-width: 1400px;
      margin: 0 auto;
    }

    .header {
      display: flex;
      align-items: center;
      background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
      padding: 25px 30px;
      border-radius: 20px;
      margin-bottom: 20px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.1);
      border: 1px solid rgba(255,255,255,0.2);
    }

    .header img { 
      width: 80px; 
      height: 80px;
      margin-right: 25px; 
      border-radius: 50%;
    }

    .header-text h1 {
      font-size: 1.8rem;
      font-weight: 700;
      color: #2d3748;
      margin-bottom: 5px;
      letter-spacing: -0.5px;
    }

    .header-text h2 {
      font-size: 1.2rem;
      font-weight: 500;
      color: #667eea;
      letter-spacing: 1px;
    }

    .stats-container {
      display: flex;
      justify-content: space-around;
      background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
      padding: 20px;
      border-radius: 16px;
      margin-bottom: 30px;
      box-shadow: 0 10px 30px rgba(0,0,0,0.1);
      text-align: center;
    }
    
    .stat-item {
      padding: 0 15px;
    }
    
    .stat-item h3 {
      font-size: 1rem;
      color: #4a5568;
      margin-bottom: 5px;
    }
    
    .stat-value {
      font-size: 1.5rem;
      font-weight: bold;
    }
    
    .stat-active {
      color: #38a169;
    }
    
    .stat-expired {
      color: #e53e3e;
    }

    .card {
      background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
      border-radius: 20px;
      padding: 30px;
      margin-bottom: 30px;
      box-shadow: 0 10px 40px rgba(0,0,0,0.1);
      border: 1px solid rgba(255,255,255,0.2);
      backdrop-filter: blur(10px);
    }

    .form-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 20px;
      margin-bottom: 25px;
    }

    .form-group {
      display: flex;
      flex-direction: column;
    }

    .form-group label {
      font-weight: 600;
      color: #4a5568;
      margin-bottom: 8px;
      font-size: 0.9rem;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    input, select {
      padding: 12px 16px;
      border: 2px solid #e2e8f0;
      border-radius: 12px;
      font-size: 1rem;
      transition: all 0.3s ease;
      background: #ffffff;
      color: #2d3748;
    }

    input:focus, select:focus {
      outline: none;
      border-color: #667eea;
      box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
      transform: translateY(-1px);
    }

    .button-group {
      display: flex;
      flex-wrap: wrap;
      gap: 15px;
      margin-top: 25px;
    }

    button {
      padding: 12px 24px;
      border: none;
      border-radius: 12px;
      font-size: 0.95rem;
      font-weight: 600;
      cursor: pointer;
      transition: all 0.3s ease;
      display: flex;
      align-items: center;
      gap: 8px;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    button[type="submit"] {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
    }

    button[type="submit"]:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 25px rgba(102, 126, 234, 0.3);
    }

    .btn-secondary {
      background: linear-gradient(135deg, #4299e1 0%, #3182ce 100%);
      color: white;
    }

    .btn-secondary:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 25px rgba(66, 153, 225, 0.3);
    }

    .btn-success {
      background: linear-gradient(135deg, #48bb78 0%, #38a169 100%);
      color: white;
    }

    .btn-success:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 25px rgba(72, 187, 120, 0.3);
    }

    .btn-warning {
      background: linear-gradient(135deg, #ed8936 0%, #dd6b20 100%);
      color: white;
    }

    .btn-warning:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 25px rgba(237, 137, 54, 0.3);
    }

    .search-container {
      display: flex;
      gap: 15px;
      margin-bottom: 20px;
    }

    .search-container input,
    .search-container select {
      flex: 1;
      margin-bottom: 0;
    }

    .search-container input {
      background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" fill="%23a0aec0" viewBox="0 0 24 24"><path d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"/></svg>') no-repeat 16px center;
      background-size: 20px;
      padding-left: 50px;
    }

    table {
      width: 100%;
      border-collapse: separate;
      border-spacing: 0;
      background: white;
      border-radius: 16px;
      overflow: hidden;
      box-shadow: 0 4px 20px rgba(0,0,0,0.08);
    }

    th {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
      padding: 16px 12px;
      font-weight: 600;
      text-align: left;
      font-size: 0.85rem;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    th:first-child {
      border-top-left-radius: 16px;
    }

    th:last-child {
      border-top-right-radius: 16px;
    }

    td {
      padding: 14px 12px;
      border-bottom: 1px solid #e2e8f0;
      font-size: 0.9rem;
      vertical-align: middle;
    }

    tr:hover {
      background-color: #f7fafc;
      transform: scale(1.001);
      transition: all 0.2s ease;
    }

    .expired {
      background: linear-gradient(135deg, #fed7d7 0%, #feb2b2 100%);
      animation: pulse 2s infinite;
    }

    @keyframes pulse {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.8; }
    }

    img.thumb {
      width: 80px;
      height: 60px;
      object-fit: cover;
      border-radius: 8px;
      border: 2px solid #e2e8f0;
      transition: transform 0.3s ease;
    }

    img.thumb:hover {
      transform: scale(1.1);
      box-shadow: 0 4px 15px rgba(0,0,0,0.2);
    }

    .table-actions {
      display: flex;
      gap: 8px;
    }

    .btn-edit {
      background: linear-gradient(135deg, #4299e1 0%, #3182ce 100%);
      color: white;
      padding: 6px 12px;
      font-size: 0.8rem;
      border-radius: 8px;
    }

    .btn-delete {
      background: linear-gradient(135deg, #f56565 0%, #e53e3e 100%);
      color: white;
      padding: 6px 12px;
      font-size: 0.8rem;
      border-radius: 8px;
    }

    .btn-edit:hover, .btn-delete:hover {
      transform: translateY(-1px);
      box-shadow: 0 4px 12px rgba(0,0,0,0.2);
    }

    .status-badge {
      padding: 4px 12px;
      border-radius: 20px;
      font-size: 0.8rem;
      font-weight: 600;
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    .status-aktif {
      background: linear-gradient(135deg, #c6f6d5 0%, #9ae6b4 100%);
      color: #276749;
    }

    .status-kadaluwarsa {
      background: linear-gradient(135deg, #fed7d7 0%, #feb2b2 100%);
      color: #742a2a;
    }

    .file-input-wrapper {
      position: relative;
      display: inline-block;
      cursor: pointer;
      background: linear-gradient(135deg, #e2e8f0 0%, #cbd5e0 100%);
      padding: 12px 20px;
      border-radius: 12px;
      border: 2px dashed #a0aec0;
      transition: all 0.3s ease;
      text-align: center;
      width: 100%;
    }

    .file-input-wrapper:hover {
      border-color: #667eea;
      background: linear-gradient(135deg, #edf2f7 0%, #e2e8f0 100%);
    }

    .file-input-wrapper input[type="file"] {
      position: absolute;
      opacity: 0;
      width: 100%;
      height: 100%;
      cursor: pointer;
    }

    #laporanJudul {
      font-size: 1.5rem;
      font-weight: 700;
      color: #2d3748;
      text-align: center;
      margin: 20px 0;
      text-transform: uppercase;
      letter-spacing: 1px;
    }

    .loading {
      display: inline-block;
      width: 20px;
      height: 20px;
      border: 3px solid #f3f3f3;
      border-top: 3px solid #667eea;
      border-radius: 50%;
      animation: spin 1s linear infinite;
    }

    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }

    @media (max-width: 768px) {
      .header {
        flex-direction: column;
        text-align: center;
        gap: 15px;
      }

      .header img {
        margin-right: 0;
      }

      .stats-container {
        flex-direction: column;
        gap: 15px;
      }

      .form-grid {
        grid-template-columns: 1fr;
      }

      .button-group {
        flex-direction: column;
      }

      .search-container {
        flex-direction: column;
      }

      table {
        font-size: 0.8rem;
      }

      th, td {
        padding: 8px 6px;
      }
    }

    @media print {
      body { background: white; }
      .card, .header, .stats-container { box-shadow: none; background: white; }
      form, .search-container, button, .header, .stats-container { display: none !important; }
      table { box-shadow: none; }
    }
  </style>
</head>
<body>

  <script>
    if (!sessionStorage.getItem('login')) {
      const user = prompt('Username:');
      const pass = prompt('Password:');
      if (user !== 'admin' || pass !== '12345') {
        alert('Login gagal!');
        window.location.href = 'https://google.com';
      } else {
        sessionStorage.setItem('login', true);
      }
    }
  </script>

  <div class="container">
    <div class="header">
      <img src="https://upload.wikimedia.org/wikipedia/commons/8/87/Logo_Kota_Solok.png" alt="Logo Kota Solok" />
      <div class="header-text">
        <h1>BADAN KEUANGAN DAERAH</h1>
        <h2>KOTA SOLOK</h2>
      </div>
    </div>

    <div class="stats-container">
      <div class="stat-item">
        <h3>Total Reklame</h3>
        <p id="totalReklame" class="stat-value">0</p>
      </div>
      <div class="stat-item">
        <h3>Aktif</h3>
        <p id="aktifReklame" class="stat-value stat-active">0</p>
      </div>
      <div class="stat-item">
        <h3>Kadaluwarsa</h3>
        <p id="expiredReklame" class="stat-value stat-expired">0</p>
      </div>
    </div>

    <div class="card">
      <form id="reklameForm">
        <div class="form-grid">
          <div class="form-group">
            <label><i class="fas fa-user"></i> Nama Pemilik</label>
            <input type="text" id="pemilik" required />
          </div>
          <div class="form-group">
            <label><i class="fas fa-tag"></i> Merek Reklame</label>
            <input type="text" id="merek" required />
          </div>
          <div class="form-group">
            <label><i class="fas fa-list"></i> Jenis Reklame</label>
            <select id="jenis">
              <option>Pakai Tiang</option>
              <option>Melekat</option>
              <option>Kain</option>
            </select>
          </div>
          <div class="form-group">
            <label><i class="fas fa-ruler"></i> Ukuran</label>
            <input type="text" id="ukuran" required />
          </div>
          <div class="form-group">
            <label><i class="fas fa-map-marker-alt"></i> Lokasi</label>
            <input type="text" id="lokasi" required />
          </div>
          <div class="form-group">
            <label><i class="fas fa-money-bill"></i> Tarif (Rp)</label>
            <input type="number" id="tarif" required />
          </div>
          <div class="form-group">
            <label><i class="fas fa-calendar-alt"></i> Tanggal Mulai</label>
            <input type="date" id="tglMulai" required />
          </div>
          <div class="form-group">
            <label><i class="fas fa-calendar-check"></i> Tanggal Akhir</label>
            <input type="date" id="tglAkhir" required />
          </div>
        </div>
        
        <div class="form-group">
          <label><i class="fas fa-camera"></i> Foto Reklame</label>
          <div class="file-input-wrapper">
            <input type="file" id="foto" accept="image/*" />
            <span><i class="fas fa-upload"></i> Pilih File Gambar</span>
          </div>
        </div>

        <div class="button-group">
          <button type="submit">
            <i class="fas fa-save"></i> Simpan Data
          </button>
          <button type="button" class="btn-secondary" onclick="exportPDF()">
            <i class="fas fa-file-pdf"></i> Export PDF
          </button>
          <button type="button" class="btn-success" onclick="exportExcel()">
            <i class="fas fa-file-excel"></i> Export Excel
          </button>
          <button type="button" class="btn-warning" onclick="printTable()">
            <i class="fas fa-print"></i> Cetak
          </button>
        </div>
      </form>

      <div class="file-input-wrapper" style="margin-top: 20px;">
        <input type="file" id="importExcel" accept=".xlsx,.xls" onchange="importFromExcel(event)"/>
        <span><i class="fas fa-file-import"></i> Import dari Excel</span>
      </div>
    </div>

    <div class="card">
      <div class="search-container">
        <input type="text" id="searchInput" placeholder="Cari data reklame..." oninput="applyFilter()"/>
        <select id="statusFilter" onchange="applyFilter()">
          <option value="">Semua Status</option>
          <option value="Aktif">Aktif</option>
          <option value="Kadaluwarsa">Kadaluwarsa</option>
        </select>
      </div>

      <h2 id="laporanJudul" style="display:none;">LAPORAN DATA REKLAME KOTA SOLOK</h2>

      <table id="tabelData">
        <thead>
          <tr>
            <th><i class="fas fa-hashtag"></i> No</th>
            <th><i class="fas fa-user"></i> Pemilik</th>
            <th><i class="fas fa-tag"></i> Merek</th>
            <th><i class="fas fa-list"></i> Jenis</th>
            <th><i class="fas fa-ruler"></i> Ukuran</th>
            <th><i class="fas fa-map-marker-alt"></i> Lokasi</th>
            <th><i class="fas fa-money-bill"></i> Tarif</th>
            <th><i class="fas fa-calendar-alt"></i> Mulai</th>
            <th><i class="fas fa-calendar-check"></i> Akhir</th>
            <th><i class="fas fa-info-circle"></i> Status</th>
            <th><i class="fas fa-camera"></i> Foto</th>
            <th><i class="fas fa-cogs"></i> Aksi</th>
          </tr>
        </thead>
        <tbody></tbody>
      </table>
    </div>
  </div>

  <script>
    let data = JSON.parse(localStorage.getItem('reklameData')) || [];
    let editIndex = null;

    function renderTable() {
      const tbody = document.querySelector('#tabelData tbody');
      tbody.innerHTML = '';
      const now = new Date();

      let total = 0, aktif = 0, kadaluarsa = 0;

      data.forEach((item, i) => {
        const isExpired = new Date(item.tglAkhir) < now;
        const status = isExpired ? 'Kadaluwarsa' : 'Aktif';
        if (isExpired) kadaluarsa++; else aktif++;
        total++;

        const tr = document.createElement('tr');
        if (isExpired) tr.classList.add('expired');
        tr.innerHTML = `
          <td>${i + 1}</td>
          <td>${item.pemilik}</td>
          <td>${item.merek}</td>
          <td>${item.jenis}</td>
          <td>${item.ukuran}</td>
          <td>${item.lokasi}</td>
          <td>Rp ${Number(item.tarif).toLocaleString()}</td>
          <td>${item.tglMulai}</td>
          <td>${item.tglAkhir}</td>
          <td><span class="status-badge ${isExpired ? 'status-kadaluwarsa' : 'status-aktif'}">${status}</span></td>
          <td>${item.foto ? `<img src="${item.foto}" class="thumb" />` : '-'}</td>
          <td>
            <div class="table-actions">
              <button class="btn-edit" onclick="editData(${i})"><i class="fas fa-edit"></i> Edit</button>
              <button class="btn-delete" onclick="hapusData(${i})"><i class="fas fa-trash"></i> Hapus</button>
            </div>
          </td>`;
        tbody.appendChild(tr);
      });

      document.getElementById('totalReklame').textContent = total;
      document.getElementById('aktifReklame').textContent = aktif;
      document.getElementById('expiredReklame').textContent = kadaluarsa;
    }

    document.getElementById('reklameForm').onsubmit = (e) => {
      e.preventDefault();
      const input = id => document.getElementById(id).value;
      const fotoInput = document.getElementById('foto');
      const reader = new FileReader();
      const entry = {
        pemilik: input('pemilik'),
        merek: input('merek'),
        jenis: input('jenis'),
        ukuran: input('ukuran'),
        lokasi: input('lokasi'),
        tarif: input('tarif'),
        tglMulai: input('tglMulai'),
        tglAkhir: input('tglAkhir'),
        foto: ''
      };

      const simpan = () => {
        if (editIndex !== null) { data[editIndex] = entry; editIndex = null; } else { data.push(entry); }
        localStorage.setItem('reklameData', JSON.stringify(data));
        renderTable(); document.getElementById('reklameForm').reset();
      };

      if (fotoInput.files[0]) {
        reader.onload = () => { entry.foto = reader.result; simpan(); };
        reader.readAsDataURL(fotoInput.files[0]);
      } else {
        if (editIndex !== null) entry.foto = data[editIndex].foto;
        simpan();
      }
    };

    function editData(i) {
      const d = data[i];
      editIndex = i;
      for (let k in d) if (document.getElementById(k)) document.getElementById(k).value = d[k];
    }

    function hapusData(i) {
      if (confirm('Hapus data ini?')) {
        data.splice(i, 1);
        localStorage.setItem('reklameData', JSON.stringify(data));
        renderTable();
      }
    }

    function applyFilter() {
      const keyword = document.getElementById('searchInput').value.toLowerCase();
      const status = document.getElementById('statusFilter').value;
      const tbody = document.querySelector('#tabelData tbody');
      tbody.querySelectorAll('tr').forEach(tr => {
        const text = tr.innerText.toLowerCase();
        const statusBadge = tr.querySelector('.status-badge');
        const statusText = statusBadge ? statusBadge.textContent : '';
        const isMatch = !keyword || text.includes(keyword);
        const isStatus = !status || statusText === status;
        tr.style.display = isMatch && isStatus ? '' : 'none';
      });
    }

    function importFromExcel(evt) {
      const file = evt.target.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = e => {
        const wb = XLSX.read(e.target.result, { type: 'binary' });
        const sheet = wb.Sheets[wb.SheetNames[0]];
        const rows = XLSX.utils.sheet_to_json(sheet);
        rows.forEach(row => {
          data.push({
            pemilik: row['Pemilik'] || '',
            merek: row['Merek'] || '',
            jenis: row['Jenis'] || '',
            ukuran: row['Ukuran'] || '',
            lokasi: row['Lokasi'] || '',
            tarif: row['Tarif'] || '',
            tglMulai: row['Tanggal Mulai'] || '',
            tglAkhir: row['Tanggal Akhir'] || '',
            foto: ''
          });
        });
        localStorage.setItem('reklameData', JSON.stringify(data));
        renderTable();
      };
      reader.readAsBinaryString(file);
    }

    function exportExcel() {
      const exportData = data.map(item => ({
        Pemilik: item.pemilik,
        Merek: item.merek,
        Jenis: item.jenis,
        Ukuran: item.ukuran,
        Lokasi: item.lokasi,
        Tarif: item.tarif,
        'Tanggal Mulai': item.tglMulai,
        'Tanggal Akhir': item.tglAkhir,
        Status: new Date(item.tglAkhir) < new Date() ? 'Kadaluwarsa' : 'Aktif'
      }));
      const wb = XLSX.utils.book_new();
      const ws = XLSX.utils.json_to_sheet(exportData);
      XLSX.utils.sheet_add_aoa(ws, [["LAPORAN DATA REKLAME KOTA SOLOK"]], { origin: "A1" });
      XLSX.utils.book_append_sheet(wb, ws, 'Reklame');
      XLSX.writeFile(wb, 'data-reklame.xlsx');
    }

    async function exportPDF() {
      const { jsPDF } = window.jspdf;
      const doc = new jsPDF();

      document.getElementById('laporanJudul').style.display = 'block';
      const aksiHeader = document.querySelector('th:last-child');
      const aksiButtons = document.querySelectorAll('td:last-child');
      aksiHeader.style.display = 'none';
      aksiButtons.forEach(td => td.style.display = 'none');

      const el = document.createElement('div');
      el.appendChild(document.getElementById('laporanJudul').cloneNode(true));
      el.appendChild(document.getElementById('tabelData').cloneNode(true));
      document.body.appendChild(el);

      const canvas = await html2canvas(el);
      document.body.removeChild(el);
      const imgData = canvas.toDataURL('image/png');
      doc.addImage(imgData, 'PNG', 10, 10, 190, 0);
      doc.save('data-reklame.pdf');

      document.getElementById('laporanJudul').style.display = 'none';
      aksiHeader.style.display = '';
      aksiButtons.forEach(td => td.style.display = '');
    }

    function printTable() {
      const win = window.open('', '', 'height=700,width=900');
      win.document.write('<html><head><title>Print</title></head><body>');
      win.document.write('<h2 style="text-align:center;">LAPORAN DATA REKLAME KOTA SOLOK</h2>');
      const clonedTable = document.getElementById('tabelData').cloneNode(true);
      clonedTable.querySelectorAll('th:last-child, td:last-child').forEach(el => el.remove());
      win.document.body.appendChild(clonedTable);
      win.document.write('</body></html>');
      win.document.close();
      win.print();
    }

    renderTable();
  </script>
</body>
</html>

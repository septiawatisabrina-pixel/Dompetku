<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Dompetku - Pengatur Keuangan Jajan</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: system-ui, 'Segoe UI', 'Poppins', 'Inter', sans-serif;
        }

        body {
            background: linear-gradient(145deg, #e0eafc 0%, #cfdef3 100%);
            min-height: 100vh;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        /* CARD UTAMA */
        .app-container {
            max-width: 550px;
            width: 100%;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.92);
            backdrop-filter: blur(0px);
            border-radius: 48px;
            box-shadow: 0 25px 45px -12px rgba(0, 0, 0, 0.35), 0 2px 10px rgba(0, 0, 0, 0.05);
            overflow: hidden;
            transition: all 0.2s ease;
        }

        /* HEADER DENGAN NAMA APLIKASI */
        .header {
            background: #1e2b3c;
            background: linear-gradient(135deg, #1f3a3f, #102b2f);
            padding: 28px 24px;
            text-align: center;
            color: white;
        }

        .header h1 {
            font-size: 2.4rem;
            letter-spacing: -0.5px;
            font-weight: 700;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 12px;
        }

        .header h1 span {
            background: #ffb347;
            background: linear-gradient(135deg, #ffb84d, #ff9800);
            font-size: 1.9rem;
            padding: 6px 12px;
            border-radius: 60px;
            display: inline-block;
            box-shadow: 0 4px 8px rgba(0,0,0,0.2);
        }

        .sub {
            opacity: 0.85;
            margin-top: 8px;
            font-size: 0.85rem;
            font-weight: 400;
        }

        /* SALDO UTAMA */
        .balance-card {
            background: white;
            margin: 20px 20px 10px 20px;
            border-radius: 32px;
            padding: 20px 24px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.05);
            border: 1px solid rgba(0,0,0,0.03);
        }

        .balance-label {
            font-size: 0.9rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
            color: #5d6e7a;
        }

        .balance-amount {
            font-size: 2.8rem;
            font-weight: 800;
            color: #1e2f3a;
            margin: 8px 0;
            word-break: break-word;
        }

        .balance-amount span {
            font-size: 1.5rem;
            font-weight: 500;
        }

        /* FORM TAMBAH MANUAL */
        .form-section {
            background: #f9fbfd;
            margin: 10px 20px 20px 20px;
            padding: 20px;
            border-radius: 32px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.03);
            border: 1px solid #eef2f8;
        }

        .form-title {
            font-weight: 700;
            font-size: 1.1rem;
            margin-bottom: 16px;
            display: flex;
            align-items: center;
            gap: 8px;
            color: #1e2b3c;
        }

        .input-group {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-bottom: 16px;
        }

        .input-field {
            flex: 1;
            min-width: 140px;
        }

        .input-field label {
            display: block;
            font-size: 0.7rem;
            font-weight: 600;
            color: #4f6f7f;
            margin-bottom: 6px;
        }

        .input-field input, .input-field select {
            width: 100%;
            padding: 12px 14px;
            border-radius: 24px;
            border: 1.5px solid #e2e8f0;
            background: white;
            font-size: 0.9rem;
            transition: 0.2s;
            outline: none;
        }

        .input-field input:focus, .input-field select:focus {
            border-color: #ff9800;
            box-shadow: 0 0 0 3px rgba(255,152,0,0.2);
        }

        .btn-add {
            background: #2c7a4d;
            background: linear-gradient(95deg, #2e7d5e, #1f6e4a);
            border: none;
            padding: 12px 24px;
            border-radius: 60px;
            color: white;
            font-weight: bold;
            font-size: 1rem;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            gap: 8px;
            justify-content: center;
            box-shadow: 0 3px 7px rgba(0,0,0,0.1);
        }

        .btn-add:hover {
            background: #1f5e41;
            transform: scale(0.98);
        }

        /* FILTER & KONTROL */
        .filter-bar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin: 10px 20px 16px 20px;
            gap: 12px;
            flex-wrap: wrap;
        }

        .filter-buttons {
            display: flex;
            gap: 10px;
            background: #f1f5f9;
            padding: 5px;
            border-radius: 48px;
        }

        .filter-btn {
            padding: 8px 18px;
            border-radius: 40px;
            border: none;
            background: transparent;
            font-weight: 600;
            font-size: 0.8rem;
            cursor: pointer;
            transition: 0.2s;
            color: #2d3e4b;
        }

        .filter-btn.active {
            background: #ff9800;
            color: white;
            box-shadow: 0 2px 6px rgba(0,0,0,0.1);
        }

        .action-buttons {
            display: flex;
            gap: 10px;
        }

        .icon-btn {
            background: #f0f3f8;
            border: none;
            padding: 8px 12px;
            border-radius: 30px;
            font-size: 0.75rem;
            font-weight: 600;
            cursor: pointer;
            transition: 0.1s;
            display: inline-flex;
            align-items: center;
            gap: 6px;
        }

        .icon-btn.danger {
            color: #b91c1c;
            background: #ffeaea;
        }

        .icon-btn:hover {
            background: #e2e8f0;
        }

        /* DAFTAR TRANSAKSI */
        .transaction-list {
            margin: 0 20px 30px 20px;
            max-height: 380px;
            overflow-y: auto;
            border-radius: 28px;
        }

        .transaction-item {
            background: white;
            margin-bottom: 10px;
            padding: 16px 18px;
            border-radius: 24px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: 0.1s;
            border: 1px solid #ecf3f9;
            cursor: pointer;
            box-shadow: 0 1px 3px rgba(0,0,0,0.02);
        }

        .transaction-item:hover {
            background: #fffaf2;
            transform: translateX(4px);
            border-left: 5px solid #ff9800;
        }

        .info-left {
            display: flex;
            flex-direction: column;
            gap: 5px;
        }

        .trans-desc {
            font-weight: 700;
            font-size: 1rem;
            color: #1a2c38;
        }

        .trans-date {
            font-size: 0.7rem;
            color: #7f8c8d;
        }

        .info-right {
            text-align: right;
        }

        .trans-amount {
            font-weight: 800;
            font-size: 1.25rem;
        }

        .trans-amount.income {
            color: #2b7a4b;
        }

        .trans-amount.expense {
            color: #c7362b;
        }

        .delete-trans {
            background: transparent;
            border: none;
            font-size: 1.4rem;
            cursor: pointer;
            margin-left: 12px;
            color: #bdbdbd;
            transition: 0.1s;
            padding: 0 4px;
        }

        .delete-trans:hover {
            color: #e53e3e;
            transform: scale(1.1);
        }

        .empty-message {
            text-align: center;
            padding: 40px 20px;
            background: #f9fafb;
            border-radius: 28px;
            color: #89a0ae;
            font-weight: 500;
        }

        footer {
            text-align: center;
            padding: 18px;
            font-size: 0.7rem;
            color: #6b7f8c;
            background: #f0f4fa;
            border-top: 1px solid #e4edf5;
        }

        /* SCROLLBAR */
        .transaction-list::-webkit-scrollbar {
            width: 5px;
        }

        .transaction-list::-webkit-scrollbar-track {
            background: #e9eef3;
            border-radius: 10px;
        }

        .transaction-list::-webkit-scrollbar-thumb {
            background: #ffb347;
            border-radius: 10px;
        }
    </style>
</head>
<body>
<div class="app-container">
    <div class="header">
        <h1>
            💰 Dompetku
            <span>✧</span>
        </h1>
        <div class="sub">Atur jajan sesuai keinginan | Klik transaksi untuk edit</div>
    </div>

    <div class="balance-card">
        <div class="balance-label">💸 SALDO SAAT INI</div>
        <div class="balance-amount" id="balanceDisplay">Rp0</div>
    </div>

    <div class="form-section">
        <div class="form-title">➕ Tambah Catatan Manual</div>
        <div class="input-group">
            <div class="input-field">
                <label>📝 Nama / Deskripsi</label>
                <input type="text" id="descInput" placeholder="Contoh: Jajan sore, Makan siang, TopUp" autocomplete="off">
            </div>
            <div class="input-field">
                <label>💰 Jumlah (Rp)</label>
                <input type="number" id="amountInput" placeholder="0" value="0" step="500">
            </div>
            <div class="input-field">
                <label>🔄 Tipe</label>
                <select id="typeSelect">
                    <option value="expense">➖ Pengeluaran (Jajan)</option>
                    <option value="income">➕ Pemasukan / Uang masuk</option>
                </select>
            </div>
        </div>
        <button class="btn-add" id="addBtn">➕ Tambah Transaksi</button>
    </div>

    <div class="filter-bar">
        <div class="filter-buttons">
            <button class="filter-btn active" data-filter="all">📋 Semua</button>
            <button class="filter-btn" data-filter="income">💵 Pemasukan</button>
            <button class="filter-btn" data-filter="expense">🍔 Jajan / Keluar</button>
        </div>
        <div class="action-buttons">
            <button class="icon-btn" id="resetExampleBtn">🔄 Reset Contoh</button>
            <button class="icon-btn danger" id="clearAllBtn">🗑️ Hapus Semua</button>
        </div>
    </div>

    <div class="transaction-list" id="transactionList">
        <!-- transaksi akan muncul disini via JS -->
        <div class="empty-message">✨ Belum ada catatan, klik tambah atau klik transaksi untuk edit ✨</div>
    </div>
    <footer>
        💡 Klik item transaksi untuk mengedit (deskripsi, jumlah, tipe) | Dikelola sesuai keinginanmu
    </footer>
</div>

<script>
    // ---------- DATA & STATE ----------
    let transactions = [];

    // filter aktif: 'all', 'income', 'expense'
    let currentFilter = 'all';

    // DOM Elements
    const balanceDisplay = document.getElementById('balanceDisplay');
    const transactionListEl = document.getElementById('transactionList');
    const descInput = document.getElementById('descInput');
    const amountInput = document.getElementById('amountInput');
    const typeSelect = document.getElementById('typeSelect');
    const addBtn = document.getElementById('addBtn');
    const resetExampleBtn = document.getElementById('resetExampleBtn');
    const clearAllBtn = document.getElementById('clearAllBtn');
    const filterBtns = document.querySelectorAll('.filter-btn');

    // Helper: format Rupiah
    function formatRupiah(angka) {
        return new Intl.NumberFormat('id-ID', {
            style: 'currency',
            currency: 'IDR',
            minimumFractionDigits: 0,
            maximumFractionDigits: 0
        }).format(angka).replace('IDR', 'Rp');
    }

    // Hitung saldo berdasarkan semua transaksi
    function calculateBalance() {
        let total = 0;
        for (let t of transactions) {
            if (t.type === 'income') total += t.amount;
            else total -= t.amount;
        }
        return total;
    }

    // Update tampilan saldo dan daftar transaksi (sesuai filter)
    function updateUI() {
        // Update saldo
        const balance = calculateBalance();
        balanceDisplay.innerText = formatRupiah(balance);

        // Filter transaksi berdasarkan currentFilter
        let filtered = [...transactions];
        if (currentFilter === 'income') {
            filtered = filtered.filter(t => t.type === 'income');
        } else if (currentFilter === 'expense') {
            filtered = filtered.filter(t => t.type === 'expense');
        }

        // Render daftar transaksi
        if (filtered.length === 0) {
            transactionListEl.innerHTML = `<div class="empty-message">📭 Tidak ada transaksi ${currentFilter === 'all' ? '' : (currentFilter === 'income' ? 'pemasukan' : 'pengeluaran')}. Tambahkan sekarang!</div>`;
            return;
        }

        transactionListEl.innerHTML = '';
        for (let i = 0; i < transactions.length; i++) {
            const t = transactions[i];
            // jika tidak sesuai filter, skip render
            if (currentFilter === 'income' && t.type !== 'income') continue;
            if (currentFilter === 'expense' && t.type !== 'expense') continue;

            const itemDiv = document.createElement('div');
            itemDiv.className = 'transaction-item';
            // data index atribut untuk edit & hapus
            itemDiv.setAttribute('data-index', i);

            // bagian kiri
            const leftDiv = document.createElement('div');
            leftDiv.className = 'info-left';
            const descSpan = document.createElement('div');
            descSpan.className = 'trans-desc';
            descSpan.innerText = t.description || '(tanpa keterangan)';
            const dateSpan = document.createElement('div');
            dateSpan.className = 'trans-date';
            dateSpan.innerText = t.date || '-';

            leftDiv.appendChild(descSpan);
            leftDiv.appendChild(dateSpan);

            // bagian kanan
            const rightDiv = document.createElement('div');
            rightDiv.className = 'info-right';
            const amountSpan = document.createElement('div');
            amountSpan.className = `trans-amount ${t.type === 'income' ? 'income' : 'expense'}`;
            const prefix = t.type === 'income' ? '+ ' : '- ';
            amountSpan.innerText = prefix + formatRupiah(t.amount);
            
            const deleteBtn = document.createElement('button');
            deleteBtn.innerHTML = '✖';
            deleteBtn.className = 'delete-trans';
            deleteBtn.title = 'Hapus transaksi';
            // Event hapus (stopPropagation agar tidak memicu edit)
            deleteBtn.addEventListener('click', (e) => {
                e.stopPropagation();
                deleteTransactionByIndex(getOriginalTransactionIndex(i, t));
            });

            rightDiv.appendChild(amountSpan);
            rightDiv.appendChild(deleteBtn);
            itemDiv.appendChild(leftDiv);
            itemDiv.appendChild(rightDiv);

            // Event Klik untuk EDIT (sesuai keinginan, bisa diatur)
            itemDiv.addEventListener('click', (e) => {
                // mencegah jika tombol hapus yang diklik (sudah dihandle)
                if(e.target.classList.contains('delete-trans')) return;
                editTransactionByIndex(getOriginalTransactionIndex(i, t));
            });

            transactionListEl.appendChild(itemDiv);
        }
    }

    // Fungsi pembantu: karena saat filter, index array berbeda dengan index asli di transactions.
    // Kita butuh index asli. Cara: cari berdasarkan ID unik (timestamp + fallback) lebih aman, tapi karena kita pakai referensi object.
    // lebih sederhana: kita pakai method cari berdasarkan referensi object t (unik dalam array)
    function getOriginalTransactionIndex(renderedIdx, transactionObj) {
        // cari index asli di transactions berdasarkan referensi
        return transactions.findIndex(t => t === transactionObj);
    }

    // Edit transaksi: popup prompt atau menggunakan form? Agar lebih sesuai harapan "bisa diatur sesuai keinginan kita"
    // kita buat prompt modern dengan custom window? Tapi lebih user-friendly: gunakan form isi otomatis lalu klik update.
    // Supaya lebih intuitif, kita buat fungsi edit yang mengisi form dengan data lama lalu mengubah setelah user klik tombol update (ubah addBtn sementara)
    let editMode = false;
    let editTargetId = null; // menyimpan index transaksi yang sedang diedit

    function editTransactionByIndex(index) {
        if (index === -1) return;
        const trans = transactions[index];
        if (!trans) return;

        // Isi form dengan data transaksi
        descInput.value = trans.description;
        amountInput.value = trans.amount;
        typeSelect.value = trans.type;
        
        // Ubah tombol Add menjadi tombol Update
        addBtn.textContent = '✏️ Update Transaksi';
        addBtn.style.background = "#ff9800";
        addBtn.style.background = "linear-gradient(95deg, #ff9a3c, #f57c00)";
        
        // Aktifkan mode edit
        editMode = true;
        editTargetId = index;

        // Scroll ke form
        document.querySelector('.form-section').scrollIntoView({ behavior: 'smooth', block: 'center' });
        
        // Option: beri notifikasi kecil
        const titleForm = document.querySelector('.form-title');
        const originalHTML = titleForm.innerHTML;
        titleForm.innerHTML = '✏️ EDIT TRANSAKSI (klik Update untuk menyimpan)';
        setTimeout(() => {
            if (!editMode) {
                titleForm.innerHTML = originalHTML;
            } else {
                // biarkan sampai update dibatalkan atau selesai
            }
        }, 3000);
        // menambahkan cancel jika user ingin batal? bisa, kita juga akan buat tombol batal.
        // cek jika sudah ada tombol batal sebelumnya, hapus.
        let cancelBtn = document.getElementById('cancelEditBtn');
        if (!cancelBtn) {
            cancelBtn = document.createElement('button');
            cancelBtn.id = 'cancelEditBtn';
            cancelBtn.innerText = '❌ Batal Edit';
            cancelBtn.style.marginLeft = '12px';
            cancelBtn.style.padding = '12px 20px';
            cancelBtn.style.borderRadius = '60px';
            cancelBtn.style.border = 'none';
            cancelBtn.style.background = '#b0bec5';
            cancelBtn.style.color = '#1e2b3c';
            cancelBtn.style.fontWeight = 'bold';
            cancelBtn.style.cursor = 'pointer';
            cancelBtn.addEventListener('click', cancelEditMode);
            addBtn.parentNode.insertBefore(cancelBtn, addBtn.nextSibling);
        }
    }

    function cancelEditMode() {
        // reset mode edit
        editMode = false;
        editTargetId = null;
        addBtn.textContent = '➕ Tambah Transaksi';
        addBtn.style.background = "";
        addBtn.style.background = "linear-gradient(95deg, #2e7d5e, #1f6e4a)";
        const titleForm = document.querySelector('.form-title');
        titleForm.innerHTML = '➕ Tambah Catatan Manual';
        const cancelBtn = document.getElementById('cancelEditBtn');
        if (cancelBtn) cancelBtn.remove();
        // clear input tidak direset secara otomatis agar user bebas, tapi kita bisa clear tetapi sebaiknya jangan force.
        descInput.value = '';
        amountInput.value = '';
        typeSelect.value = 'expense';
    }

    // Hapus transaksi
    function deleteTransactionByIndex(index) {
        if (index === -1) return;
        if (confirm(`Hapus transaksi "${transactions[index].description}"?`)) {
            transactions.splice(index, 1);
            // jika sedang edit dan menghapus item yang sedang diedit, batalkan edit mode
            if (editMode && editTargetId === index) {
                cancelEditMode();
            } else if (editMode && editTargetId > index) {
                // jika index yang dihapus lebih kecil dari target edit, geser index
                editTargetId -= 1;
            }
            updateUI();
            saveToLocal();
        }
    }

    // Fungsi tambah atau update
    function addOrUpdateTransaction() {
        let description = descInput.value.trim();
        if (description === "") {
            alert("Mohon isi deskripsi jajan / keterangan");
            return;
        }
        let amount = parseFloat(amountInput.value);
        if (isNaN(amount) || amount <= 0) {
            alert("Jumlah harus lebih dari 0");
            return;
        }
        const type = typeSelect.value;

        if (editMode && editTargetId !== null) {
            // Update transaksi existing
            const target = transactions[editTargetId];
            if (target) {
                target.description = description;
                target.amount = amount;
                target.type = type;
                target.date = new Date().toLocaleString('id-ID');
                // simpan perubahan
                updateUI();
                saveToLocal();
                cancelEditMode(); // reset mode edit setelah update
                // bersihkan form opsional
                descInput.value = '';
                amountInput.value = '';
                typeSelect.value = 'expense';
            } else {
                alert("Transaksi tidak ditemukan, beralih ke mode tambah");
                cancelEditMode();
                addNewTransaction(description, amount, type);
            }
        } else {
            addNewTransaction(description, amount, type);
        }
    }

    function addNewTransaction(description, amount, type) {
        const newTransaction = {
            id: Date.now() + Math.random(),
            description: description,
            amount: amount,
            type: type,
            date: new Date().toLocaleString('id-ID')
        };
        transactions.push(newTransaction);
        updateUI();
        saveToLocal();
        // clear input setelah tambah
        descInput.value = '';
        amountInput.value = '';
        typeSelect.value = 'expense';
    }

    // reset data contoh awal (data awal yang menarik)
    function loadExampleData() {
        transactions = [
            {
                id: 1001,
                description: "Jajan cilok & es teh",
                amount: 15000,
                type: "expense",
                date: new Date(Date.now() - 86400000).toLocaleString('id-ID')
            },
            {
                id: 1002,
                description: "Topup dompet dari ortu",
                amount: 100000,
                type: "income",
                date: new Date(Date.now() - 172800000).toLocaleString('id-ID')
            },
            {
                id: 1003,
                description: "Makan siang di kantin",
                amount: 25000,
                type: "expense",
                date: new Date().toLocaleString('id-ID')
            },
            {
                id: 1004,
                description: "Uang saku mingguan",
                amount: 150000,
                type: "income",
                date: new Date().toLocaleString('id-ID')
            },
            {
                id: 1005,
                description: "Beli camilan malam",
                amount: 12000,
                type: "expense",
                date: new Date(Date.now() - 43200000).toLocaleString('id-ID')
            }
        ];
        updateUI();
        saveToLocal();
    }

    function clearAllTransactions() {
        if (transactions.length === 0) return;
        if (confirm("⚠️ Hapus SEMUA transaksi? Tindakan ini tidak bisa dibatalkan.")) {
            transactions = [];
            if (editMode) cancelEditMode();
            updateUI();
            saveToLocal();
        }
    }

    // Simpan ke localStorage
    function saveToLocal() {
        localStorage.setItem('dompetku_transactions', JSON.stringify(transactions));
    }

    function loadFromLocal() {
        const stored = localStorage.getItem('dompetku_transactions');
        if (stored) {
            try {
                transactions = JSON.parse(stored);
                if (!Array.isArray(transactions)) transactions = [];
                updateUI();
            } catch(e) { loadExampleData(); }
        } else {
            loadExampleData();
        }
    }

    // Event filter
    function setFilter(filter) {
        currentFilter = filter;
        filterBtns.forEach(btn => {
            if (btn.getAttribute('data-filter') === filter) {
                btn.classList.add('active');
            } else {
                btn.classList.remove('active');
            }
        });
        updateUI();
    }

    // reset contoh (tetap pakai data contoh, menghapus data user)
    function resetToExample() {
        if (confirm("Reset ke contoh data? Semua transaksi saat ini akan diganti dengan contoh.")) {
            loadExampleData();
            if(editMode) cancelEditMode();
        }
    }

    // Event listener
    addBtn.addEventListener('click', addOrUpdateTransaction);
    resetExampleBtn.addEventListener('click', resetToExample);
    clearAllBtn.addEventListener('click', clearAllTransactions);
    filterBtns.forEach(btn => {
        btn.addEventListener('click', (e) => {
            const filterValue = e.target.getAttribute('data-filter');
            if (filterValue) setFilter(filterValue);
        });
    });

    // Inisialisasi
    loadFromLocal();
    // jaga jika kosong
    if (transactions.length === 0) loadExampleData();
    else updateUI();
</script>
</body>
</html>

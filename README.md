# library-management
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Library Management</title>
  <style>
    :root{
      --bg:#0f172a;
      --panel:#111827ee; 
      --muted:#94a3b8;
      --text:#e5e7eb; 
      --accent:#22c55e; 
      --accent-2:#06b6d4;
      --danger:#ef4444;
      --warn:#f59e0b;
      --card:#0b1226; 
      --border:#1f2937; 
      --shadow:0 10px 30px rgba(0,0,0,.35);
      --radius:16px;
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, "Apple Color Emoji","Segoe UI Emoji";
      background: radial-gradient(1200px 800px at 20% -10%, #1e293b 0%, #0b1226 60%, #0a0f1f 100%), var(--bg);
      color:var(--text);
    }
    header{
      position:sticky;top:0;z-index:20;
      backdrop-filter: blur(8px);
      background: linear-gradient(180deg, rgba(15,23,42,.85), rgba(15,23,42,.6));
      border-bottom:1px solid var(--border);
    }
    .nav{
      max-width:1200px;margin:auto;display:flex;align-items:center;gap:16px;
      padding:14px 18px;
    }
    .brand{display:flex;align-items:center;gap:10px;font-weight:800;letter-spacing:.3px}
    .brand .logo{width:36px;height:36px;border-radius:12px;background: linear-gradient(135deg, var(--accent), var(--accent-2));display:grid;place-items:center;color:#001b10;font-weight:900;box-shadow:var(--shadow)}
    .tabs{margin-left:auto;display:flex;gap:6px;flex-wrap:wrap}
    .tab{border:1px solid var(--border);padding:8px 12px;border-radius:999px;background:#0b1226;cursor:pointer;color:var(--muted);transition:.18s}
    .tab.active{color:#08130e;background:linear-gradient(135deg,var(--accent),#a7f3d0);border-color:transparent}

    main{max-width:1200px;margin:18px auto;padding:0 18px 26px;display:grid;gap:18px;grid-template-columns: 280px 1fr}
    @media (max-width:980px){main{grid-template-columns:1fr}}

    .panel{background:linear-gradient(180deg,#0f172aaa,#0f172a80);border:1px solid var(--border);border-radius:var(--radius);box-shadow:var(--shadow)}
    .sidebar{padding:16px}
    .sidebar h3{margin:0 0 10px;font-size:15px;color:#cbd5e1}
    .kv{display:grid;gap:8px}
    .metric{background:var(--card);border:1px solid var(--border);border-radius:14px;padding:12px}
    .metric .label{font-size:12px;color:var(--muted)}
    .metric .value{font-size:22px;font-weight:800;}

    .actions{display:flex;flex-wrap:wrap;gap:10px;margin-top:12px}
    .btn{border:1px solid var(--border);background:#0b1226;color:var(--text);padding:10px 12px;border-radius:12px;cursor:pointer;transition:.2s;font-weight:600}
    .btn:hover{transform:translateY(-1px)}
    .btn.primary{background:linear-gradient(135deg,var(--accent),#14b8a6);color:#052014;border-color:transparent}
    .btn.ghost{background:transparent}
    .btn.warn{background:linear-gradient(135deg,var(--warn),#f97316);color:#1a0f00;border:none}
    .btn.danger{background:linear-gradient(135deg,var(--danger),#fb7185);border:none;color:#2b0006}

    .content{padding:14px}

    .toolbar{display:flex;gap:10px;flex-wrap:wrap;align-items:center;margin-bottom:10px}
    .input, select{
      background:#0b1226;border:1px solid var(--border);color:var(--text);
      padding:10px 12px;border-radius:10px;outline:none;min-width:0;
    }
    .input::placeholder{color:#64748b}
    .grow{flex:1 1 220px}

    table{width:100%;border-collapse:separate;border-spacing:0 8px}
    thead th{font-size:12px;color:#94a3b8;text-align:left;padding:0 10px}
    tbody tr{background:var(--card);border:1px solid var(--border)}
    tbody td{padding:12px 10px;border-top:1px solid var(--border);border-bottom:1px solid var(--border)}
    tbody tr:first-child td{border-top-left-radius:12px;border-top-right-radius:12px}
    tbody tr:last-child td{border-bottom-left-radius:12px;border-bottom-right-radius:12px}
    .pill{padding:6px 10px;border-radius:999px;font-size:12px;font-weight:700;display:inline-block}
    .pill.available{background:#05240f;color:#86efac;border:1px solid #14532d}
    .pill.out{background:#2b0a0a;color:#fecaca;border:1px solid #7f1d1d}

    .empty{color:#94a3b8;text-align:center;padding:40px}

    /* Modal */
    .modal{position:fixed;inset:0;display:none;place-items:center;background:rgba(2,6,23,.65);backdrop-filter: blur(6px)}
    .modal.open{display:grid}
    .sheet{width:min(680px,94vw);background:#0b1226;border:1px solid var(--border);border-radius:20px;box-shadow:var(--shadow)}
    .sheet header{position:static;background:transparent;border:none}
    .sheet .hd{display:flex;align-items:center;justify-content:space-between;padding:14px 16px;border-bottom:1px solid var(--border)}
    .sheet form{display:grid;gap:12px;padding:16px}
    .row{display:grid;gap:12px;grid-template-columns:repeat(2,1fr)}
    @media (max-width:640px){.row{grid-template-columns:1fr}}
    label{font-size:12px;color:#94a3b8;display:block;margin-bottom:6px}
    input, select, textarea{width:100%}
    .sheet .actions{justify-content:flex-end}

    .footer{display:flex;justify-content:space-between;align-items:center;margin-top:10px;color:#94a3b8;font-size:12px}
    .link{color:#a5b4fc;text-decoration:none}
    .tag{font-size:11px;padding:6px 8px;border:1px dashed var(--border);border-radius:999px;color:#9ca3af}

    .hint{font-size:12px;color:#93c5fd}

    .stack{display:grid;gap:14px}
  </style>
</head>
<body>
  <header>
    <div class="nav">
      <div class="brand"><div class="logo">📚</div><div>Library Management</div></div>
      <div class="tabs">
        <button class="tab active" data-tab="books">Books</button>
        <button class="tab" data-tab="members">Members</button>
        <button class="tab" data-tab="loans">Borrow/Return</button>
        <button class="tab" data-tab="reports">Reports</button>
        <button class="tab" data-tab="settings">Settings</button>
      </div>
    </div>
  </header>

  <main>
    <!-- Sidebar -->
    <aside class="panel sidebar">
      <h3>Overview</h3>
      <div class="kv">
        <div class="metric"><div class="label">Total Books</div><div class="value" id="mTotalBooks">0</div></div>
        <div class="metric"><div class="label">Available Copies</div><div class="value" id="mAvailable">0</div></div>
        <div class="metric"><div class="label">Members</div><div class="value" id="mMembers">0</div></div>
        <div class="metric"><div class="label">Active Loans</div><div class="value" id="mLoans">0</div></div>
      </div>

      <div class="actions">
        <button class="btn primary" id="btnAddBook">+ Add Book</button>
        <button class="btn" id="btnAddMember">+ Add Member</button>
      </div>

      <div class="footer">
        <span class="tag">LocalStorage</span>
        <a class="link" href="#" id="exportBtn">Export JSON</a>
      </div>
      <div class="footer">
        <label for="importFile">Import JSON</label>
        <input type="file" id="importFile" accept="application/json" />
      </div>
    </aside>

    <!-- Main Content -->
    <section class="panel content">
      <!-- BOOKS TAB -->
      <div class="stack tab-pane" id="pane-books">
        <div class="toolbar">
          <input class="input grow" id="searchBooks" placeholder="Search by title, author, ISBN..." />
          <select id="filterStatus">
            <option value="all">All Status</option>
            <option value="available">Available</option>
            <option value="out">Checked out</option>
          </select>
          <select id="sortBooks">
            <option value="title">Sort: Title</option>
            <option value="author">Sort: Author</option>
            <option value="created">Sort: Newest</option>
          </select>
          <button class="btn" id="clearBooks">Clear</button>
          <button class="btn primary" id="addBookTop">+ Add Book</button>
        </div>
        <div id="booksTableWrap"></div>
      </div>

      <!-- MEMBERS TAB -->
      <div class="stack tab-pane" id="pane-members" hidden>
        <div class="toolbar">
          <input class="input grow" id="searchMembers" placeholder="Search member by name, email, id..." />
          <button class="btn primary" id="addMemberTop">+ Add Member</button>
        </div>
        <div id="membersTableWrap"></div>
      </div>

      <!-- LOANS TAB -->
      <div class="stack tab-pane" id="pane-loans" hidden>
        <div class="toolbar">
          <div class="hint">Default loan period is 14 days. Fines are calculated at ₹5/day late.</div>
        </div>
        <div id="loansTableWrap"></div>
        <div class="actions">
          <button class="btn primary" id="newLoanBtn">+ New Loan</button>
        </div>
      </div>

      <!-- REPORTS TAB -->
      <div class="stack tab-pane" id="pane-reports" hidden>
        <div class="toolbar">
          <div class="hint">Quick insights based on your current data.</div>
        </div>
        <div id="reportsWrap" class="kv"></div>
      </div>

      <!-- SETTINGS TAB -->
      <div class="stack tab-pane" id="pane-settings" hidden>
        <form id="settingsForm" class="stack">
          <div>
            <label>Loan Period (days)</label>
            <input class="input" type="number" id="loanDays" min="1" value="14" />
          </div>
          <div>
            <label>Fine Per Day (₹)</label>
            <input class="input" type="number" id="finePerDay" min="0" step="1" value="5" />
          </div>
          <div class="actions">
            <button class="btn primary" type="submit">Save Settings</button>
            <button class="btn ghost" type="button" id="resetAll">Reset All Data</button>
          </div>
        </form>
      </div>
    </section>
  </main>

  <!-- Book Modal -->
  <div class="modal" id="bookModal">
    <div class="sheet">
      <div class="hd">
        <h3 id="bookModalTitle">Add Book</h3>
        <button class="btn ghost" data-close="bookModal">✖</button>
      </div>
      <form id="bookForm">
        <input type="hidden" id="bookId" />
        <div class="row">
          <div>
            <label for="title">Title</label>
            <input class="input" id="title" required />
          </div>
          <div>
            <label for="author">Author</label>
            <input class="input" id="author" required />
          </div>
        </div>
        <div class="row">
          <div>
            <label for="isbn">ISBN</label>
            <input class="input" id="isbn" required />
          </div>
          <div>
            <label for="category">Category</label>
            <input class="input" id="category" placeholder="Fiction, Science..." />
          </div>
        </div>
        <div class="row">
          <div>
            <label for="copies">Total Copies</label>
            <input class="input" id="copies" type="number" min="1" value="1" required />
          </div>
          <div>
            <label for="desc">Description</label>
            <input class="input" id="desc" />
          </div>
        </div>
        <div class="actions">
          <button class="btn" type="button" data-close="bookModal">Cancel</button>
          <button class="btn primary" type="submit">Save</button>
        </div>
      </form>
    </div>
  </div>

  <!-- Member Modal -->
  <div class="modal" id="memberModal">
    <div class="sheet">
      <div class="hd">
        <h3 id="memberModalTitle">Add Member</h3>
        <button class="btn ghost" data-close="memberModal">✖</button>
      </div>
      <form id="memberForm">
        <input type="hidden" id="memberId" />
        <div class="row">
          <div>
            <label for="mname">Name</label>
            <input class="input" id="mname" required />
          </div>
          <div>
            <label for="memail">Email</label>
            <input class="input" type="email" id="memail" />
          </div>
        </div>
        <div class="row">
          <div>
            <label for="mphone">Phone</label>
            <input class="input" id="mphone" />
          </div>
          <div>
            <label for="maddr">Address</label>
            <input class="input" id="maddr" />
          </div>
        </div>
        <div class="actions">
          <button class="btn" type="button" data-close="memberModal">Cancel</button>
          <button class="btn primary" type="submit">Save</button>
        </div>
      </form>
    </div>
  </div>

  <!-- Loan Modal -->
  <div class="modal" id="loanModal">
    <div class="sheet">
      <div class="hd">
        <h3>New Loan</h3>
        <button class="btn ghost" data-close="loanModal">✖</button>
      </div>
      <form id="loanForm">
        <div class="row">
          <div>
            <label>Member</label>
            <select id="loanMember" class="input"></select>
          </div>
          <div>
            <label>Book</label>
            <select id="loanBook" class="input"></select>
          </div>
        </div>
        <div class="row">
          <div>
            <label>Issue Date</label>
            <input type="date" id="issueDate" class="input" />
          </div>
          <div>
            <label>Due Date</label>
            <input type="date" id="dueDate" class="input" />
          </div>
        </div>
        <div class="actions">
          <button class="btn" type="button" data-close="loanModal">Cancel</button>
          <button class="btn primary" type="submit">Create Loan</button>
        </div>
      </form>
    </div>
  </div>

  <script>  const store = {
    key: 'libmgr.v1',
    load(){
      const raw = localStorage.getItem(this.key);
      if(!raw) return {books:[], members:[], loans:[], settings:{loanDays:14,finePerDay:5}};
      try{const data = JSON.parse(raw); return Object.assign({books:[],members:[],loans:[],settings:{loanDays:14,finePerDay:5}}, data);}catch(e){
        console.error('Bad JSON in storage', e); return {books:[], members:[], loans:[], settings:{loanDays:14,finePerDay:5}};
      }
    },
    save(data){ localStorage.setItem(this.key, JSON.stringify(data)); }
  };
  let state = store.load();

  const $ = sel => document.querySelector(sel);
  const $$ = sel => Array.from(document.querySelectorAll(sel));

  function openModal(id){ $('#'+id).classList.add('open'); }
  function closeModal(id){ $('#'+id).classList.remove('open'); }
  $$("[data-close]").forEach(btn=> btn.addEventListener('click', e=> closeModal(btn.dataset.close)) );

  function uid(prefix){ return `${prefix}_${Math.random().toString(36).slice(2,9)}`; }

  function formatDate(d){ if(!d) return ''; const dt = new Date(d); return dt.toLocaleDateString(); }

  function daysBetween(a,b){ const ms = (new Date(b) - new Date(a)); return Math.ceil(ms/86400000); }

  function computeAvailability(book){
    const active = state.loans.filter(l=> l.bookId===book.id && !l.returnedAt).length;
    const available = Math.max(0, (book.copies||1) - active);
    return {active, available};
  }

  function refreshMetrics(){
    $('#mTotalBooks').textContent = state.books.length;
    const available = state.books.reduce((sum,b)=> sum + computeAvailability(b).available, 0);
    $('#mAvailable').textContent = available;
    $('#mMembers').textContent = state.members.length;
    $('#mLoans').textContent = state.loans.filter(l=>!l.returnedAt).length;
  }

  $$('.tab').forEach(t=> t.addEventListener('click', ()=>{
    $$('.tab').forEach(x=>x.classList.remove('active'));
    t.classList.add('active');
    const name = t.dataset.tab;
    $$('.tab-pane').forEach(p=> p.hidden = !p.id.endsWith(name));
    renderAll();
  }));

  function renderBooks(){
    const q = $('#searchBooks').value.trim().toLowerCase();
    const status = $('#filterStatus').value;
    const sort = $('#sortBooks').value;

    let rows = state.books.map(b=>({ ...b, ...computeAvailability(b)}));
    if(q){ rows = rows.filter(r=> `${r.title} ${r.author} ${r.isbn}`.toLowerCase().includes(q)); }
    if(status==='available'){ rows = rows.filter(r=> r.available>0); }
    if(status==='out'){ rows = rows.filter(r=> r.available===0); }

    rows.sort((a,b)=>{
      if(sort==='title') return a.title.localeCompare(b.title);
      if(sort==='author') return a.author.localeCompare(b.author);
      if(sort==='created') return (b.createdAt||0) - (a.createdAt||0);
      return 0;
    });

    const wrap = $('#booksTableWrap');
    if(rows.length===0){ wrap.innerHTML = `<div class="empty">No books found. Add your first book.</div>`; return; }

    const html = [`<table><thead><tr>
      <th>Title</th><th>Author</th><th>ISBN</th><th>Category</th><th>Copies</th><th>Status</th><th></th>
    </tr></thead><tbody>`];
    for(const r of rows){
      html.push(`<tr>
        <td>${r.title||''}</td>
        <td>${r.author||''}</td>
        <td>${r.isbn||''}</td>
        <td>${r.category||''}</td>
        <td>${r.copies||1}</td>
        <td>${r.available>0? `<span class="pill available">${r.available} available</span>` : `<span class="pill out">All checked out</span>` }</td>
        <td style="text-align:right">
          <button class="btn" data-edit-book="${r.id}">Edit</button>
          <button class="btn danger" data-delete-book="${r.id}">Delete</button>
        </td>
      </tr>`);
    }
    html.push('</tbody></table>');
    wrap.innerHTML = html.join('');

    // actions
    $$('[data-edit-book]').forEach(b=> b.addEventListener('click', ()=> editBook(b.dataset.editBook)) );
    $$('[data-delete-book]').forEach(b=> b.addEventListener('click', ()=> deleteBook(b.dataset.deleteBook)) );
  }

  function editBook(id){
    const book = state.books.find(b=> b.id===id);
    $('#bookModalTitle').textContent = 'Edit Book';
    $('#bookId').value = book.id;
    $('#title').value = book.title||'';
    $('#author').value = book.author||'';
    $('#isbn').value = book.isbn||'';
    $('#category').value = book.category||'';
    $('#copies').value = book.copies||1;
    $('#desc').value = book.desc||'';
    openModal('bookModal');
  }

  function deleteBook(id){
    if(!confirm('Delete this book?')) return;
    // prevent delete if loan active
    const active = state.loans.some(l=> l.bookId===id && !l.returnedAt);
    if(active){ alert('Cannot delete: this book has an active loan.'); return; }
    state.books = state.books.filter(b=> b.id!==id);
    persist();
  }

  function resetBookForm(){
    $('#bookModalTitle').textContent = 'Add Book';
    $('#bookForm').reset();
    $('#bookId').value = '';
    openModal('bookModal');
  }

  $('#btnAddBook').addEventListener('click', resetBookForm);
  $('#addBookTop').addEventListener('click', resetBookForm);

  $('#bookForm').addEventListener('submit', e=>{
    e.preventDefault();
    const id = $('#bookId').value || uid('book');
    const book = {
      id,
      title: $('#title').value.trim(),
      author: $('#author').value.trim(),
      isbn: $('#isbn').value.trim(),
      category: $('#category').value.trim(),
      copies: Math.max(1, parseInt($('#copies').value||'1',10)),
      desc: $('#desc').value.trim(),
      createdAt: Date.now()
    };
    if($('#bookId').value){
      state.books = state.books.map(b=> b.id===id ? {...b, ...book} : b);
    }else{
      state.books.push(book);
    }
    persist();
    closeModal('bookModal');
  });

  $('#clearBooks').addEventListener('click', ()=>{
    $('#searchBooks').value=''; $('#filterStatus').value='all'; $('#sortBooks').value='title'; renderBooks();
  });
  ['keyup','change'].forEach(evt=>{
    $('#searchBooks').addEventListener(evt, renderBooks);
    $('#filterStatus').addEventListener(evt, renderBooks);
    $('#sortBooks').addEventListener(evt, renderBooks);
  });
  function renderMembers(){
    const q = $('#searchMembers').value.trim().toLowerCase();
    let rows = state.members;
    if(q){ rows = rows.filter(m=> `${m.name} ${m.email} ${m.id}`.toLowerCase().includes(q)); }

    const wrap = $('#membersTableWrap');
    if(rows.length===0){ wrap.innerHTML = `<div class="empty">No members yet. Add one to get started.</div>`; return; }

    const html = [`<table><thead><tr>
      <th>Name</th><th>Email</th><th>Phone</th><th>Address</th><th></th>
    </tr></thead><tbody>`];
    for(const m of rows){
      html.push(`<tr>
        <td>${m.name||''}</td>
        <td>${m.email||''}</td>
        <td>${m.phone||''}</td>
        <td>${m.addr||''}</td>
        <td style="text-align:right">
          <button class="btn" data-edit-member="${m.id}">Edit</button>
          <button class="btn danger" data-delete-member="${m.id}">Delete</button>
        </td>
      </tr>`);
    }
    html.push('</tbody></table>');
    wrap.innerHTML = html.join('');

    $$('[data-edit-member]').forEach(b=> b.addEventListener('click', ()=> editMember(b.dataset.editMember)) );
    $$('[data-delete-member]').forEach(b=> b.addEventListener('click', ()=> deleteMember(b.dataset.deleteMember)) );
  }

  function editMember(id){
    const m = state.members.find(x=> x.id===id);
    $('#memberModalTitle').textContent = 'Edit Member';
    $('#memberId').value = m.id;
    $('#mname').value = m.name||'';
    $('#memail').value = m.email||'';
    $('#mphone').value = m.phone||'';
    $('#maddr').value = m.addr||'';
    openModal('memberModal');
  }

  function deleteMember(id){
    if(!confirm('Delete this member?')) return;
    const active = state.loans.some(l=> l.memberId===id && !l.returnedAt);
    if(active){ alert('Cannot delete: this member has an active loan.'); return; }
    state.members = state.members.filter(m=> m.id!==id);
    persist();
  }

  function resetMemberForm(){
    $('#memberModalTitle').textContent = 'Add Member';
    $('#memberForm').reset();
    $('#memberId').value = '';
    openModal('memberModal');
  }

  $('#btnAddMember').addEventListener('click', resetMemberForm);
  $('#addMemberTop').addEventListener('click', resetMemberForm);

  $('#memberForm').addEventListener('submit', e=>{
    e.preventDefault();
    const id = $('#memberId').value || uid('mem');
    const m = {
      id,
      name: $('#mname').value.trim(),
      email: $('#memail').value.trim(),
      phone: $('#mphone').value.trim(),
      addr: $('#maddr').value.trim(),
      createdAt: Date.now()
    };
    if($('#memberId').value){
      state.members = state.members.map(x=> x.id===id ? {...x, ...m} : x);
    }else{
      state.members.push(m);
    }
    persist();
    closeModal('memberModal');
  });

  $('#searchMembers').addEventListener('keyup', renderMembers);

  function renderLoans(){
    const wrap = $('#loansTableWrap');
    if(state.loans.length===0){ wrap.innerHTML = `<div class="empty">No loans yet. Create one.</div>`; return; }

    const html = [`<table><thead><tr>
      <th>Member</th><th>Book</th><th>Issued</th><th>Due</th><th>Status</th><th>Fine</th><th></th>
    </tr></thead><tbody>`];
    for(const l of state.loans){
      const member = state.members.find(m=> m.id===l.memberId);
      const book = state.books.find(b=> b.id===l.bookId);
      const status = l.returnedAt ? 'Returned' : (new Date(l.dueAt) < new Date() ? 'Overdue' : 'Active');
      const fine = l.returnedAt ? l.fine||0 : calcFine(l);
      html.push(`<tr>
        <td>${member?member.name:'?'}</td>
        <td>${book?book.title:'?'}</td>
        <td>${formatDate(l.issuedAt)}</td>
        <td>${formatDate(l.dueAt)}</td>
        <td>${status}</td>
        <td>₹${fine}</td>
        <td style="text-align:right">
          ${l.returnedAt ? '' : `<button class="btn warn" data-return-loan="${l.id}">Mark Returned</button>`}
          <button class="btn danger" data-delete-loan="${l.id}">Delete</button>
        </td>
      </tr>`);
    }
    html.push('</tbody></table>');
    wrap.innerHTML = html.join('');

    $$('[data-return-loan]').forEach(b=> b.addEventListener('click', ()=> returnLoan(b.dataset.returnLoan)) );
    $$('[data-delete-loan]').forEach(b=> b.addEventListener('click', ()=> deleteLoan(b.dataset.deleteLoan)) );
  }

  function populateLoanDropdowns(){
    const memSel = $('#loanMember');
    const bookSel = $('#loanBook');
    memSel.innerHTML = state.members.map(m=> `<option value="${m.id}">${m.name}</option>`).join('');
    bookSel.innerHTML = state.books.filter(b=> computeAvailability(b).available>0).map(b=> `<option value="${b.id}">${b.title} (${computeAvailability(b).available} available)</option>`).join('');
  }

  function newLoan(){
    if(state.members.length===0 || state.books.length===0){ alert('Need at least one member and one available book.'); return; }
    const today = new Date();
    const due = new Date(today); due.setDate(due.getDate() + (state.settings.loanDays||14));
    populateLoanDropdowns();
    $('#issueDate').value = today.toISOString().slice(0,10);
    $('#dueDate').value = due.toISOString().slice(0,10);
    openModal('loanModal');
  }

  function calcFine(loan){
    const perDay = Number(state.settings.finePerDay||5);
    const lateDays = Math.max(0, daysBetween(loan.dueAt, new Date()));
    return lateDays * perDay;
  }

  function returnLoan(id){
    const loan = state.loans.find(l=> l.id===id);
    if(!loan) return;
    const fine = calcFine(loan);
    if(!confirm(`Mark as returned? Fine: ₹${fine}`)) return;
    loan.returnedAt = new Date().toISOString();
    loan.fine = fine;
    persist();
  }

  function deleteLoan(id){
    if(!confirm('Delete this loan record?')) return;
    state.loans = state.loans.filter(l=> l.id!==id);
    persist();
  }

  $('#newLoanBtn').addEventListener('click', newLoan);

  $('#loanForm').addEventListener('submit', e=>{
    e.preventDefault();
    const memberId = $('#loanMember').value;
    const bookId = $('#loanBook').value;
    if(!memberId || !bookId){ alert('Select member and book'); return; }
    const book = state.books.find(b=> b.id===bookId);
    if(!book || computeAvailability(book).available===0){ alert('Selected book is not available'); return; }
    const loan = {
      id: uid('loan'),
      memberId,
      bookId,
      issuedAt: new Date($('#issueDate').value||new Date()).toISOString(),
      dueAt: new Date($('#dueDate').value).toISOString(),
      returnedAt: null,
      fine: 0
    };
    state.loans.unshift(loan);
    persist();
    closeModal('loanModal');
  });

  function renderReports(){
    const totalBooks = state.books.length;
    const totalCopies = state.books.reduce((s,b)=> s + (b.copies||1),0);
    const totalAvailable = state.books.reduce((s,b)=> s + computeAvailability(b).available,0);
    const activeLoans = state.loans.filter(l=> !l.returnedAt).length;
    const overdue = state.loans.filter(l=> !l.returnedAt && new Date(l.dueAt)<new Date()).length;

    const topCategories = Object.entries(state.books.reduce((acc,b)=>{ acc[b.category||'Uncategorized']=(acc[b.category||'Uncategorized']||0)+1; return acc; },{}))
      .sort((a,b)=> b[1]-a[1]).slice(0,5);

    $('#reportsWrap').innerHTML = `
      <div class="metric"><div class="label">Titles / Copies</div><div class="value">${totalBooks} / ${totalCopies}</div></div>
      <div class="metric"><div class="label">Available Now</div><div class="value">${totalAvailable}</div></div>
      <div class="metric"><div class="label">Active Loans</div><div class="value">${activeLoans}</div></div>
      <div class="metric"><div class="label">Overdue</div><div class="value">${overdue}</div></div>
      <div class="metric"><div class="label">Top Categories</div><div>${topCategories.map(([k,v])=>`<span class='tag'>${k}: ${v}</span>`).join(' ')||'<span class="tag">–</span>'}</div></div>
    `;
  }

  $('#settingsForm').addEventListener('submit', e=>{
    e.preventDefault();
    state.settings.loanDays = Math.max(1, parseInt($('#loanDays').value||'14',10));
    state.settings.finePerDay = Math.max(0, parseInt($('#finePerDay').value||'5',10));
    persist(true);
    alert('Settings saved');
  });

  $('#resetAll').addEventListener('click', ()=>{
    if(!confirm('This will clear all data. Continue?')) return;
    state = {books:[],members:[],loans:[],settings:{loanDays:14,finePerDay:5}};
    persist();
  });

  function persist(fromSettings=false){
    store.save(state);
    refreshMetrics();
    renderAll();
    if(!fromSettings){ $('#loanDays').value = state.settings.loanDays; $('#finePerDay').value = state.settings.finePerDay; }
  }

  
  $('#exportBtn').addEventListener('click', (e)=>{
    e.preventDefault();
    const blob = new Blob([JSON.stringify(state,null,2)], {type:'application/json'});
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a'); a.href = url; a.download = 'library-data.json'; a.click(); URL.revokeObjectURL(url);
  });
  $('#importFile').addEventListener('change', (e)=>{
    const file = e.target.files[0]; if(!file) return;
    const reader = new FileReader();
    reader.onload = () => {
      try{ const data = JSON.parse(reader.result);
        if(!data || typeof data!=='object') throw new Error('Invalid file');
        state = Object.assign({books:[],members:[],loans:[],settings:{loanDays:14,finePerDay:5}}, data);
        persist();
      }catch(err){ alert('Import failed: '+err.message); }
    };
    reader.readAsText(file);
  });

  function renderAll(){
    // Which pane is visible?
    if(!$('#pane-books').hidden) renderBooks();
    if(!$('#pane-members').hidden) renderMembers();
    if(!$('#pane-loans').hidden) renderLoans();
    if(!$('#pane-reports').hidden) renderReports();
  }

  
  (function init(){
    
    if(state.books.length===0 && state.members.length===0 && state.loans.length===0){
      state.books.push(
        {id:uid('book'), title:'The Pragmatic Programmer', author:'Andrew Hunt', isbn:'978-0201616224', category:'Programming', copies:3, desc:'Classic software craftsmanship', createdAt:Date.now()},
        {id:uid('book'), title:'Atomic Habits', author:'James Clear', isbn:'978-0735211292', category:'Self-help', copies:2, desc:'Build better habits', createdAt:Date.now()},
        {id:uid('book'), title:'Sapiens', author:'Yuval Harari', isbn:'978-0062316097', category:'History', copies:1, desc:'A brief history of humankind', createdAt:Date.now()}
      );
      state.members.push(
        {id:uid('mem'), name:'Aishwarya N', email:'aish@example.com', phone:'9876543210', addr:'Lucknow', createdAt:Date.now()},
        {id:uid('mem'), name:'Prankur Shukla', email:'prankur@example.com', phone:'9123456780', addr:'Kanpur', createdAt:Date.now()}
      );
    }

    $('#loanDays').value = state.settings.loanDays;
    $('#finePerDay').value = state.settings.finePerDay;

  
    $('#newLoanBtn').addEventListener('click', populateLoanDropdowns);

    $$('.modal').forEach(m=> m.addEventListener('click', (e)=>{ if(e.target===m) m.classList.remove('open'); }));

    refreshMetrics();
    renderAll();
  })();
  </script>
</body>
</html>

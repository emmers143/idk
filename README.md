<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>My Stories</title>
  <style>
    body{
      font-family:"Comic Sans MS", "Segoe UI", Roboto, Helvetica, Arial;
      margin:2rem;
      background:#fdf6e3;
      color:#374151;
    }
    .card{
      border:none;
      padding:2rem;
      border-radius:20px;
      max-width:900px;
      background:#fffdf5;
      box-shadow:0 8px 20px rgba(0,0,0,0.1);
      margin:auto;
    }
    h1,h2{
      margin-top:0;
      font-weight:bold;
      color:#ff6b6b;
    }
    form{
      margin-bottom:1rem;
    }
    input[type="url"]{
      padding:.5rem;
      border:2px dashed #fbbf24;
      border-radius:12px;
      background:#fff8dc;
      width:70%;
    }
    .story-row{
      display:flex;
      justify-content:space-between;
      align-items:center;
      padding:1rem;
      margin:.75rem 0;
      border-radius:12px;
      font-size:1rem;
    }
    .story-row.empty{
      background:#fef9c3;
      border:2px dashed #fde047;
      text-align:center;
    }
    .story-row.available{
      background:#d1fae5;
      border:2px solid #34d399;
    }
    .story-row a{
      color:#3b82f6;
      font-weight:bold;
      text-decoration:none;
    }
    .story-row a:hover{
      text-decoration:underline;
    }
    button{
      border:none;
      padding:.6rem 1rem;
      border-radius:9999px;
      cursor:pointer;
      font-weight:bold;
      transition:transform 0.1s ease-in-out;
    }
    button:hover{
      transform:scale(1.05);
    }
    .btn-add{
      background:#f472b6;
      color:white;
      margin-left:.5rem;
    }
    .btn-add:hover{
      background:#db2777;
    }
    .btn-view{
      background:#60a5fa;
      color:white;
    }
    .btn-view:hover{
      background:#2563eb;
    }
    .btn-delete{
      background:#fb7185;
      color:white;
    }
    .btn-delete:hover{
      background:#e11d48;
    }
    .controls{
      display:flex;
      gap:.5rem;
    }
  </style>
</head>
<body>
  <div class="card">
    <h1>📚 My Stories</h1>
    <p>Paste the link to your Google Doc story and add it to your collection!</p>
    <form id="storyForm">
      <input type="url" id="storyUrl" placeholder="https://docs.google.com/document/..." required />
      <button type="submit" class="btn-add">✨ Add Story</button>
    </form>

    <h2>📖 Story Collection</h2>
    <div id="storyList">
      <div class="story-row empty">No stories yet 😢</div>
    </div>
  </div>

  <script>
    const form = document.getElementById('storyForm');
    const storyUrlInput = document.getElementById('storyUrl');
    const storyList = document.getElementById('storyList');

    form.addEventListener('submit', function(e){
      e.preventDefault();
      const url = storyUrlInput.value;
      if(!url) return;

      // Remove "no stories" message if present
      const emptyMsg = storyList.querySelector('.story-row.empty');
      if(emptyMsg) emptyMsg.remove();

      // Create new story row
      const row = document.createElement('div');
      row.className = 'story-row available';
      row.innerHTML = `
        <div>
          <a href="${url}" target="_blank">${url}</a>
        </div>
        <div class="controls">
          <a href="${url}" target="_blank"><button class="btn-view">👀 View</button></a>
          <button class="btn-delete">🗑 Delete</button>
        </div>
      `;

      // Add delete functionality
      row.querySelector('.btn-delete').addEventListener('click', () => {
        row.remove();
        if(!storyList.querySelector('.story-row')){
          storyList.innerHTML = '<div class="story-row empty">No stories yet 😢</div>';
        }
      });

      storyList.appendChild(row);
      storyUrlInput.value = '';
    });
  </script>
</body>
</html>

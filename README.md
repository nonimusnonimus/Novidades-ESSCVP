<!DOCTYPE html>
<html lang="pt">
<head>
  <meta charset="UTF-8" />
  <title>Site de Informações</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <style>
    body {
      font-family: Arial, Helvetica, sans-serif;
      background-color: #f4f4f4;
      margin: 0;
      padding: 0;
    }
    header {
      background-color: #2c3e50;
      color: white;
      padding: 20px;
      text-align: center;
    }
    main {
      max-width: 800px;
      margin: 20px auto;
      background: white;
      padding: 20px;
      border-radius: 6px;
    }
    h2 {
      color: #2c3e50;
    }
    form {
      margin-top: 20px;
    }
    input, textarea, button {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      font-size: 14px;
    }
    button {
      background-color: #2c3e50;
      color: white;
      border: none;
      cursor: pointer;
    }
    button:hover {
      background-color: #34495e;
    }
    .comentario {
      border-bottom: 1px solid #ddd;
      padding: 10px 0;
    }
    footer {
      text-align: center;
      padding: 15px;
      color: #666;
      font-size: 14px;
    }
  </style>
</head>
<body>

  <header>
    <h1>Bem-vindo ao nosso site</h1>
    <p>Aqui você encontra informações e pode deixar seu comentário</p>
  </header>

  <main>
    <section>
      <h2>Informações</h2>
      <p>
        Este é um site simples criado para partilhar informações com os visitantes.
        As pessoas podem ler o conteúdo e deixar comentários logo abaixo.
      </p>
    </section>

    <section>
      <h2>Deixe seu comentário</h2>
      <form id="formComentario">
        <input type="text" id="nome" placeholder="Seu nome" required />
        <textarea id="mensagem" placeholder="Seu comentário" required></textarea>
        <button type="submit">Publicar comentário</button>
      </form>
    </section>

    <section>
      <h2>Comentários</h2>
      <div id="listaComentarios"></div>
    </section>
  </main>

  <footer>
    © 2026 - Site simples de informações
  </footer>

  <script>
    const form = document.getElementById('formComentario');
    const lista = document.getElementById('listaComentarios');

    function carregarComentarios() {
      const comentarios = JSON.parse(localStorage.getItem('comentarios')) || [];
      lista.innerHTML = '';
      comentarios.forEach(c => {
        const div = document.createElement('div');
        div.className = 'comentario';
        div.innerHTML = `<strong>${c.nome}</strong><p>${c.mensagem}</p>`;
        lista.appendChild(div);
      });
    }

    form.addEventListener('submit', function(e) {
      e.preventDefault();
      const nome = document.getElementById('nome').value;
      const mensagem = document.getElementById('mensagem').value;

      const comentarios = JSON.parse(localStorage.getItem('comentarios')) || [];
      comentarios.push({ nome, mensagem });
      localStorage.setItem('comentarios', JSON.stringify(comentarios));

      form.reset();
      carregarComentarios();
    });

    carregarComentarios();
  </script>

</body>
</html>

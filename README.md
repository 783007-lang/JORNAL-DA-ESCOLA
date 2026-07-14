<!doctype html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Jornal Escolar</title>

  <style>
    :root{
      --azul-escuro:#0b1f44;
      --azul:#1f5eff;
      --vermelho:#e61e2b;
      --vermelho-escuro:#8f0f16;
      --branco:#ffffff;
      --cinza:#e9eef7;
      --cinza-escuro:#2b2f36;
      --card:#ffffffcc;
      --sombra: 0 12px 30px rgba(0,0,0,.18);
      --borda: rgba(255,255,255,.25);
      --fonte: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;
    }

    *{ box-sizing:border-box; margin:0; padding:0; }
    body{
      font-family: var(--fonte);
      color: #0b1020;
      background:
        radial-gradient(circle at 10% 10%, rgba(31,94,255,.35), transparent 40%),
        radial-gradient(circle at 80% 30%, rgba(230,30,43,.35), transparent 40%),
        linear-gradient(135deg, var(--azul-escuro) 0%, #0d2b63 45%, var(--vermelho-escuro) 100%);
      min-height: 100vh;
      padding: 24px;
    }

    .page{
      max-width: 1150px;
      margin: 0 auto;
      background: transparent;
    }

    /* 🔷 Cabeçalho */
    .topbar{
      background: linear-gradient(90deg, rgba(31,94,255,.18), rgba(230,30,43,.18));
      border: 1px solid var(--borda);
      border-radius: 18px;
      padding: 18px;
      box-shadow: var(--sombra);
      margin-bottom: 18px;
      position: relative;
      overflow: hidden;
    }
    .topbar:before{
      content:"";
      position:absolute;
      inset:-2px;
      background:
        linear-gradient(120deg, rgba(31,94,255,.22), transparent 45%),
        linear-gradient(300deg, rgba(230,30,43,.22), transparent 45%);
      pointer-events:none;
    }
    .topbar-inner{
      position: relative;
      display:flex;
      align-items:flex-start;
      justify-content:space-between;
      gap: 16px;
      flex-wrap: wrap;
    }
    .brand{
      display:flex;
      gap: 14px;
      align-items:center;
    }
    .logo{
      width: 52px; height: 52px;
      border-radius: 14px;
      background: linear-gradient(135deg, var(--azul), var(--vermelho));
      display:flex;
      align-items:center;
      justify-content:center;
      color: white;
      font-weight: 900;
      letter-spacing: .5px;
      border: 2px solid rgba(255,255,255,.35);
    }
    .brand h1{
      color: white;
      font-size: 20px;
      line-height: 1.2;
    }
    .brand p{
      color: rgba(255,255,255,.85);
      margin-top: 6px;
      font-size: 13px;
    }
    .meta{
      text-align:right;
      color: rgba(255,255,255,.9);
      font-size: 13px;
      line-height: 1.4;
      margin-top: 4px;
    }
    .pill{
      display:inline-block;
      padding: 6px 10px;
      border-radius: 999px;
      border: 1px solid rgba(255,255,255,.3);
      background: rgba(255,255,255,.08);
      margin-left: 8px;
      font-weight: 700;
      letter-spacing: .2px;
    }

    /* 🧱 Layout */
    .grid{
      display:grid;
      grid-template-columns: 2fr 1fr;
      gap: 18px;
    }

    /* 🧩 Cards base */
    .card{
      background: var(--card);
      border: 1px solid var(--borda);
      border-radius: 18px;
      padding: 16px;
      box-shadow: var(--sombra);
      backdrop-filter: blur(6px);
      transition: transform .18s ease, box-shadow .18s ease, border-color .18s ease, filter .18s ease;
    }

    /* ✨ Interatividade: hover */
    .card.interactive{
      cursor: pointer;
    }
    .card.interactive:hover{
      transform: translateY(-4px) scale(1.01);
      border-color: rgba(255,255,255,.55);
      box-shadow: 0 16px 40px rgba(0,0,0,.25);
      filter: saturate(1.1);
    }

    /* 🔽 Conteúdo extra (oculto) */
    .more{
      display: none;
      margin-top: 12px;
      padding-top: 12px;
      border-top: 1px solid rgba(0,0,0,.08);
      animation: fadeIn .18s ease;
    }
    .more.open{ display:block; }
    @keyframes fadeIn{
      from{ opacity: 0; transform: translateY(-6px); }
      to{ opacity: 1; transform: translateY(0); }
    }

    /* Título do card */
    .card h2{
      font-size: 16px;
      color: var(--cinza-escuro);
      margin-bottom: 12px;
      display:flex;
      align-items:center;
      gap: 10px;
      letter-spacing: .2px;
    }

    .badge{
      width: 34px; height: 34px;
      border-radius: 12px;
      display:flex;
      align-items:center;
      justify-content:center;
      color: white;
      font-weight: 900;
      border: 2px solid rgba(255,255,255,.35);
      background: linear-gradient(135deg, var(--azul), var(--vermelho));
    }

    /* Notícias */
    .news-list{
      display:flex;
      flex-direction:column;
      gap: 12px;
    }
    .news-item{
      background: rgba(255,255,255,.65);
      border: 1px solid rgba(0,0,0,.06);
      border-radius: 16px;
      padding: 12px;
      transition: transform .15s ease;
    }
    .news-item:hover{
      transform: translateY(-2px);
    }
    .news-item h3{
      font-size: 14px;
      margin-bottom: 6px;
      color: #0b1020;
    }
    .news-item p{
      font-size: 13px;
      color: #2f3440;
      line-height: 1.35;
    }
    .tag-row{
      display:flex;
      gap: 8px;
      flex-wrap: wrap;
      margin-top: 10px;
    }
    .tag{
      font-size: 12px;
      padding: 5px 9px;
      border-radius: 999px;
      border: 1px solid rgba(0,0,0,.08);
      background: rgba(31,94,255,.08);
      color: #103070;
      font-weight: 700;
    }
    .tag.red{
      background: rgba(230,30,43,.10);
      color: #7a0a10;
    }
    .tag.blue{
      background: rgba(31,94,255,.10);
      color: #0b2b72;
    }

    /* Lateral */
    .stack{
      display:flex;
      flex-direction:column;
      gap: 18px;
    }

    .list{
      display:flex;
      flex-direction:column;
      gap: 10px;
      margin-top: 6px;
    }
    .list-item{
      display:flex;
      gap: 10px;
      align-items:flex-start;
      padding: 10px;
      border-radius: 14px;
      background: rgba(255,255,255,.62);
      border: 1px solid rgba(0,0,0,.06);
    }
    .dot{
      width: 10px; height: 10px;
      border-radius: 50%;
      margin-top: 5px;
      background: linear-gradient(135deg, var(--azul), var(--vermelho));
      flex: 0 0 auto;
    }
    .list-item div{
      font-size: 13px;
      line-height: 1.35;
      color: #2f3440;
    }
    .list-item strong{
      display:block;
      color: #0b1020;
      margin-bottom: 2px;
      font-size: 13px;
    }

    /* Fofocas */
    .rumor{
      background: linear-gradient(180deg, rgba(230,30,43,.10), rgba(31,94,255,.06));
      border: 1px dashed rgba(230,30,43,.35);
    }

    /* Rodapé */
    .footer{
      margin-top: 18px;
      text-align:center;
      color: rgba(255,255,255,.9);
      font-size: 12px;
      padding: 14px;
    }
    .footer .line{
      display:inline-block;
      padding: 8px 14px;
      border-radius: 999px;
      border: 1px solid rgba(255,255,255,.25);
      background: rgba(255,255,255,.08);
    }

    /* 📱 Responsivo */
    @media (max-width: 980px){
      .grid{ grid-template-columns: 1fr; }
      .meta{ text-align:left; }
      .topbar-inner{ align-items:flex-start; }
    }
  </style>
</head>

<body>
  <div class="page">
    <header class="topbar">
      <div class="topbar-inner">
        <div class="brand">
          <div class="logo">JS</div>
          <div>
            <h1>🗞️ Jornal Escolar • Governador Pedro Ivo Campos</h1>
            <p>Notícias da semana • Dicas • Curiosidades • Cantina • Fofocas</p>
          </div>
        </div>

        <div class="meta">
          Semana de <span class="pill">__ / __ / ____</span><br/>
          Edição Especial: <span class="pill">Azul &amp; Vermelho</span>
        </div>
      </div>
    </header>

    <main class="grid">
      <!-- 📰 Notícias da semana (clique abre Notícias do mês) -->
      <section class="card interactive" data-target="news-more" aria-label="Notícias da semana (clique para ver mais)">
        <h2><span class="badge">📰</span> Notícias da semana</h2>

        <div class="news-list">
          <article class="news-item">
            <h3>🏫 Projeto “Leitura em Família” movimenta a escola</h3>
            <p>Os estudantes compartilharam uma frase marcante e recomendam livros para o mural.</p>
            <div class="tag-row">
              <span class="tag blue">Educação</span>
              <span class="tag">Leitura</span>
              <span class="tag red">Participação</span>
            </div>
          </article>

          <article class="news-item">
            <h3>⚽ Treino aberto de esportes incentiva colaboração</h3>
            <p>As atividades em equipes reforçam o respeito e a torcida junto!</p>
            <div class="tag-row">
              <span class="tag blue">Esportes</span>
              <span class="tag">Amizade</span>
            </div>
          </article>

          <article class="news-item">
            <h3>🎨 Feira de Ciências: ideias brilhantes para apresentar</h3>
            <p>Equipes estão finalizando experimentos e pôsteres com muita criatividade.</p>
            <div class="tag-row">
              <span class="tag red">Ciências</span>
              <span class="tag">Criatividade</span>
            </div>
          </article>
        </div>

        <!-- Conteúdo extra (Notícias do mês) -->
        <div class="more" id="news-more">
          <h3 style="margin-bottom:8px; color:#0b1020;">📌 Notícias do mês (próximos destaques)</h3>
          <div class="news-item" style="margin-bottom:10px;">
            <h3 style="font-size:14px;">📚 Mutirão de leitura + troca de livros</h3>
            <p>Traga um livro e encontre outro para levar para casa.</p>
          </div>
          <div class="news-item">
            <h3 style="font-size:14px;">🏆 Olimpíada de conhecimento (gincana por turmas)</h3>
            <p>Desafios rápidos nas áreas de matemática, língua portuguesa e ciências.</p>
          </div>
        </div>
      </section>

      <aside class="stack">
        <!-- 💡 Dicas -->
        <section class="card interactive" data-target="dicas-more" aria-label="Dicas (clique para ver mais)">
          <h2><span class="badge">💡</span> Dicas</h2>
          <div class="list">
            <div class="list-item">
              <span class="dot"></span>
              <div>
                <strong>Como estudar melhor</strong>
                Faça um resumo com 5 tópicos. Depois, explique como se fosse um amigo.
              </div>
            </div>
            <div class="list-item">
              <span class="dot"></span>
              <div>
                <strong>Organização rápida</strong>
                Separe um cantinho só para trabalhos: caderno, folhas e canetas.
              </div>
            </div>
          </div>

          <div class="more" id="dicas-more">
            <div class="list-item" style="background: rgba(255,255,255,.7);">
              <span class="dot"></span>
              <div>
                <strong>Bônus:</strong>
                Use 25 minutos de estudo + 5 de pausa. Ajuda a manter o foco sem cansar!
                😄
              </div>
            </div>
          </div>
        </section>

        <!-- 🤔 Curiosidades -->
        <section class="card interactive" data-target="curios-more" aria-label="Curiosidades (clique para ver mais)">
          <h2><span class="badge">🤔</span> Curiosidades</h2>
          <div class="list">
            <div class="list-item">
              <span class="dot"></span>
              <div>
                <strong>Você sabia?</strong>
                O cérebro continua processando informações enquanto você descansa.
              </div>
            </div>
            <div class="list-item">
              <span class="dot"></span>
              <div>
                <strong>Pequeno fato</strong>
                Água ajuda na concentração: hidratado, você rende mais.
              </div>
            </div>
          </div>

          <div class="more" id="curios-more">
            <div class="list-item" style="background: rgba(255,255,255,.7);">
              <span class="dot"></span>
              <div>
                <strong>Curiosidade:</strong>
                Aprender algo novo pode melhorar a memória com o tempo!
                📖✨
              </div>
            </div>
          </div>
        </section>

        <!-- 🍽️ Cantina -->
        <section class="card interactive" data-target="cantina-more" aria-label="Comidas da cantina (clique para ver mais)">
          <h2><span class="badge">🍽️</span> Comidas da cantina</h2>
          <div class="list">
            <div class="list-item">
              <span class="dot"></span>
              <div><strong>Segunda:</strong> Arroz, feijão, frango desfiado e salada.</div>
            </div>
            <div class="list-item">
              <span class="dot"></span>
              <div><strong>Quarta:</strong> Macarrão ao molho e legumes salteados.</div>
            </div>
            <div class="list-item">
              <span class="dot"></span>
              <div><strong>Sexta:</strong> Sanduíche natural + fruta da estação.</div>
            </div>
          </div>

          <div class="more" id="cantina-more">
            <div class="list-item" style="background: rgba(255,255,255,.7);">
              <span class="dot"></span>
              <div>
                <strong>Votação rápida:</strong> Qual você quer que volte na próxima semana?
                ( ) Arroz com frango • ( ) Macarrão • ( ) Sanduíche natural 🗳️
              </div>
            </div>
          </div>
        </section>

        <!-- 🎭 Fofocas -->
        <section class="card rumor interactive" data-target="fofocas-more" aria-label="Fofocas (clique para ver mais)">
          <h2><span class="badge">🎭</span> Fofocas (do bem) 😅</h2>
          <div class="list">
            <div class="list-item">
              <span class="dot"></span>
              <div>
                <strong>Boato:</strong> pode ter surpresa no corredor por causa da decoração!
              </div>
            </div>
            <div class="list-item">
              <span class="dot"></span>
              <div>
                <strong>Segredo:</strong> tem turma ensaiando uma música para a Feira de Ciências!
                🎶
              </div>
            </div>
          </div>

          <div class="more" id="fofocas-more">
            <div class="list-item" style="background: rgba(255,255,255,.72);">
              <span class="dot"></span>
              <div>
                <strong>Atualização:</strong> a galera está escondendo “frases motivacionais” no mural
                — quem achar, compartilha! 😄
              </div>
            </div>
          </div>
        </section>
      </aside>
    </main>

    <footer class="footer">
      <span class="line">🧑‍💻 Dica: passe o mouse e clique no card para abrir mais!</span>
    </footer>
  </div>

  <script>
    // ✅ Clique no card abre/fecha o conteúdo extra
    const cards = document.querySelectorAll(".card.interactive");

    cards.forEach(card => {
      card.addEventListener("click", () => {
        const targetId = card.getAttribute("data-target");
        const el = document.getElementById(targetId);

        // fecha outros (opcional, para não abrir tudo ao mesmo tempo)
        document.querySelectorAll(".more.open").forEach(openEl => {
          if (openEl !== el) openEl.classList.remove("open");
        });

        el.classList.toggle("open");
      });
    });

    // 🧹 Evita abrir/fechar ao clicar em seleção de texto (opcional)
    // (Mantido simples para o exemplo funcionar bem.)
  </script>
</body>
</html>


<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Sistema de Etiquetas</title>
  
  <link
    href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap"
    rel="stylesheet"
  />
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

  <style>
    :root {
      --primary-color: #D32F2F; /* Vermelho escuro */
      --secondary-color: #FFC107; /* Amarelo */
      --background-gradient: linear-gradient(135deg, #f0f0f0, #e0e0e0); /* Gradiente neutro */
      --label-width: 300px;
      --label-font-size: 16px;
      --label-border-color: var(--primary-color);
      --label-background: #FFFFFF; /* Fundo branco para as etiquetas */
      --label-shadow: rgba(0, 0, 0, 0.1);
      --btn-hover-bg: #B71C1C;
      --btn-secondary-hover-bg: #FFA000;
    }

    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: "Poppins", sans-serif;
      min-height: 100vh;
      background: var(--background-gradient);
      padding: 20px;
      color: #333;
    }

    .container {
      max-width: 1200px;
      margin: 0 auto;
      background: white;
      padding: 25px;
      border-radius: 10px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
    }

    .header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding-bottom: 15px;
      border-bottom: 3px solid var(--primary-color);
      margin-bottom: 30px;
    }

    .header-logo {
      height: 80px;
      width: auto;
    }

    h1,
    h2 {
      color: var(--primary-color);
      margin-bottom: 20px;
    }

    .form-section {
      margin-bottom: 30px;
      padding: 20px;
      background: #fff0f0;
      border-radius: 8px;
    }

    .separador {
      border-top: 1px solid #ccc; /* Cor e espessura da linha */
      margin: 20px 0; /* Espaçamento acima e abaixo da linha */
    }

    .form-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
      margin-bottom: 20px;
    }

    .form-group {
      margin-bottom: 15px;
    }

    label {
      display: block;
      margin-bottom: 8px;
      font-weight: 600;
      color: #333;
    }

    input[type="text"],
    select {
      width: 100%;
      padding: 10px 12px;
      border: 1px solid #ddd;
      border-radius: 5px;
      font-size: 14px;
      transition: border 0.3s ease, box-shadow 0.3s ease;
    }

    input[type="text"]:focus,
    select:focus {
      border-color: var(--primary-color);
      box-shadow: 0 0 5px rgba(211, 47, 47, 0.5);
      outline: none;
    }

    .btn {
      background: var(--primary-color);
      color: white;
      border: none;
      padding: 12px 24px;
      border-radius: 5px;
      cursor: pointer;
      font-weight: 600;
      margin-right: 10px;
      margin-bottom: 10px;
      transition: background 0.3s ease, transform 0.2s ease;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }

    .btn:hover {
      background: var(--btn-hover-bg);
      transform: translateY(-2px);
    }

    .btn-secondary {
      background: var(--secondary-color);
      color: #333;
    }

    .btn-secondary:hover {
      background: var(--btn-secondary-hover-bg);
      transform: translateY(-2px);
    }

    /* Etiquetas lado a lado com espaçamento */
    .labels-container {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      padding: 20px 0;
      justify-content: flex-start; /* Alinha à esquerda */
    }

    .label-card {
      width: var(--label-width);
      position: relative;
      border: 2px solid var(--label-border-color);
      border-radius: 12px;
      padding: 20px;
      background: var(--label-background); /* Fundo branco */
      box-shadow: 0 2px 6px var(--label-shadow);
      display: flex;
      flex-direction: column;
      align-items: flex-start;
      font-size: var(--label-font-size);
    }

    .logos-container {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 20px;
      margin-bottom: 15px;
      width: 100%;
    }

    .label-logo {
      height: 35px;
      width: auto;
    }

    .label-header {
      color: var(--primary-color);
      font-size: 1.3em;
      font-weight: 700;
      text-align: center;
      width: 100%;
      margin-bottom: 20px;
      word-wrap: break-word;
    }

    .label-content {
      width: 100%;
      display: flex;
      flex-direction: column;
      gap: 10px;
      word-wrap: break-word;
    }

    .label-field {
      display: flex;
      align-items: center;
      flex-wrap: wrap;
    }

    .label-field span {
      font-weight: 600;
      color: var(--primary-color);
      margin-right: 10px;
      word-wrap: break-word;
    }

    @media (max-width: 600px) {
      .label-card {
        width: 100%; /* Ajusta para 100% em telas menores */
      }
    }

    @media print {
      body {
        background: none;
      }

      .label-card {
        break-inside: avoid;
        box-shadow: none;
      }

      /* Alguns elementos não são impressos */
      .container > *:not(.labels-container) {
        display: none;
      }
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="header">
      <img src="techverify.png" alt="TechVerify" class="header-logo" />
      <h1>Sistema de Etiquetas</h1>
    </div>

    <div class="form-section">
      <h2>1. Configuração dos Campos</h2>
      <div class="form-grid" id="labelsConfig">
        <div class="form-group">
          <label>Campo 1 (Ex: RG):</label>
          <input type="text" id="labelCampo1" value="RG" />
        </div>
        <div class="form-group">
          <label>Campo 2 (Ex: ID):</label>
          <input type="text" id="labelCampo2" value="ID" />
        </div>
        <div class="form-group">
          <label>Campo 3 (Ex: Nº Série):</label>
          <input type="text" id="labelCampo3" value="Nº Série" />
        </div>
        <div class="form-group">
          <label>Campo 4 (Ex: Sensor):</label>
          <input type="text" id="labelCampo4" value="Sensor" />
        </div>
        <div class="form-group">
          <label>Campo 5 (Ex: Local):</label>
          <input type="text" id="labelCampo5" value="Local" />
        </div>
        <div class="form-group">
          <label>Campo 6 (Ex: Data):</label>
          <input type="text" id="labelCampo6" value="Data" />
        </div>
      </div>
    </div>

    <div class="separador"></div> <!-- Linha de separação -->

    <div class="form-section">
      <h2>2. Tamanho das Etiquetas</h2>
      <div class="form-grid">
        <div class="form-group">
          <label>Selecione o tamanho:</label>
          <select id="labelSizeSelect" onchange="changeLabelSize()">
            <option value="t1">T1 - 120px (Fonte 9px)</option>
            <option value="t2">T2 - 150px (Fonte 10px)</option>
            <option value="t3">T3 - 200px (Fonte 12px)</option>
            <option value="t4">T4 - 250px (Fonte 14px)</option>
            <option value="t5" selected>T5 - 300px (Fonte 16px)</option>
            <option value="t6">T6 - 350px (Fonte 18px)</option>
            <option value="t7">T7 - 400px (Fonte 20px)</option>
            <option value="t8">T8 - 500px (Fonte 24px)</option>
          </select>
        </div>
      </div>

      <div class="buttons-group">
        <button class="btn" onclick="addAparelho()">Adicionar Aparelho</button>
        <button class="btn btn-secondary" onclick="downloadAllAsSinglePDF()">Baixar PDF</button>
        <button class="btn" onclick="clearAllFields()">Limpar Tudo</button>
      </div>
    </div>

    <div id="aparelhosWrapper"></div>
    <div id="labelsContainer" class="labels-container"></div>
  </div>

  <script>
    let aparelhos = [];
    let aparelhoCount = 0; // Contador para IDs únicos

    // Tabela com 8 tamanhos (largura em px e tamanho de fonte)
    const sizeMap = {
      t1:  { width: "120px", fontSize: "9px" },
      t2:  { width: "150px", fontSize: "10px" },
      t3:  { width: "200px", fontSize: "12px" },
      t4:  { width: "250px", fontSize: "14px" },
      t5:  { width: "300px", fontSize: "16px" },
      t6:  { width: "350px", fontSize: "18px" },
      t7:  { width: "400px", fontSize: "20px" },
      t8:  { width: "500px", fontSize: "24px" },
    };

    // Função para converter px para mm
    function pxToMm(pxString) {
      const pxValue = parseInt(pxString.replace("px", ""), 10) || 300;
      return pxValue * 0.264583;
    }

    // Função para alterar o tamanho das etiquetas no site
    function changeLabelSize() {
      const sel = document.getElementById("labelSizeSelect").value;
      const sz = sizeMap[sel] || sizeMap.t5;
      document.documentElement.style.setProperty("--label-width", sz.width);
      document.documentElement.style.setProperty("--label-font-size", sz.fontSize);
      // Remover altura fixa para permitir ajuste automático
      document.documentElement.style.removeProperty("--label-height");

      // Atualiza todas as etiquetas existentes
      aparelhos.forEach(aparelho => {
        const labelId = `label-${aparelho.id}`;
        const labelDiv = document.getElementById(labelId);
        if (labelDiv) {
          labelDiv.style.width = sz.width;
          labelDiv.style.fontSize = sz.fontSize;
        }
      });
    }

    // Adiciona um novo aparelho (conjunto de campos)
    function addAparelho() {
      aparelhoCount++;
      const id = aparelhoCount;
      aparelhos.push({
        id: id,
        campo1: "",
        campo2: "",
        campo3: "",
        campo4: "",
        campo5: "",
        campo6: "",
      });

      const n1 = document.getElementById("labelCampo1").value.trim();
      const n2 = document.getElementById("labelCampo2").value.trim();
      const n3 = document.getElementById("labelCampo3").value.trim();
      const n4 = document.getElementById("labelCampo4").value.trim();
      const n5 = document.getElementById("labelCampo5").value.trim();
      const n6 = document.getElementById("labelCampo6").value.trim();

      const div = document.createElement("div");
      div.className = "form-grid";
      div.innerHTML = `
        <div class="form-group">
          <label>${n1 || "Campo 1"}:</label>
          <input type="text" id="aparelho-${id}-campo1" oninput="updateAparelho(${id}, 'campo1', this.value)" placeholder="Digite ${n1 || 'Campo 1'}">
        </div>
        <div class="form-group">
          <label>${n2 || "Campo 2"}:</label>
          <input type="text" id="aparelho-${id}-campo2" oninput="updateAparelho(${id}, 'campo2', this.value)" placeholder="Digite ${n2 || 'Campo 2'}">
        </div>
        <div class="form-group">
          <label>${n3 || "Campo 3"}:</label>
          <input type="text" id="aparelho-${id}-campo3" oninput="updateAparelho(${id}, 'campo3', this.value)" placeholder="Digite ${n3 || 'Campo 3'}">
        </div>
        <div class="form-group">
          <label>${n4 || "Campo 4"}:</label>
          <input type="text" id="aparelho-${id}-campo4" oninput="updateAparelho(${id}, 'campo4', this.value)" placeholder="Digite ${n4 || 'Campo 4'}">
        </div>
        <div class="form-group">
          <label>${n5 || "Campo 5"}:</label>
          <input type="text" id="aparelho-${id}-campo5" oninput="updateAparelho(${id}, 'campo5', this.value)" placeholder="Digite ${n5 || 'Campo 5'}">
        </div>
        <div class="form-group">
          <label>${n6 || "Campo 6"}:</label>
          <input type="text" id="aparelho-${id}-campo6" oninput="updateAparelho(${id}, 'campo6', this.value)" placeholder="Digite ${n6 || 'Campo 6'}">
        </div>
      `;
      document.getElementById("aparelhosWrapper").appendChild(div);

      // Cria a etiqueta correspondente
      createLabel(id, { campo1: n1, campo2: n2, campo3: n3, campo4: n4, campo5: n5, campo6: n6 });
    }

    // Cria uma etiqueta vazia correspondente a um aparelho
    function createLabel(id, campos) {
      const labelsContainer = document.getElementById("labelsContainer");

      const labelDiv = document.createElement("div");
      labelDiv.className = "label-card";
      labelDiv.id = `label-${id}`;

      labelDiv.innerHTML = `
        <div class="logos-container">
          <img src="logo kma.png" alt="KMA" class="label-logo">
          <img src="logo bureau veritas.png" alt="Bureau Veritas" class="label-logo">
        </div>
        <div class="label-header">
          Etiqueta de Identificação
        </div>
        <div class="label-content">
          ${campos.campo1 ? `<div class="label-field campo1"><span>${campos.campo1}:</span> </div>` : ""}
          ${campos.campo2 ? `<div class="label-field campo2"><span>${campos.campo2}:</span> </div>` : ""}
          ${campos.campo3 ? `<div class="label-field campo3"><span>${campos.campo3}:</span> </div>` : ""}
          ${campos.campo4 ? `<div class="label-field campo4"><span>${campos.campo4}:</span> </div>` : ""}
          ${campos.campo5 ? `<div class="label-field campo5"><span>${campos.campo5}:</span> </div>` : ""}
          ${campos.campo6 ? `<div class="label-field campo6"><span>${campos.campo6}:</span> </div>` : ""}
        </div>
      `;
      labelsContainer.appendChild(labelDiv);
    }

    // Atualiza o valor do campo no array de aparelhos e na etiqueta
    function updateAparelho(id, field, value) {
      // Atualiza o array de aparelhos
      const aparelho = aparelhos.find(ap => ap.id === id);
      if (aparelho) {
        aparelho[field] = value;
      }

      // Atualiza a etiqueta correspondente
      const labelId = `label-${id}`;
      const labelDiv = document.getElementById(labelId);
      if (labelDiv) {
        // Verifica se o campo tem um rótulo definido
        const campoLabel = getCampoLabel(field);
        if (campoLabel) {
          const fieldDiv = labelDiv.querySelector(`.label-content .${field}`);
          if (fieldDiv) {
            fieldDiv.innerHTML = `<span>${campoLabel}:</span> ${value}`;
          } else {
            // Cria o campo na etiqueta se ainda não existir
            const newFieldDiv = document.createElement("div");
            newFieldDiv.className = `label-field ${field}`;
            newFieldDiv.innerHTML = `<span>${campoLabel}:</span> ${value}`;
            labelDiv.querySelector(".label-content").appendChild(newFieldDiv);
          }
        } else {
          // Se o rótulo não estiver definido, remove o campo da etiqueta
          const fieldDiv = labelDiv.querySelector(`.label-content .${field}`);
          if (fieldDiv) {
            fieldDiv.remove();
          }
        }
      }
    }

    // Retorna o rótulo do campo com base no campo
    function getCampoLabel(field) {
      const campoLabels = {
        campo1: document.getElementById("labelCampo1").value.trim(),
        campo2: document.getElementById("labelCampo2").value.trim(),
        campo3: document.getElementById("labelCampo3").value.trim(),
        campo4: document.getElementById("labelCampo4").value.trim(),
        campo5: document.getElementById("labelCampo5").value.trim(),
        campo6: document.getElementById("labelCampo6").value.trim(),
      };
      return campoLabels[field] || "";
    }

    // Limpa todos os campos e etiquetas
    function clearAllFields() {
      if (confirm("Tem certeza que deseja limpar todas as etiquetas e campos?")) {
        aparelhos = [];
        aparelhoCount = 0;
        document.getElementById("aparelhosWrapper").innerHTML = "";
        document.getElementById("labelsContainer").innerHTML = "";
      }
    }

    // Gera e baixa o PDF com todas as etiquetas em modo grade,
    // respeitando o tamanho escolhido (px => convertido em mm).
    async function downloadAllAsSinglePDF() {
      const labelsContainer = document.getElementById("labelsContainer");
      const labelElements = labelsContainer.getElementsByClassName("label-card");

      if (!labelElements.length) return alert("Nenhuma etiqueta para gerar PDF.");

      try {
        const { jsPDF } = window.jspdf;
        const pdf = new jsPDF({
          orientation: "portrait",
          unit: "mm",
          format: "a4",
        });

        const pdfWidth = pdf.internal.pageSize.getWidth();  // ~210 mm
        const pdfHeight = pdf.internal.pageSize.getHeight(); // ~297 mm
        const pageMargin = 10;  // Margem lateral
        const labelMargin = 10;  // Espaço horizontal e vertical entre etiquetas

        let currentX = pageMargin;
        let currentY = pageMargin;
        let maxHeightInRow = 0;

        for (let i = 0; i < labelElements.length; i++) {
          const label = labelElements[i];

          // Captura a etiqueta como canvas
          const canvas = await html2canvas(label, {
            scale: 2,
            useCORS: true,
            logging: false,
          });
          const imgData = canvas.toDataURL("image/png");
          const imgProps = pdf.getImageProperties(imgData);

          // Calcula a largura e altura da imagem em mm
          const labelWidthPx = getComputedStyle(label).getPropertyValue("--label-width").trim();
          const labelWidthMm = pxToMm(labelWidthPx);
          const labelHeightPx = label.offsetHeight + "px"; // Usa offsetHeight para obter a altura real
          const labelHeightMm = pxToMm(labelHeightPx);

          // Verifica se a etiqueta cabe na linha atual
          if (currentX + labelWidthMm > pdfWidth - pageMargin) {
            // Move para a próxima linha
            currentX = pageMargin;
            currentY += maxHeightInRow + labelMargin;
            maxHeightInRow = 0;
          }

          // Verifica se a etiqueta cabe na página atual
          if (currentY + labelHeightMm > pdfHeight - pageMargin) {
            pdf.addPage();
            currentX = pageMargin;
            currentY = pageMargin;
            maxHeightInRow = 0;
          }

          // Adiciona a imagem ao PDF
          pdf.addImage(
            imgData,
            "PNG",
            currentX,
            currentY,
            labelWidthMm,
            labelHeightMm
          );

          // Atualiza a posição para a próxima etiqueta
          currentX += labelWidthMm + labelMargin;
          if (labelHeightMm > maxHeightInRow) {
            maxHeightInRow = labelHeightMm;
          }
        }

        pdf.save("etiquetas.pdf");
      } catch (error) {
        console.error("Erro ao gerar PDF:", error);
        alert("Erro ao gerar o PDF. Por favor, tente novamente.");
      }
    }

    // Inicializa o tamanho padrão (T5) ao carregar a página
    window.onload = function () {
      changeLabelSize();
    };
  </script>
</body>
</html>

# Anmeldung für die Geländespiele

<html lang="de">
<head>
  <meta charset="UTF-8" />
  <title>Gruppendaten erfassen</title>
</head>
<body>
  <h1>Gruppendaten erfassen</h1>
  <form id="dataForm">
    <label>
      Gruppennummer:
      <input type="text" name="groupNumber" required />
    </label><br><br>

    <label>
      Name:
      <input type="text" name="name" required />
    </label><br><br>

    <label>Altersklasse:</label><br>
    <label><input type="radio" name="ageClass" value="Kind" required /> Kind</label><br>
    <label><input type="radio" name="ageClass" value="Jugendlich" /> Jugendlich</label><br>
    <label><input type="radio" name="ageClass" value="Erwachsen" /> Erwachsen</label><br><br>

    <button type="submit">Absenden</button>
  </form>

  <p id="responseMessage"></p>

  <script>
    const form = document.getElementById('dataForm');
    const responseMessage = document.getElementById('responseMessage');

    form.addEventListener('submit', function(event) {
      event.preventDefault();

      const formData = new FormData(form);
      const data = {
        groupNumber: formData.get('groupNumber'),
        name: formData.get('name'),
        ageClass: formData.get('ageClass')
      };

      fetch('DEINE_WEB_APP_URL_HIER_EINFÜGEN', {
        method: 'POST',
        body: JSON.stringify(data),
        headers: {
          'Content-Type': 'application/json'
        }
      })
      .then(response => response.json())
      .then(result => {
        if (result.result === 'success') {
          responseMessage.textContent = 'Daten erfolgreich gespeichert!';
          form.reset();
        } else {
          responseMessage.textContent = 'Fehler: ' + (result.message || 'Unbekannt');
        }
      })
      .catch(error => {
        responseMessage.textContent = 'Fehler beim Senden: ' + error.message;
      });
    });
  </script>
</body>
</html>

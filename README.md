# Création-de-tableau-et-bibliotheques-dynamiques
Sur base d'un formulaire HTML que j'ai créé, je voudrais créer un tableau dynamique à partir d'un menu <select> et <option> sur plusieurs lignes. Lorsque l'on sélectionne plusieurs fois un choix sous <select> et <otpion>, je voudrais que cette option puisse être enregistrée en Python et que le tableau crée des lignes de cellules automatiquement par ajouts de choix


Dans mon html j'ai créé ceci: 

<table>
  <thead>
    <tr>
      <th>Arbre</th>
      <th>Taille</th>
      </tr>
  </thead>  
  <tbody id="Typologiearbres">
    <tr>
      <td>
        <select name="abre_1">
            <option value="None" selected> - None - </option>
            <option value="Feuille1">Feuille1</option>
            <option value="Feuille2">Feuille2</option>
        <select number="Taille_1">
       </td>
     </tr>
    <tr>
      <td>
        <select name="abre_2"> 
            <option value="None" selected> - None - </option>
            <option value="Feuille1">Feuille1</option>
            <option value="Feuille2">Feuille2</option>
      <select number="Taille_2  ">
      </td>

      Etc

J'ai ensuite créé, dans un autre document python, une méthode Flask qui reprend ces valeurs au travers de route (cela fonctionne): 

                            @app.route('/')
                            def index():
                                return render_template('questions.html')

                            @app.route('/submit', methods=['POST'])

                            arbres_info = []
                            for i in range(1, 3):  # Boucle de 1 à 3 du formulaire
                                arbre = request.form.get(f'arbre_{i}')
                                
            
                                arbres_info = {
                                    "Arbre": arbre,
                                }


Ensuite, j'aimerai créer dans un document word (il sort déjà le document word), un tableau qui crée des lignes supplémentaire à chaque fois que l'on sélectionne "Feuille1". Avec donc si possible deux colonnes: 
  
      columns = ["Description", "Caractéristiques de la feuille"]
      data = []

Cela veut dire que pour les arbre_1, arbre_2 et suivants (si nécessaire), je voudrais qu'il ajoute toutes les "Feuille1" sélectionnées sous la première colonne Description. J'ai essayé tant bien que mal de le faire et je n'y arrive pas.

Dans caractéristiques de la feuille, j'aimerai qu'il reprenne les données de "Taille" avec comme condition que cette taille soit < à 50. 

Voici le tableau que j'aimerai ajouter (en espérant que les codes soient corrects). C'est donc dans ce tableau que je voudrais qu'il ajoute les lignes.


      def add_table_to_doc(doc, data, heading):
          doc.add_heading(heading, level=2).paragraph_format.alignment = WD_ALIGN_PARAGRAPH.CENTER
       
    
        doc = document_nature
        # Add the table to the document
        table = doc.add_table(rows=len(df) + 1, cols=3, style='Table Grid')
        table.autofit = True

        # Fill the data into the table and apply color
        for i, row in enumerate(df.itertuples()):
            table_row = table.rows[i].cells

            # Fill the data into the cells
            for col in range(3):  # Three columns as specified
                cell_value = row[col + 1]
                        
                if isinstance(cell_value, (int, float)) and not np.isnan(cell_value):
                    table_row[col].text = str(int(cell_value))
                else:
                    table_row[col].text = str(cell_value)

                if i == 0 or i == 1:
                    set_cell_color(table_row[col], color='ffb3b3')  # Red for header and "Montant au départ" row
                else:
                    set_cell_color(table_row[col], color='ffffff')  # White for other rows

                # Bold the headers
                if i == 0:
                    table_row[col].paragraphs[0].runs[0].font.bold = True
                    table_row[col].paragraphs[0].paragraph_format.alignment = WD_ALIGN_PARAGRAPH.CENTER


Je crois que pour créer tout ceci, il faudra créer des bibliothèques. Mais je ne parviens pas à les réaliser. Pourriez-vous m'aider

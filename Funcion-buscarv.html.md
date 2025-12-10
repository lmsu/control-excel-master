Original
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="author" content="Luis M. Salinas">
    <title>Función BUSCARV - Excel</title>
    <style>
        /* --- VARIABLES BASE --- */
        :root {
            --espaciado-ppal: 15px;
            --borde-radio: 8px;
            --sombra-nav: 0 4px 6px rgba(0, 0, 0, 0.1);
            --sombra-card: 0 2px 8px rgba(0,0,0,0.1);
        }

        /* === TEMAS POR IDIOMA === */
        .theme-es { --color-ppal: #1e88e5; --color-secundario: #1565c0; --color-fondo: #a0bce7; --color-texto: #0d3040; }
        .theme-en { --color-ppal: #43a047; --color-secundario: #2e7d32; --color-fondo: #f1f8e9; --color-texto: #1b5e20; }
        .theme-ca { --color-ppal: #FF9966; --color-secundario: #654321; --color-fondo: #fff8e1; --color-texto: #d32f2f; }
        .theme-fr { --color-ppal: #e53935; --color-secundario: #c62828; --color-fondo: #ffebee; --color-texto: #1a237e; }

        /* --- ESTILOS BASE --- */
        * { box-sizing: border-box; }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--color-fondo);
            color: var(--color-texto);
            line-height: 1.6;
            transition: background-color 0.5s, color 0.5s;
        }
        a { text-decoration: none; color: inherit; }

        /* HEADER */
        header {
            background-color: var(--color-ppal);
            box-shadow: var(--sombra-nav);
            padding: 0 var(--espaciado-ppal);
            margin-bottom: 30px;
        }
        .header-top {
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px 0;
            text-align: center;
        }
        .img-office {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            object-fit: cover;
            border: 3px solid white;
            margin-bottom: 12px;
        }
        .header-top h1 {
            color: white;
            margin: 0;
            font-size: 1.6rem;
        }

        /* MAIN CONTENIDO */
        .contenido-ppal {
            display: flex;
            gap: 30px;
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 var(--espaciado-ppal) 30px;
        }
        .rect-uno, .rect-dos {
            background: white;
            border-radius: var(--borde-radio);
            box-shadow: var(--sombra-card);
            padding: 20px;
            border: 3px solid var(--color-secundario);
        }
        .rect-uno { flex: 0 0 40%; }
        .rect-dos { flex: 0 0 60%; }

        /* SECCIONES SINTAXIS Y DESARROLLO */
        .sect-ppal1, .sect-ppal2 {
            max-width: 1200px;
            margin: 10px auto 40px;
            padding: 0 var(--espaciado-ppal);
        }
        .sect-ppal1 > h1, .sect-ppal2 > h1 {
            text-align: center;
            color: var(--color-ppal);
            margin: 30px 0 20px;
        }
        .doble-columna {
            display: flex;
            gap: 25px;
            margin-bottom: 40px;
        }
        .section1, .section1a {
            flex: 1;
            background: white;
            padding: 20px;
            border-radius: var(--borde-radio);
            box-shadow: var(--sombra-card);
        }
        .section1 {
            border-left: 7px solid var(--color-ppal);
            border-bottom: 7px solid var(--color-secundario);
            border-top: 2px solid var(--color-ppal);
            border-right: 2px solid var(--color-secundario);
        }
        .section1a {
            border-left: 7px solid var(--color-ppal);
            border-bottom: 7px solid var(--color-secundario);
            border-top: 2px solid var(--color-ppal);
            border-right: 2px solid var(--color-secundario);
        }

        /* EJERCICIOS */
        .ejercicios-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 30px;
        }
        .ejercicio-card {
            background: white;
            padding: 20px;
            border-radius: var(--borde-radio);
            box-shadow: var(--sombra-card);
            position: relative;
            border-left: 7px solid var(--color-ppal);
            border-bottom: 7px solid var(--color-secundario);
            border-top: 2px solid var(--color-ppal);
            border-right: 2px solid var(--color-secundario);
        }
        .ejercicio-par { border-left: 2px solid var(--color-ppal); }
        .ejercicio-par::before {
            content: "";
            position: absolute;
            top: 0;
            bottom: 0;
            left: -15px;
            width: 2px;
            background-color: var(--color-ppal);
        }
        .ejercicio-card h3 {
            color: var(--color-ppal);
            margin-top: 0;
        }
        .formula {
            background-color: #f0f4ff;
            padding: 8px 12px;
            border-radius: 4px;
            font-family: monospace;
            margin: 10px 0;
            display: inline-block;
        }
        .resultado {
            font-weight: bold;
            color: var(--color-secundario);
        }

        /* FOOTER */
        .app-footer {
            background-color: #37474f;
            color: white;
            padding: 25px 0;
            text-align: center;
            margin-top: 40px;
        }
        .contenido-pie { max-width: 1200px; margin: 0 auto; padding: 0 var(--espaciado-ppal); }
        .footer-links a {
            color: #b0bec5;
            margin: 0 8px;
            font-size: 0.85em;
            white-space: nowrap;
        }
        .footer-links a:hover { color: white; }

        /* BOTONES DE IDIOMA */
        .language-selector {
            display: flex;
            gap: 6px;
            margin-top: 15px;
        }
        .language-selector button {
            background: none;
            border: 1px solid white;
            color: white;
            padding: 5px 10px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 0.9em;
        }
        .language-selector button.active {
            background: white;
            color: var(--color-ppal);
            font-weight: bold;
        }

        /* RESPONSIVE */
        @media (max-width: 900px) {
            .contenido-ppal, .doble-columna, .ejercicios-grid {
                flex-direction: column;
                grid-template-columns: 1fr;
            }
            .ejercicio-par::before { display: none; }
            .rect-uno, .rect-dos { flex: 1; }
        }
    </style>
</head>
<body class="theme-es">
    <header>
        <div class="header-top">
            <img src="Aula virtual de clase.png" alt="Luis Salinas" class="img-office">
            <h1 data-lang-key="titulo-pagina">Función BUSCARV en Excel</h1>
            <div class="language-selector">
                <button data-lang="es">ES</button>
                <button data-lang="en">EN</button>
                <button data-lang="ca">CA</button>
                <button data-lang="fr">FR</button>
            </div>
        </div>
    </header>

    <main>
        <div class="contenido-ppal">
            <div class="rect-uno">
                <img src="Profesor Salinas - Funcion.png" alt="Función BUSCARV" style="width:100%; border-radius:8px;">
            </div>
            <div class="rect-dos">
                <p data-lang-key="descripcion-buscarv">La función <strong>BUSCARV</strong> (o VLOOKUP en inglés) busca un valor en la primera columna de una tabla y devuelve un valor en la misma fila desde una columna especificada. Es esencial para vincular datos entre tablas.</p>
            </div>
        </div>

        <section class="sect-ppal1">
            <h1 data-lang-key="sintaxis-y-desarrollo">Sintaxis y Desarrollo</h1>
            <div class="doble-columna">
                <section class="section1">
                    <h2 data-lang-key="sintaxis">Sintaxis</h2>
                    <p data-lang-key="sintaxis-texto">La sintaxis de la función BUSCARV es:</p>
                    <div class="formula">=BUSCARV(valor_buscado; tabla_matriz; núm_columna; [rango_verdadero])</div>
                    <ul>
                        <li data-lang-key="sintaxis-li1"><strong>valor_buscado</strong>: valor a buscar (en la primera columna de la tabla).</li>
                        <li data-lang-key="sintaxis-li2"><strong>tabla_matriz</strong>: rango que contiene los datos.</li>
                        <li data-lang-key="sintaxis-li3"><strong>núm_columna</strong>: número de columna (desde la izquierda de la tabla) del valor a devolver.</li>
                        <li data-lang-key="sintaxis-li4"><strong>rango_verdadero</strong>: FALSO para coincidencia exacta (recomendado), VERDADERO para aproximada.</li>
                    </ul>
                </section>
                <section class="section1a">
                    <h2 data-lang-key="desarrollo">Desarrollo</h2>
                    <p data-lang-key="desarrollo-texto">Ejemplo: <span class="formula">=BUSCARV("Lápiz"; A2:D10; 3; FALSO)</span> busca "Lápiz" en la columna A y devuelve el valor de la columna C (tercera columna del rango).</p>
                    <p data-lang-key="desarrollo-texto2">⚠️ La búsqueda se hace siempre en la <strong>primera columna</strong> del rango. Si no se encuentra el valor y se usa FALSO, devuelve #N/A.</p>
                </section>
            </div>
        </section>

        <section class="sect-ppal2">
            <h1 data-lang-key="ejercicios-practica">Ejercicios de Práctica</h1>
            <div class="ejercicios-grid" id="ejercicios-container">
                <!-- Los ejercicios se generarán con JavaScript -->
            </div>
        </section>
    </main>

    <footer class="app-footer">
        <div class="contenido-pie">
            <p data-lang-key="copyright">&copy; Noviembre 2025 - Luis M. Salinas</p>
            <div class="footer-links">
                <a href="#" data-lang-key="politica-privacidad">🔋 Política de Privacidad</a>
                <a href="#" data-lang-key="terminos-uso">⏳ Términos de Uso</a>
                <a href="#" data-lang-key="contacto-footer">🛂 Contacto: Luis M. Salinas - Tecnólogo Electrónico - UDO</a>
                <a href="#" data-lang-key="telefono">☎️ Teléfono: +34 673 484 940</a>
                <a href="#" data-lang-key="soporte-tecnico">⚒️ Soporte Técnico: Diseño y Confección de Páginas Web | Desarrollo de Agentes y Workflows en Make</a>
                <a href="#" data-lang-key="email">📧 Email: lsalinasuban@gmail.com</a>
            </div>
        </div>
    </footer>

    <script>
        const translations = {
            'es': {
                'titulo-pagina': 'Función BUSCARV en Excel',
                'descripcion-buscarv': 'La función <strong>BUSCARV</strong> (o VLOOKUP en inglés) busca un valor en la primera columna de una tabla y devuelve un valor en la misma fila desde una columna especificada. Es esencial para vincular datos entre tablas.',
                'sintaxis-y-desarrollo': 'Sintaxis y Desarrollo',
                'sintaxis': 'Sintaxis',
                'sintaxis-texto': 'La sintaxis de la función BUSCARV es:',
                'sintaxis-li1': '<strong>valor_buscado</strong>: valor a buscar (en la primera columna de la tabla).',
                'sintaxis-li2': '<strong>tabla_matriz</strong>: rango que contiene los datos.',
                'sintaxis-li3': '<strong>núm_columna</strong>: número de columna (desde la izquierda de la tabla) del valor a devolver.',
                'sintaxis-li4': '<strong>rango_verdadero</strong>: FALSO para coincidencia exacta (recomendado), VERDADERO para aproximada.',
                'desarrollo': 'Desarrollo',
                'desarrollo-texto': 'Ejemplo: <span class="formula">=BUSCARV("Lápiz"; A2:D10; 3; FALSO)</span> busca "Lápiz" en la columna A y devuelve el valor de la columna C (tercera columna del rango).',
                'desarrollo-texto2': '⚠️ La búsqueda se hace siempre en la <strong>primera columna</strong> del rango. Si no se encuentra el valor y se usa FALSO, devuelve #N/A.',
                'ejercicios-practica': 'Ejercicios de Práctica',
                'ejercicio-titulo': 'Ejercicio',
                'datos': 'Datos:',
                'formula': 'Fórmula:',
                'resultado': 'Resultado:',
                'copyright': '© Noviembre 2025 - Luis M. Salinas',
                'contacto': '✉️ Contacto',
                'email': '📧 lsalinasuban@gmail.com'
            },
            'en': {
                'titulo-pagina': 'VLOOKUP Function in Excel',
                'descripcion-buscarv': 'The <strong>VLOOKUP</strong> function searches for a value in the first column of a table and returns a value in the same row from a specified column. Essential for linking data across tables.',
                'sintaxis-y-desarrollo': 'Syntax and Explanation',
                'sintaxis': 'Syntax',
                'sintaxis-texto': 'The VLOOKUP syntax is:',
                'sintaxis-li1': '<strong>lookup_value</strong>: value to search for (in the first column).',
                'sintaxis-li2': '<strong>table_array</strong>: range containing the data.',
                'sintaxis-li3': '<strong>col_index_num</strong>: column number (from left) to return.',
                'sintaxis-li4': '<strong>range_lookup</strong>: FALSE for exact match (recommended), TRUE for approximate.',
                'desarrollo': 'Explanation',
                'desarrollo-texto': 'Example: <span class="formula">=VLOOKUP("Pencil", A2:D10, 3, FALSE)</span> searches "Pencil" in column A and returns value from column C.',
                'desarrollo-texto2': '⚠️ Search is always in the <strong>first column</strong> of the range. If not found with FALSE, returns #N/A.',
                'ejercicios-practica': 'Practice Exercises',
                'ejercicio-titulo': 'Exercise',
                'datos': 'Data:',
                'formula': 'Formula:',
                'resultado': 'Result:',
                'copyright': '© November 2025 - Luis M. Salinas',
                'contacto': '✉️ Contact',
                'email': '📧 lsalinasuban@gmail.com'
            },
            'ca': {
                'titulo-pagina': 'Funció BUSCARV a Excel',
                'descripcion-buscarv': 'La funció <strong>BUSCARV</strong> busca un valor a la primera columna d’una taula i en retorna un altre de la mateixa fila d’una columna especificada. És essencial per enllaçar dades entre taules.',
                'sintaxis-y-desarrollo': 'Sintaxi i Desenvolupament',
                'sintaxis': 'Sintaxi',
                'sintaxis-texto': 'La sintaxi de BUSCARV és:',
                'sintaxis-li1': '<strong>valor_buscat</strong>: valor a cercar (a la primera columna).',
                'sintaxis-li2': '<strong>taula_matriu</strong>: rang que conté les dades.',
                'sintaxis-li3': '<strong>núm_columna</strong>: número de columna (des de l’esquerra) del valor a retornar.',
                'sintaxis-li4': '<strong>rang_veritable</strong>: FALS per coincidència exacta (recomanat), CERT per aproximada.',
                'desarrollo': 'Desenvolupament',
                'desarrollo-texto': 'Exemple: <span class="formula">=BUSCARV("Llapis"; A2:D10; 3; FALS)</span> cerca "Llapis" a la columna A i en retorna el valor de la columna C.',
                'desarrollo-texto2': '⚠️ La cerca es fa sempre a la <strong>primera columna</strong> del rang. Si no es troba amb FALS, retorna #N/A.',
                'ejercicios-practica': 'Exercicis pràctics',
                'ejercicio-titulo': 'Exercici',
                'datos': 'Dades:',
                'formula': 'Fórmula:',
                'resultado': 'Resultat:',
                'copyright': '© Novembre 2025 - Luis M. Salinas',
                'contacto': '✉️ Contacte',
                'email': '📧 lsalinasuban@gmail.com'
            },
            'fr': {
                'titulo-pagina': 'Fonction RECHERCHEV dans Excel',
                'descripcion-buscarv': 'La fonction <strong>RECHERCHEV</strong> recherche une valeur dans la première colonne d’un tableau et renvoie une valeur de la même ligne depuis une colonne spécifiée. Essentielle pour lier des données entre tableaux.',
                'sintaxis-y-desarrollo': 'Syntaxe et Explication',
                'sintaxis': 'Syntaxe',
                'sintaxis-texto': 'La syntaxe de RECHERCHEV est :',
                'sintaxis-li1': '<strong>valeur_cherchée</strong> : valeur à rechercher (dans la première colonne).',
                'sintaxis-li2': '<strong>table_matrice</strong> : plage contenant les données.',
                'sintaxis-li3': '<strong>no_index_col</strong> : numéro de colonne (depuis la gauche) à renvoyer.',
                'sintaxis-li4': '<strong>valeur_proche</strong> : FAUX pour correspondance exacte (recommandé), VRAI pour approximative.',
                'desarrollo': 'Explication',
                'desarrollo-texto': 'Exemple : <span class="formula">=RECHERCHEV("Crayon"; A2:D10; 3; FAUX)</span> cherche "Crayon" en colonne A et renvoie la valeur de la colonne C.',
                'desarrollo-texto2': '⚠️ La recherche se fait toujours dans la <strong>première colonne</strong> de la plage. Si non trouvé avec FAUX, renvoie #N/A.',
                'ejercicios-practica': 'Exercices pratiques',
                'ejercicio-titulo': 'Exercice',
                'datos': 'Données :',
                'formula': 'Formule :',
                'resultado': 'Résultat :',
                'copyright': '© Novembre 2025 - Luis M. Salinas',
                'contacto': '✉️ Contact',
                'email': '📧 lsalinasuban@gmail.com'
            }
        };

        // Datos de los 10 ejercicios para BUSCARV
        const ejercicios = [
            { datos: '"Producto A", Tabla A2:C5, col 2', formula: '=BUSCARV("Producto A";A2:C5;2;FALSO)', resultado: '"Lápiz"' },
            { datos: '"ID101", Rango F1:H4, col 3', formula: '=BUSCARV("ID101";F1:H4;3;FALSO)', resultado: '25' },
            { datos: 'B2 (valor="X"), Tabla D2:F6, col 2', formula: '=BUSCARV(B2;D2:F6;2;FALSO)', resultado: '"Rojo"' },
            { datos: '"Ana", A1:C3, col 3', formula: '=BUSCARV("Ana";A1:C3;3;FALSO)', resultado: '85' },
            { datos: '"Z", Tabla (no existe)', formula: '=BUSCARV("Z";A1:B10;2;FALSO)', resultado: '#N/A' },
            { datos: '100, Tabla G1:I5, col 3', formula: '=BUSCARV(100;G1:I5;3;FALSO)', resultado: '"Alto"' },
            { datos: '"Clave2", J2:L6, col 2', formula: '=BUSCARV("Clave2";J2:L6;2;FALSO)', resultado: '"Módulo B"' },
            { datos: '"Producto C", A2:C5, col 1', formula: '=BUSCARV("Producto C";A2:C5;1;FALSO)', resultado: '"Producto C"' },
            { datos: '"Error404", Rango M1:O3, col 2', formula: '=BUSCARV("Error404";M1:O3;2;FALSO)', resultado: '#N/A' },
            { datos: '"Carlos", P1:R4, col 3', formula: '=BUSCARV("Carlos";P1:R4;3;FALSO)', resultado: '92' }
        ];

        function renderExercises(lang) {
            const container = document.getElementById('ejercicios-container');
            container.innerHTML = '';
            const t = translations[lang];

            ejercicios.forEach((ej, i) => {
                const num = i + 1;
                const card = document.createElement('div');
                card.className = `ejercicio-card ${num % 2 === 0 ? 'ejercicio-par' : ''}`;
                card.innerHTML = `
                    <h3>${t['ejercicio-titulo']} ${num}</h3>
                    <p><strong>${t['datos']}</strong> ${ej.datos}</p>
                    <p><strong>${t['formula']}</strong> <span class="formula">${ej.formula}</span></p>
                    <p><strong>${t['resultado']}</strong> <span class="resultado">${ej.resultado}</span></p>
                `;
                container.appendChild(card);
            });
        }

        function setLanguage(lang) {
            const elements = document.querySelectorAll('[data-lang-key]');
            const t = translations[lang];
            document.body.className = document.body.className.replace(/\btheme-\w+\b/g, '').trim();
            document.body.classList.add(`theme-${lang}`);

            elements.forEach(el => {
                const key = el.dataset.langKey;
                if (t[key]) {
                    // Usar innerHTML solo si contiene etiquetas HTML
                    if (key === 'descripcion-buscarv' || key === 'desarrollo-texto' || key === 'desarrollo-texto2') {
                        el.innerHTML = t[key];
                    } else {
                        el.textContent = t[key];
                    }
                }
            });

            // Actualizar botones de idioma
            document.querySelectorAll('.language-selector button').forEach(btn => {
                btn.classList.toggle('active', btn.dataset.lang === lang);
            });

            // Renderizar ejercicios
            renderExercises(lang);

            localStorage.setItem('userLang', lang);
        }

        document.addEventListener('DOMContentLoaded', () => {
            const savedLang = localStorage.getItem('userLang') || 'es';
            setLanguage(savedLang);

            // Evento cambio de idioma
            document.querySelectorAll('.language-selector button').forEach(btn => {
                btn.addEventListener('click', () => setLanguage(btn.dataset.lang));
            });
        });
    </script>
</body>
</html>


Primera Modificación
Perfecto, Luis. Vamos a mejorar tu página de forma integral para convertirla en una herramienta educativa interactiva, accesible y profesional. A continuación te presento el HTML actualizado con todos los cambios solicitados:

✅ Cambios implementados:
Nombres de clases CSS más semánticos: rect-uno → intro-media, rect-dos → intro-text.
Mejor manejo de imágenes: fallback con onerror y atributos alt descriptivos.
Botón “Copiar fórmula” en cada ejercicio (con retroalimentación visual).
Soporte de traducción en el footer completo.
Ejercicios interactivos: el usuario puede editar el valor buscado y ver el resultado simulado en tiempo real.
Simulador interactivo adicional (sección nueva) para practicar con una tabla de ejemplo.
Validación visual de errores (como #N/A si no se encuentra).
Mejoras de accesibilidad: lang dinámico, aria-live para mensajes, etc.
📄 Código HTML actualizado:
html
<!DOCTYPE html>

        // Inicializar simulador
        document.getElementById('input-valor-buscar').addEventListener('input', simularBusqueda);
        document.getElementById('input-columna').addEventListener('input', simularBusqueda);

        function setLanguage(lang) {
            const elements = document.querySelectorAll('[data-lang-key]');
            const t = translations[lang];
            document.body.className = document.body.className.replace(/\btheme-\w+\b/g, '').trim();
            document.body.classList.add(`theme-${lang}`);
            document.documentElement.setAttribute('lang', lang);

            elements.forEach(el => {
                const key = el.dataset.langKey;
                if (t[key]) {
                    if (['descripcion-buscarv', 'desarrollo-texto', 'desarrollo-texto2'].includes(key)) {
                        el.innerHTML = t[key];
                    } else {
                        el.textContent = t[key];
                    }
                }
            });

            document.querySelectorAll('.language-selector button').forEach(btn => {
                btn.classList.toggle('active', btn.dataset.lang === lang);
            });

            renderExercises(lang);

            // Actualizar textos en ejercicios (etiqueta "Valor a buscar")
            if (t['valor-a-buscar']) {
                document.querySelectorAll('[data-lang-key="valor-a-buscar"]')?.forEach(el => {
                    el.textContent = t['valor-a-buscar'];
                });
            }

            localStorage.setItem('userLang', lang);
        }

        document.addEventListener('DOMContentLoaded', () => {
            const savedLang = localStorage.getItem('userLang') || 'es';
            setLanguage(savedLang);

            document.querySelectorAll('.language-selector button').forEach(btn => {
                btn.addEventListener('click', () => setLanguage(btn.dataset.lang));
            });
        });
    </script>
</body>
</html>
🔧 Notas finales:
Los ejercicios ahora son interactivos: el estudiante puede cambiar el valor buscado y ver el resultado en tiempo real.
Simulador realista: usa una tabla interna y muestra resultados como Excel.
Todo el footer se traduce.
Clases CSS renombradas a intro-media y intro-text.
Manejo seguro de imágenes: si fallan, se muestran placeholders.
Accesible y moderno.
¿Quieres que lo exporte como archivo .html descargable, o que lo integre en un entorno tipo CodePen o GitHub Pages? También puedo ayudarte a empaquetarlo para Moodle o tu Aula Virtual.








# php-soda-MIN

Una biblioteca PHP para trabajar con la API de datos abiertos de Socrata. Proporcionada como una alternativa a la implementación oficial de Socrata, esta biblioteca llena las deficiencias de la biblioteca oficial al proporcionar más funcionalidad, un enfoque más orientado a objetos, documentación y mucho código de ejemplo.

Esta biblioteca es totalmente compatible con la interacción con la API de datos abiertos de Socrata (SODA) mediante la obtención de conjuntos de datos, el manejo de tokens, el manejo de autenticación básica y tokens OAuth2.0 para escribir o modificar conjuntos de datos.

# Requisitos
PHP 5.6+

# Instalación
Esta biblioteca está disponible en Packagist como allejo / php-soda, agréguela usando Composer.

¿No estás usando Composer? No se preocupe, esta biblioteca también se proporciona como un archivo Phar para que la incluya en su código. Obtenga el último archivo de Phar de nuestros lanzamientos.

Consulte nuestro artículo wiki si necesita ayuda para usar esta biblioteca.

# Utilización básica
Aquí hay algunos ejemplos rápidos sobre cómo funciona PhpSoda, pero hay mucho más que puede hacer. Consulte nuestra wiki para ver todo lo demás.

# Obtener un dataset

// Create a client with information about the API to handle tokens and authentication
$sc = new SodaClient("opendata.socrata.com");

// Access a dataset based on the API end point
$ds = new SodaDataset($sc, "pkfj-5jsd");

// Create a SoqlQuery that will be used to filter out the results of a dataset
$soql = new SoqlQuery();

// Write a SoqlQuery naturally
$soql->select("date_posted", "state", "sample_type")
     ->where("state = 'AR'")
     ->limit(1);

// Fetch the dataset into an associative array
$results = $ds->getDataset($soql);
Updating a dataset

// Create a client with information about the API to handle tokens and authentication
$sc = new SodaClient("opendata.socrata.com", "<token here>", "email@example.com", "password");

// The dataset to upload
$data = file_get_contents("dataset.json");

// Access a dataset based on the API end point
$ds = new SodaDataset($sc, "1234-abcd");

// To upsert a dataset
$ds->upsert($data);

// To replace a dataset
$ds->replace($data);
Note: This library supports writing directly to datasets with the Socrata Open Data API. For datasets with one or more data transformations applied to the schema through the Socrata Data Management Experience (the user interface for creating datasets), use the Socrata Data Management API to apply those same transformations to all updates. For more details on when to use SODA vs the Socrata Data Management API, see the Data Management API documentation

Getting Help
To get help, see if our wiki has any information regarding your question. If the wiki can't help you, you may either create an issue or stop by IRC; I'm available on IRC as "allejo" so feel free to ping me. I recommend creating an issue in case others have the same question but for quick help, IRC works just fine.

To report a bug or request a feature, please submit an issue.

IRC
Channel: #socrata-soda
Network: irc.freenode.net

Thank You
Official Socrata PHP Library
C# Socrata Library
License
MIT

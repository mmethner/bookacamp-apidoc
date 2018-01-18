php-apidoc
==========

Generate documentation for php API based application. No dependency. No framework required.

* [Requirements](#requirements)
* [Installation](#installation)
* [Usage](#usage)
* [Available Methods](#methods)
* [Credits](#credits)

### <a id="requirements"></a>Requirements

PHP >= 5.3.2

### <a id="installation"></a>Installation

The recommended installation is via composer. Just add the following line to your composer.json:

```json
{
    ...
    "repositories": [
    {
        "type": "vcs",
        "url": "https://github.com/mmethner/php-apidoc"
    }
    ],
    "require": {
        ...
        "mmethner/php-apidoc": "dev-bookacamp"
    }
}
```

```bash
$ php composer.phar update
```
### <a id="usage"></a>Usage

```php
<?php

namespace Some\Namespace;

class User
{
    /**
     * @ApiDescription(section="User", description="Get information about user")
     * @ApiMethod(type="get")
     * @ApiRoute(name="/user/get/{id}")
     * @ApiParams(name="id", type="integer", nullable=false, description="User id")
     * @ApiParams(name="data", type="object", sample="{'user_id':'int','user_name':'string','profile':{'email':'string','age':'integer'}}")
     * @ApiReturnHeaders(sample="HTTP 200 OK")
     * @ApiReturn(type="object", sample="{
     *  'transaction_id':'int',
     *  'transaction_status':'string'
     * }")
     */
    public function get()
    {

    }

    /**
     * @ApiDescription(section="User", description="Create's a new user")
     * @ApiMethod(type="post")
     * @ApiRoute(name="/user/create")
     * @ApiParams(name="username", type="string", nullable=false, description="Username")
     * @ApiParams(name="email", type="string", nullable=false, description="Email")
     * @ApiParams(name="password", type="string", nullable=false, description="Password")
     * @ApiParams(name="age", type="integer", nullable=true, description="Age")
     */
    public function create()
    {

    }
}
```

Create an apidoc.php file in your project root folder as follow:


```php
# apidoc.php
<?php

use Crada\Apidoc\Builder;
use Crada\Apidoc\Exception;

$classes = array(
    'Some\Namespace\User',
    'Some\Namespace\OtherClass',
);

$output_dir  = __DIR__.'/apidocs';
$output_file = 'api.html'; // defaults to index.html

try {
    $builder = new Builder($classes, $output_dir, 'Api Title', $output_file);
    $builder->generate();
} catch (Exception $e) {
    echo 'There was an error generating the documentation: ', $e->getMessage();
}

```

Then, execute it via CLI

```php
$ php apidoc.php
```

### <a id="methods"></a>Available Methods

Here is the list of methods available so far :

* @ApiDescription(section="...", description="...")
* @ApiMethod(type="(get|post|put|delete|patch")
* @ApiRoute(name="...")
* @ApiParams(name="...", type="...", nullable=..., description="...", [sample=".."])
* @ApiHeaders(name="...", type="...", nullable=..., description="...")
* @ApiReturnHeaders(sample="...")
* @ApiReturn(type="...", sample="...")
* @ApiBody(sample="...")

### <a id="credits"></a>Credits

Thanks to the work of Calin Rada.    
This project is based on the work of https://github.com/calinrada/php-apidoc
and customized to fit for www.bookacamp.de


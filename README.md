bookacamp-apidoc
==========

Generate documentation for www.bookacamp.de api.

For general purpose php api documentation see https://github.com/calinrada/php-apidoc

* [Requirements](#requirements)
* [Installation](#installation)
* [Usage](#usage)
* [Available Methods](#methods)
* [Credits](#credits)

### <a id="requirements"></a>Requirements

PHP >= 7.1

### <a id="installation"></a>Installation

The recommended installation is via composer. Just add the following line to your composer.json:

```json
{
    ...
    "repositories": [
    {
        "type": "vcs",
        "url": "https://github.com/mmethner/bookacamp-apidoc"
    }
    ],
    "require": {
        ...
        "mmethner/bookacamp-apidoc": "dev-bookacamp"
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
     * @ApiParams(name="id", type="integer", required=false, description="User id")
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
     * @ApiParams(name="username", type="string", required=false, description="Username")
     * @ApiParams(name="email", type="string", required=false, description="Email")
     * @ApiParams(name="password", type="string", required=false, description="Password")
     * @ApiParams(name="age", type="integer", required=true, description="Age")
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

use Bookacamp\Apidoc\Builder;

$classes = array(
    'Some\Namespace\User',
    'Some\Namespace\OtherClass',
);

$outputDir  = __DIR__.'/apidocs';
$outputFile = 'api.html'; // defaults to index.html

try {
    $builder = new Builder($classes, $outputDir, 'Api Title', $outputFile);
    $builder->generate();
} catch (\Exception $e) {
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
* @ApiParams(name="...", type="...", required=..., description="...", [sample=".."])
* @ApiHeaders(name="...", type="...", required=..., description="...")
* @ApiReturnHeaders(sample="...")
* @ApiReturn(type="...", sample="...")
* @ApiBody(sample="...")

### <a id="credits"></a>Credits

Thanks to the work of Calin Rada.    
This project is based on the work of https://github.com/calinrada/php-apidoc
and customized to fit for www.bookacamp.de


# tree-parser

[![Latest Stable Version](https://poser.pugx.org/baopham/tree-parser/v/stable)](https://packagist.org/packages/baopham/tree-parser)
[![Software License][ico-license]](LICENSE.md)
[![Build Status](https://travis-ci.org/baopham/php-tree-parser.svg?branch=master)](https://travis-ci.org/baopham/php-tree-parser)
[![Code Coverage](https://scrutinizer-ci.com/g/baopham/php-tree-parser/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/baopham/php-tree-parser/?branch=master)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/baopham/php-tree-parser/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/baopham/php-tree-parser/?branch=master)

Parse this:

```
   Root
     |- Level 1.1
       |- Level 2.1
     |- Level 1.2
       |- Level 2.2
         |- Level 3
           |- Level 4
```


to this:

```php
foreach ($root->children as $child) {
    print $child->name;

    print $child->order;

    print $child->level;

    print_r($child->children);

    print_r($child->children[0]->children);

    print $child->children[0]->parent === $child;
}
```

## Table of Content
* [Install](#install)
* [Usage](#usage)
  * [Advanced](#advanced)
* [Change log](#change-log)
* [Testing](#testing)
* [Contributing](#contributing)
* [Credits](#credits)
* [License](#license)

## Install

Via Composer

``` bash
$ composer require baopham/tree-parser
```

## Usage

``` php
// A tree with 2 spaces for indentation
$tree = <<<TREE
  Root
    |- Level 1 - Order 1
      |- Level 2 - Order 2
        |- Level 3 - Order 3
        |- Level 3 - Order 4
      |- Level 2 - Order 5
    |- Level 1 - Order 6
      |- Level 2 - Order 7
        |- Level 3 - Order 8
          |- Level 4 - Order 9
TREE;

$parser = new BaoPham\TreeParser($tree);

$parser->setIndentation(2); // number of spaces for an indentation, 2 is the default.

$root = $parser->parse();

foreach ($root->children as $child) {
    print $child->name;

    print $child->order;

    print $child->level;

    print_r($child->children);

    print_r($child->children[0]->children);

    print $child->children[0]->parent === $child;
}
```

### Advanced

```php
$tree = <<<TREE
  Root
    |- Level 1 - Order 1
      |- Level 2 - Order 2
        |- Level 3 - Order 3
        |- Level 3 - Order 4
      |- Level 2 - Order 5
    |- Level 1 - Order 6
      |- Level 2 - Order 7
        |- Level 3 - Order 8
          |- Level 4 - Order 9
TREE;

$parser = new BaoPham\TreeParser($tree);

$parser->parse();

$structure = $parser->getStructure();

// Get nodes at level 3
$level3Nodes = $structure[3];
// Get node at level 3, order 4
$node = $structure[3][4];

// Get last leaf
$orderedNodes = $parser->getOrderedNodes();
$lastLeaf = $orderedNodes[count($orderedNodes) - 1];
```


## Change log

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Testing

``` bash
$ composer test
```

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) and [CONDUCT](CONDUCT.md) for details.

## Credits

- [Bao Pham](https://github.com/baopham)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

[ico-version]: https://img.shields.io/packagist/v/baopham/tree-parser.svg?style=flat-square
[ico-license]: https://img.shields.io/badge/license-MIT-brightgreen.svg?style=flat-square
[ico-travis]: https://img.shields.io/travis/baopham/tree-parser/master.svg?style=flat-square
[ico-scrutinizer]: https://img.shields.io/scrutinizer/coverage/g/baopham/tree-parser.svg?style=flat-square
[ico-code-quality]: https://img.shields.io/scrutinizer/g/baopham/tree-parser.svg?style=flat-square
[ico-downloads]: https://img.shields.io/packagist/dt/baopham/tree-parser.svg?style=flat-square

[link-packagist]: https://packagist.org/packages/baopham/tree-parser
[link-travis]: https://travis-ci.org/baopham/tree-parser
[link-scrutinizer]: https://scrutinizer-ci.com/g/baopham/tree-parser/code-structure
[link-code-quality]: https://scrutinizer-ci.com/g/baopham/tree-parser
[link-downloads]: https://packagist.org/packages/baopham/tree-parser
[link-author]: https://github.com/baopham
[link-contributors]: ../../contributors

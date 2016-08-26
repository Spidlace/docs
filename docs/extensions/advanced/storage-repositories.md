---
title: Storage Repositories & Entity Mappings
---
Storage Repositories & Entity Mappings
======================================

Bolt 3 comes with an extensible [storage interface](/3.0/extensions/storage/introduction). 

If your extension needs to register [entity](/3.0/extensions/storage/entities) 
and [repository](/3.0/extensions/storage/repositories) mappings, 
your extension loader class should import `StorageTrait`, implement the 
`registerRepositoryMappings()` function and call `extendRepositoryMapping()` in 
your extension loader class.

#### Example

```php
namespace Bolt\Extension\DropBear\KoalaCatcher;

use Bolt\Extension\DropBear\KoalaCatcher\Storage\Entity;
use Bolt\Extension\DropBear\KoalaCatcher\Storage\Repository;
use Bolt\Extension\SimpleExtension;
use Bolt\Extension\StorageTrait;
use Silex\Application;

/**
 * An extension for catching koalas.
 *
 * @author Kenny Koala <kenny@dropbear.com.au>
 */
class KoalaCatcherExtension extends SimpleExtension
{
    use StorageTrait;

    /**
     * {@inheritdoc}
     */
    protected function registerServices(Application $app)
    {
        $this->extendRepositoryMapping();
    }

    /**
     * {@inheritdoc}
     */
    protected function registerRepositoryMappings()
    {
        return [
            'gumtree' => [Entity\GumTree::class => Repository\GumTree::class],
        ];
    }
```

**Note:** The above example uses "class name resolution" via the `::class` keyword.
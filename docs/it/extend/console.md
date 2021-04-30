# Console

Flarum consente agli sviluppatori di estensioni di aggiungere comandi personalizzati nella console oltre a [quelli di default](../console.md) insiti nel core di Flarum.

Tutto lo sviluppo dei comandi della console viene eseguito nel back-end utilizzando PHP. Per creare un comando della console personalizzato, dovrai creare una classe che estende `\Flarum\Console\AbstractCommand`.

```php
use Flarum\Console\AbstractCommand;
use Psr\Http\Message\ServerRequestInterface;
use Psr\Http\Server\MiddlewareInterface;
use Psr\Http\Server\RequestHandlerInterface;

class YourCommand implements AbstractCommand {
  protected function configure()
  {
      $this
          ->setName('IL TUO COMANDO QUI')
          ->setDescription('LA DESCRIZIONE DLE TUO COMANDO');
  }
  protected function fire()
  {
    // La tua logica qui!
  }
}
```

## Registrazione dei comandi della Console

Per registrare i comandi della console, usa l'estensore `Flarum\Extend\Console` nel file `extend.php` della tua estensione:

```php
use Flarum\Extend;
use YourNamespace\Console\CustomCommand;

return [
  // Other extenders
  (new Extend\Console())->command(CustomCommand::class)
  // Other extenders
];
```

::: tip Scheduled Commands

The [fof/console library](https://github.com/FriendsOfFlarum/console) allows you to schedule commands to run on a regular interval! However, please note that this is a community solution.

:::

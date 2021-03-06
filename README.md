# League Event Bundle for Symfony2

## Installation

```
composer require frankdejonge/league-event-bundle
```

Register the bundle:

```php
$bundles = array(
    ...
    new FrankDeJonge\LeagueEventBundle\LeagueEventBundle(),
    ...
);
```

## Usage

By default an emitter is registered under the `league_event.emitter` id.

```php
$emitter = $container->get('league_event.emitter');
```

Event listeners can be added to the emitter by tagging it with `league_event.emitter`.

```yaml
---
services:
    my_listener:
        class: Some\Listener
        tags:
            - name: league_event.listener
              event: event.name
```

## Advanced usage

Register custom emitters with custom listener bindings:

```yml
---
services:
    my_emitter:
        class: League\Event\Emitter
        tags:
            - name: league_event.emitter
              listener_tag: my_emitter.listener
    my_listener:
        class: My\Awesome\Listener
        tags:
            - name: my_emitter.listener
              event: My\Awesome\DomainEvent
```

Setting priorities is also possible:

```yml
---
services:
    my_listener:
        class: My\Awesome\Listener
        tags:
            - name: league_event.listener
              event: My\Awesome\DomainEvent
              priority: 9001
```
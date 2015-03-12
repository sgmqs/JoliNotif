# JoliNotif

JoliNotif allows you to send notification to your system directly from your php
script. The notifier will take care to use the right command available, without
having to worry if you're running on Linux, Windows or MacOS.

JoliNotif can be used from your long running task, f.e. to inform your user
that a task just finished. Originally inspired by [mikaelbr/node-notifier](https://github.com/mikaelbr/node-notifier).

## Getting started

Use [Composer](http://getcomposer.org/) to install JoliNotif in your projects:


    composer require "jolicode/jolinotif"


## Usage

The main class is `Notifier`. It should be instantiated with an array of
`Driver`. The `Notifier` constructor will choose the best driver to use,
according to which commands are available on your system.

In order to ease the use of JoliNotif, a `NotifierFactory` take care to create
a `Notifier` with the right drivers according to your system.

Look at below (or [example/index.php](example/index.php)) to see an example on
how to use JoliNotif.

```php
// Build a Notifier
$notifier = NotifierFactory::make();

// Create your notification
$notification = new Notification();
$notification->setTitle('I\'m a notification title');
$notification->setBody('And this is the body');
$notification->setIcon(__DIR__.'/notification-icon.png');

// Send it
$notifier->send($notification);
```

`Notifier#send()` will return one of these values:
- `Notifier::STATUS_SENT` if everything gone well
- `Notifier::STATUS_ERROR_DRIVER` if an error happened in the driver
- `Notifier::STATUS_NO_DRIVER` if not any driver could be used


## Notification options

Currently, only three options are supported:
- title
- body
- icon

> **Important**: The only required property on Notification is the body.
> The notifier will throw an InvalidNotificationException if it is empty.

If you use JoliNotif from a phar and provide your notification icon, the
notifier will take care to extract this image in your system temp directory
to make it accessible for native commands.

> **Note**: New properties could be added later on Notification. Drivers are
> designed to only handle the supported properties and discard not supported
> ones without throwing any exception.

## Further documentation

You can see the current and past versions using one of the following:

* the `git tag` command
* the [releases page on Github](https://github.com/jolicode/JoliNotif/releases)
* the file listing the [changes between versions](CHANGELOG.md)

You can find more documentation at the following links:

* [copyright and MIT license](LICENSE)
* [versioning and branching models](VERSIONING.md)
* [contribution instructions](CONTRIBUTING.md)

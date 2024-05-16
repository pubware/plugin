# 🔌 plugin

## Overview

The abstract `Plugin` class provides a variety of utility methods and lifecycle hooks for creating plugins that integrate directly with [packpub](https://github.com/packpub/packpub).

Plugins can be created for a wide range of functionalities. From publishing `npm` packages and interacting with `git` repositories to integrating with services like Slack, Discord, or even DoorDash.

### 🔥 Features

- 🙋‍♀️ User Prompts
- 📂 File System Operations
- 💻 Shell Execution
- 🌐 HTTP Requests
- 💬 Logging
- 🪝 Lifecycle Hooks

## Requirements

- Node 18+

## Install

Install the `@packpub/plugin` package.

```
npm install @packpub/plugin
```

## Usage

Import the `Plugin` and create a subclass.

```js
import Plugin from '@packpub/plugin'

class YourPlugin extends Plugin {
  constructor() {
    super('YourPlugin')
  }

  init() {
    this.log('Initializing plugin')
  }

  bump() {
    this.log('Bumping version')
  }

  publish() {
    this.log('Publishing package')
  }
}

export default YourPlugin
```

Implement the following hooks to control the plugin's lifecycle:

- `init`: Called when the plugin is initialized.
- `preBump`: Called before the version is bumped.
- `bump`: Called to handle the version bump.
- `prePublish`: Called before the package is published.
- `publish`: Called to handle the publishing process.
- `postPublish`: Called after the package has been published.

Any of the methods can be `async`.

## API

| Method                                                                         | Description                                       |
| ------------------------------------------------------------------------------ | ------------------------------------------------- |
| **log(message: string)**                                                       | Log a message.                                    |
| **prompt(message: string, defaultValue: string = '')**                         | Prompt the user for input.                        |
| **promptConfirm(message: string, defaultValue: boolean = false)**              | Prompt the user for a boolean confirmation.       |
| **promptSelect(message: string, choices: Choices, defaultValue: string = '')** | Prompt the user to select from a list of choices. |
| **read(path: string)**                                                         | Read the content of a file.                       |
| **write(path: string, content: string)**                                       | Write content to a file.                          |
| **exec(cmd: string, options: ExecOptions = { write: true })**                  | Execute a shell command.                          |
| **fetch<T>(url: string, options: RequestInit = {})**                           | Fetch a resource over HTTP.                       |

## Flags

The `Plugin` class supports the use of CLI flags. These flags can be set to modify the execution of various utility methods and lifecycle hooks. The following flags are available:

| Flag         | Description                                                                                                                                                                    |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **dry**      | When set to `true`, the plugin runs in dry mode and no write operations will be performed.                                                                                     |
| **headless** | When set to `true`, the plugin runs in headless mode and user prompts will return default values instead of waiting for input and write-based shell execution will be ignored. |

> [!NOTE]
> Flags are only to be set by packpub internally. You can check against a `flag` value if you need custom functionality.

## Examples

- [npm](https://github.com/packpub/npm)
- [git](https://github.com/packpub/git)

## License

MIT

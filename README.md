# 🔌 plugin

The abstract `Plugin` class provides a variety of utility methods and lifecycle hooks for integrating with [pubware](https://github.com/pubware/pubware). From publishing `npm` packages, pushing changes to `git` repositories, to integrating with services like GitHub, Slack, or DoorDash, plugins can be used for a wide range of functionalities.

### 🔥 Features

- 🙋‍♀️ User Prompts
- 📂 File Operations
- 💻 Shell Execution
- 🌐 HTTP Requests
- 📝 Console Logging
- 🔄 Lifecycle Hooks

Learn more about the [API](#api).

## Requirements

- Node 18+

## Install

Install the `@pubware/plugin` package:

```bash
npm install @pubware/plugin
```

## Usage

Import the `Plugin` and create a subclass:

```js
import Plugin from '@pubware/plugin'

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

## API

### Utility Methods

Leverage utility methods to perform various operations.

| Method                                                                                   | Description                                       |
| ---------------------------------------------------------------------------------------- | ------------------------------------------------- |
| `log(message: string)`                                                                   | Log a message.                                    |
| `prompt(message: string, defaultValue: string): Promise<string>`                         | Prompt the user for input.                        |
| `promptConfirm(message: string, defaultValue: boolean): Promise<boolean>`                | Prompt the user for a boolean confirmation.       |
| `promptSelect(message: string, choices: Choices, defaultValue: string): Promise<string>` | Prompt the user to select from a list of choices. |
| `read(path: string): Promise<string>`                                                    | Read the content of a file.                       |
| `write(path: string, content: string): Promise<void>`                                    | Write content to a file.                          |
| `exec(cmd: string, options: ExecOptions): Promise<void>`                                 | Execute a shell command.                          |
| `fetch<T>(url: string, options: RequestInit): Promise<T>`                                | Fetch a resource over HTTP.                       |

### Lifecycle Hooks

Implement hooks to integrate with the lifecycle.

| Hook            | Description                                  |
| --------------- | -------------------------------------------- |
| `init()`        | Called when the plugin is initialized.       |
| `preBump()`     | Called before the version is bumped.         |
| `bump()`        | Called to handle the version bump.           |
| `prePublish()`  | Called before the package is published.      |
| `publish()`     | Called to handle the publishing process.     |
| `postPublish()` | Called after the package has been published. |

Any hook can be `async`.

## Configuration

Plugins support configuration with a `pubware.json` file or within `package.json`. When an instance is created, the key-value pairs are passed to the plugin.

```json
{
  "plugin": {
    "key": "value"
  }
}
```

## Flags

Plugins support flags that modify the execution of various utility methods and lifecycle hooks:

| Flag       | Description                                                                                            |
| ---------- | ------------------------------------------------------------------------------------------------------ |
| `dry`      | When set to `true`, no write operations will be performed.                                             |
| `headless` | When set to `true`, user prompts will return defaults and write-based shell execution will be ignored. |

> [!IMPORTANT]
> Flags are set from the pubware CLI

## Examples

- [@pubware/npm](https://github.com/pubware/npm)
- [@pubware/git](https://github.com/pubware/git)

## License

MIT

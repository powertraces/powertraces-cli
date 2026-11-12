# PowerTraces CLI

Connect your services to [PowerTraces](https://powertraces.com) in one command. The CLI finds your .NET, Node.js (including Next.js), Python, Go and Spring Boot projects, adds the official OpenTelemetry setup, and shows every change before it makes it.

## Install

macOS and Linux:

```sh
curl -fsSL https://github.com/powertraces/powertraces-cli/releases/latest/download/install.sh | sh
```

Windows (PowerShell):

```powershell
irm https://github.com/powertraces/powertraces-cli/releases/latest/download/install.ps1 | iex
```

Both scripts check the download against `checksums.txt`. Set `POWERTRACES_CLI_VERSION` to install a specific version, or `POWERTRACES_INSTALL_DIR` to choose the folder. You can also download a binary from [Releases](https://github.com/powertraces/powertraces-cli/releases).

## Use

```sh
cd your-project
powertraces init
```

`init` asks for your organization (or server address), ingest key and secret, sends a test span, then adds the setup to each service you pick.

| Command | What it does |
| --- | --- |
| `powertraces init` | Connect the services in this folder |
| `powertraces verify` | Send a test span to check the address, key and secret |
| `powertraces enable <feature>` | Record more: `request-body`, `response-body`, `bodies`, `sql`, `sql-params` |
| `powertraces disable <feature>` | Stop recording one of those |
| `powertraces exclude /health,/metrics` | Don't trace these paths |
| `powertraces redact national_id,iban` | Mask these extra body fields and headers |
| `powertraces status` | Show what each service records and what works for its language |

Add `--dry-run` to see the changes without making them, or `--yes` to apply without asking.

Secrets go to `dotnet user-secrets` for .NET and to a git-ignored `.env` file for the other languages. In production, set the same `OTEL_*` and `POWERTRACES_*` variables in your environment.

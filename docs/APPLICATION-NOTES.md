# Application downloads and validation notes

[Back to the OUTLANDS profile](../README.md#applications-and-tools)

The [current starting guide](https://github.com/TheOutlandsDev/outlands-public-tools/blob/main/docs/START-HERE.md) routes readers to maintained downloads and worked examples. The recorded versions and validation notes below show what was checked for those releases.

## Choose a tool for your task

These download links point to the versions covered by the recorded examples. For current releases and setup instructions, follow the maintained project guides.

| Your task | Start with | Follow the exercise |
| --- | --- | --- |
| Manufacturing and reporting | [Workfloor for Windows](https://github.com/TheOutlandsDev/workfloor/releases/download/windows-v0.4.1-1/workfloor-0.4.1-windows-x64.zip) / [Cross-platform source ZIP](https://github.com/TheOutlandsDev/workfloor/releases/download/v0.4.1/workfloor-0.4.1.zip) / [Source setup guide](https://github.com/TheOutlandsDev/workfloor/blob/v0.4.1/README.md#start-here) | [Requirements, expected result and limits](https://github.com/TheOutlandsDev/outlands-public-tools/blob/main/docs/START-HERE.md#manufacturing) |
| Build a local website | [Local Site Builder for Windows](https://github.com/TheOutlandsDev/outlands-public-tools/releases/download/local-site-builder-windows-v1.0.2-2/local-site-builder-1.0.2-windows-x64.zip) / [Cross-platform source ZIP](https://github.com/TheOutlandsDev/outlands-public-tools/releases/download/local-site-builder-v1.0.2/local-site-builder-1.0.2.zip) / [Source setup guide](https://github.com/TheOutlandsDev/outlands-public-tools/blob/local-site-builder-v1.0.2/tools/local-site-builder/START-HERE.md) | [Requirements, expected result and limits](https://github.com/TheOutlandsDev/outlands-public-tools/blob/main/docs/START-HERE.md#local-website) |
| Inspect and validate code | [Developer Workspace for Windows](https://github.com/TheOutlandsDev/outlands-public-tools/releases/download/developer-workspace-windows-v0.1.1-1/developer-workspace-0.1.1-windows-x64.zip) / [Cross-platform source ZIP](https://github.com/TheOutlandsDev/outlands-public-tools/releases/download/developer-workspace-v0.1.1/developer-workspace-0.1.1.zip) / [Source setup guide](https://github.com/TheOutlandsDev/outlands-public-tools/blob/developer-workspace-v0.1.1/downloads/workbenches/developer-workspace/START-HERE.md) | [Requirements, expected result and limits](https://github.com/TheOutlandsDev/outlands-public-tools/blob/main/docs/START-HERE.md#source-review) |

[Read the complete starting guide](https://github.com/TheOutlandsDev/outlands-public-tools/blob/main/docs/START-HERE.md) · [Portfolio guide](https://connor-oshea-outlands.thatrobotguy.chatgpt.site/#start-here)

## Local Site Builder: my contribution

I designed the application: its requirements, interface and workflows, SQLite storage, draft/publish behavior, and backup/restore approach. I also handled integration and debugging, with AI assistance during implementation.

One consequential decision was keeping draft and published content separate so an unfinished edit stays private. Recovery restores verified backup contents into a fresh directory and refuses an existing destination. The tradeoff is that database changes and generated HTML are not one atomic transaction; a disk failure can leave publication incomplete and require a retry. The [validation notes](https://github.com/TheOutlandsDev/outlands-public-tools/blob/main/tools/local-site-builder/docs/VALIDATION.md) record the platform-specific checks and remaining limits.

## Reading the evidence

These are personal projects with public source and explicitly labeled demonstration data.

- **Workfloor v0.4.1:** the [portable Windows package](https://github.com/TheOutlandsDev/workfloor/blob/windows-v0.4.1-1/docs/PORTABLE-WINDOWS.md) adds an isolated bundled runtime and an extract-and-launch workflow. Its hosted browser/process checks do not establish a manual Python-free-PC test.  [Windows/Ubuntu Python 3.12/3.13 checks](https://github.com/TheOutlandsDev/workfloor/actions/runs/40723210120) cover CLI/HTTP, upgrades and recovery. [Windows browser acceptance](https://github.com/TheOutlandsDev/workfloor/actions/runs/40723210163) checks the interface; [the v0.4.1 captioned tour](https://connor-oshea-outlands.thatrobotguy.chatgpt.site/#workfloor-v04-walkthrough) shows import history, a real process restart and a restored database with the same receipt. macOS remains unqualified.
- **Local Site Builder 1.0.2:** the [focused download guide and provenance](https://github.com/TheOutlandsDev/outlands-public-tools/blob/local-site-builder-v1.0.2/tools/local-site-builder/docs/PROVENANCE.md) describe fresh-ZIP validation on Windows and Ubuntu. Checks cover private drafts, explicit local publish, stopped backup, tamper/existing-destination refusal and reopening published/private content after restore. This remains a single-user local application.
- **Code Atlas:** the published VSIX passed 38 first-launch, 39 restart and 12 Restricted Mode control assertions in Linux VS Code 1.143.0. [Native screenshots, results and reproduction](https://github.com/TheOutlandsDev/code-atlas/blob/main/docs/native-acceptance.md) show actual scanning, read-only file boundaries and restart persistence. Manual desktop search, filter and keyboard acceptance remain pending. The browser demo uses a separate fictional catalog.
- **Resource Monitor:** a Windows fictional-demo first run is recorded. Its browser adaptation does not establish live machine sampling.

Platform and recovery limits remain in each project's documentation.

The [Public Tools collection](https://github.com/TheOutlandsDev/outlands-public-tools) contains the application catalog. [Raid Control](https://connor-oshea-outlands.thatrobotguy.chatgpt.site/#raid-control) is a separate private-host dashboard case study with a sanitized idle-state capture and explicit validation limits.

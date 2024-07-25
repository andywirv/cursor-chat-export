# Cursor Chat Export

This project provides a command-line interface (CLI) tool to discover and export AI chat data from [Cursor](https://cursor.sh). The tool is implemented in `chat.py` and leverages utility classes for querying the database, formatting the chat data, and saving it to files.

Cursor's chat history is stored in `sqlite3` databases using `state.vscdb` files. One such file is for one workspace. All the chats for a workspace are saved here in so called *tabs*, one tab means a single chat.

Also see [this](https://forum.cursor.com/t/guide-5-steps-exporting-chats-prompts-from-cursor/2825) forum post on this topic.

## Features

- **Discover Chats**: Discover all `state.vscdb` files in a directory and print a few lines of dialogue so one can identify which is the workspace (chat) one is searching for. It's also possible to filter by text.
- **Export Chats**: Export chats data for a certain workspace to Markdown files or print it to the command line.

## Installation

1. Clone the repository:
    ```sh
    git clone https://github.com/somogyijanos/cursor-chat-export.git
    cd cursor-chat-export
    ```

2. Install the required dependencies:
    ```sh
    pip install -r requirements.txt
    ```

## Usage

Find, where the `state.vscdb` is located in your computer. The table below may help:

| OS               | Path                                                      |
|------------------|-----------------------------------------------------------|
| Windows          | `%APPDATA%\Cursor\User\workspaceStorage`                  |
| macOS            | `/Users/YOUR_USERNAME/Library/Application Support/Cursor/User/workspaceStorage` |
| Linux            | `/home/YOUR_USERNAME/.config/Cursor/User/workspaceStorage` |

### Discover Chats of all Workspaces
```sh
./chat.py discover --search-text "matplotlib" "/Users/myuser/Library/Application Support/Cursor/User/workspaceStorage"
```

### Auto-detect and Discover Chats
```sh
./chat.py discover --auto --search-text "matplotlib"
```

This command will automatically detect the appropriate directory for your OS and search for chats containing the word "matplotlib".

### Export Chats of a Workspace
```sh
./chat.py export --output-dir output "/Users/myuser/Library/Application Support/Cursor/User/workspaceStorage/b989572f2e2186b48b808da2da437416/state.vscdb"
```

### Auto-detect and Export Workspace Chats
```sh
./chat.py export --output-dir output --auto
```

The `--auto` flag automatically detects the Cursor workspace storage directory based on your operating system.

You can use additional flags to control which chats are exported:

- `--latest`: Exports only the most recent tab from the latest workspace.
- `--recent`: Exports all tabs from the most recently modified workspace folder.

Examples:

```sh
# Export the latest tab from the most recent workspace
./chat.py export --output-dir output --auto --latest

# Export all tabs from the most recent workspace
./chat.py export --output-dir output --auto --recent
```

These commands will automatically detect the appropriate directory for your OS, find the latest workspace, and export the chats to the specified output directory according to the chosen flag.
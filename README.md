# Tiny Things — JSON Decoder

A single-file, browser-based JSON decoder and conversation viewer for inspecting exported chat data.

It accepts pasted text, dropped files, or uploaded JSON files, detects several common export formats, and renders the result in a readable split-pane interface. Everything is processed in the browser.

## Supported formats

- Claude-style exports with `chat_messages` or `messages`.
- ChatGPT exports with conversation `mapping` trees.
- Telegram exports with a `messages` array.
- Discord exports with a `messages` array and server metadata.
- Generic JSON, displayed as a collapsible tree.

Automatic detection can be overridden from the Format panel.

## Features

- Paste JSON directly into the editor.
- Drag and drop or upload a `.json` file.
- Choose a format manually when automatic detection is not enough.
- Render conversations with roles, timestamps, titles, and a table of contents.
- Expand and collapse generic JSON objects and arrays.
- Load long conversations in batches of 80 messages.
- Copy the decoded result to the clipboard.
- Export selected conversations as `.txt` or `.pdf`.
- Adjust the reading font size from 12px to 22px.
- Drag the horizontal divider to resize the input and result panels.
- Clear the current document without reloading the page.

## Run locally

The project contains one standalone file: [decoder.html](decoder.html).

You can open it directly in a modern browser. For more predictable file-upload, clipboard, and download behavior, serve the directory locally:

```powershell
python -m http.server 8000
```

Then open <http://localhost:8000/decoder.html>.

The page loads Lucide icons, Google Fonts, and html2pdf.js from public CDNs, so those visual and PDF-export features require network access.

## Privacy

Parsing happens in the browser. The project does not include a server or persistence layer, and the loaded JSON is not intentionally sent to an application backend.

Chat exports can contain sensitive conversations, personal information, or credentials. Treat imported files carefully and avoid using this tool on shared or untrusted computers.

## Project structure

- `decoder.html` — complete UI, styles, parsing logic, format renderers, clipboard handling, and export functions.

## Limitations

- Format detection is heuristic and expects the common field shapes described above.
- PDF export depends on the html2pdf.js CDN resource.
- The viewer currently renders message text and selected metadata; provider-specific attachments and rich media are not reconstructed.

# Email Header Analyzer

Paste the raw headers of an email and this tool reconstructs the delivery path, surfaces the SPF, DKIM and DMARC results, and flags mismatches that can indicate spoofing. It is a defensive, educational tool that reads text only. No server, no tracking, no external dependencies.

## Live demo

https://0xelitesystem.github.io/email-header-analyzer/

## Features

- Message summary: From, To, Subject, Date, Message-ID, Return-Path
- Authentication results parsed from `Authentication-Results` and `Received-SPF`: SPF, DKIM, DMARC, each with a pass, fail or neutral indicator
- Delivery path reconstructed from the `Received:` chain, shown oldest first, with the `from`, `by`, `with`, `id` and timestamp for each hop and the time gap between hops
- Spoofing indicators: From domain vs Return-Path domain, and From domain vs DKIM `d=` alignment, plus SPF and DMARC failures
- View of all parsed and unfolded headers
- Dark-mode toggle, keyboard usable (Ctrl or Cmd + Enter analyzes)

## How it works

The tool unfolds the headers (a line starting with whitespace continues the previous header), then reads the fields it needs with plain string and regex parsing. The `Received:` headers are listed newest first in a real message, so the tool reverses them to show the true chronological delivery path. Authentication results are read directly from what the receiving mail server wrote in the `Authentication-Results` header. The tool does not perform DNS lookups or re-verify any DKIM signature, it reports what the headers already say. Alignment checks (From vs Return-Path, From vs DKIM `d=`) are heuristics: a mismatch is a reason to look closer, not proof of a forgery, since legitimate bulk mail and forwarding can also produce mismatches.

## Privacy

Everything runs in your browser. The headers you paste never leave your machine. You can confirm this by viewing the page source or watching the network tab in DevTools, no requests are made. The tool works offline with no external dependencies.

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT. Copyright 0xelitesystem 2026.

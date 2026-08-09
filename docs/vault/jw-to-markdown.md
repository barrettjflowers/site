---
title: Convert JW Library to Markdown
date: 2026-06-24
layout: default
---

If you're like me, you may want to run mass text manipulations, gather metrics, source control, or simply decentralize your JW Library database.

Fortunately, thanks to [this repo](https://github.com/AndreasSko/go-library-merger) most of the heavy lifting has already been done. By building on the core of this Go library, we can parse JW Library backups. At the heart of every JW Library backup file is a SQLite database. Once you understand the schema, you can do whatever you want with the data. For example, the repo mentioned above uses that data to merge backups from different devices into a single backup.

My program converts your JW Library backup into Markdown.
[https://github.com/barrettjflowers/jwtomd](https://github.com/barrettjflowers/jwtomd)

Really, that's it.
The rest is up to you.
## Why?
"Just use a device that supports JW Library natively."
Okay, then I'm probably not your target audience. =)

Need I mention the vast catalog of e-ink devices that make studying feel natural? Or maybe you just want to run it on another specialized unix-based device. I'd like the convenience of a digital space with the clarity of paper on a more open platform.

## Converting to Markdown
Clone the repository:
```bash
git clone https://github.com/barrettjflowers/jwtomd
cd jwtomd
```

Then run:
```bash
go run ./cmd/jwlexport/ your-backup.jwlibrary outputdir
```

Replace `outputdir` with your desired output directory.

There are no plans to convert Markdown back into a backup file. This is a one-way highway.

## What's next?
Since it's possible to decouple your data from JW Library, a 3rd party lightweight client could be built using the catalog and database schema for platforms that don't support JW Library, such as Intel Macs or Linux distributions.

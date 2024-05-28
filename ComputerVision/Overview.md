---
dg-publish: true
dg-home: true
---

# Overview

Home page of my Computer Vision notes. These notes are a work in progress!

The notes are created via Obsidian and published with Obsidian Digital Garden.

The source files of the notes are available on [GitHub](https://github.com/f-fuchs/ObsidianNotes).

## Table of Contents

```dataview
TABLE
	join(rows.file.link, " | ") as Notes
WHERE contains(file.folder, this.file.folder)
SORT file.name ASC
GROUP BY file.folder as Topic
```

## TODOs

 - [ ] Rework Attention Note
 - [ ] Consistent mathematical notation between notes
 - [ ] Incomplete Notes:
	- [ ] CNN
	- [ ] FNN
	- [ ] Understanding Diffusion Models A Unified Perspective
	- [ ] Generative Models
	- [ ] Pooling Layers
	- [ ] Stochastic Process
	- [ ] Adam
	- [ ] SGD

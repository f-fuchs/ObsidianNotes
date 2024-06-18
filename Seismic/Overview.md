## Table of Contents

```dataview
TABLE
	join(rows.file.link, " | ") as Notes
WHERE contains(file.folder, this.file.folder)
SORT file.name ASC
GROUP BY file.folder as Topic
```
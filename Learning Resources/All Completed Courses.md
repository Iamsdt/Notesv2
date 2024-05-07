```dataview
TABLE file.frontmatter.Author as Author, file.frontmatter.Score as Score, file.mtime as "Modified Time"
FROM #course
WHERE file.frontmatter.Status = "Done"
```



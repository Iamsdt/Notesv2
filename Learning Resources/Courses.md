
# All `In Progress` Courses

```dataview
TABLE file.frontmatter.Author as Author, file.frontmatter.Score as Score, file.mtime as "Modified Time"
FROM #course
WHERE file.frontmatter.Status = "In progress"
```


# All `Planed` Courses

```dataview
TABLE file.frontmatter.Author as Author, file.frontmatter.Score as Score, file.mtime as "Modified Time"
FROM #course
WHERE file.frontmatter.Status = "Not Started"
```


# All `Completed` Courses

```dataview
TABLE file.frontmatter.Author as Author, file.frontmatter.Score as Score, file.frontmatter.Completed as "Completed Time", file.mtime as "Modified Time"
FROM #course
WHERE file.frontmatter.Status = "Done"
```





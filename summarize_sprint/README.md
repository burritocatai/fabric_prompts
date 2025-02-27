This prompt generates a summary from Obsidian notes following Jira tasks.

You can use a function using the bash functions included in this project like below in your `.zshrc` or `.bashrc` file to help this.

```bash
concat_files ./sprint1 | fabric -p summarize_sprint > "Sprint Summary.md"
```


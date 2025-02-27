This prompt generates a summary from Obsidian notes following Jira tasks.

You can use a function like below in your `.zshrc` or `.bashrc` file to help this.

```bash

summarize_sprint() {
    if [ -z "$1" ]; then
        echo "Usage: summarize_sprint <directory>"
        return 1
    fi
    
    local directory="$1"
    local combined_text=""
            
    for file in "$directory"/*.md; do
        if [ -f "$file" ]; then
            combined_text+="$(cat "$file")"
        fi
    done
        
    local summary=$(echo "$combined_text" | fabric -p summarize_sprint -m claude-3-5-sonnet-latest)
    echo "$summary" > "Sprint Summary.md"
    echo "Sprint summary saved to Sprint Summary.md"
}

```

You can then just go to your directory where you keep the sprint notes:

```bash
cd /obsidian-directory-with-tasks/
summarize_sprint .
```
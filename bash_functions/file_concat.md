## Usage:

Concatenate all text files in the specified directory

```bash
file_concat /path/to/directory
```

Concatenate all text files in the specified directory and its subdirectories

```bash
file_concat -r /path/to/directory
```

## Code

```bash 
file_concat() {
    if [ "$#" -lt 1 ]; then
        echo "Usage: file_concat [-r] <directory>"
        return 1
    fi

    local recursive=false
    local directory=""

    if [[ "$1" == "-r" ]]; then
        recursive=true
        shift
        directory="$1"
    else
        directory="$1"
    fi

    local combined_text=""

    if $recursive; then
        for file in "$directory"/**/*.md; do
            if [ -f "$file" ]; then
                combined_text+="$(cat "$file")"
            fi
        done
    else
        for file in "$directory"/*.md; do
            if [ -f "$file" ]; then
                combined_text+="$(cat "$file")"
            fi
        done
    fi

    echo "$combined_text"
}
```

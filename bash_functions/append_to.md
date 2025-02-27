Use this to append the output to the beginning of a file, such as when summarizing:

```bash

append_to() {
    local file="$1"
    while read -r line; do
        echo "$line" >> "$file"
    done
}

```

usage:

```bash

cat my_file_to_summarize.md | fabric -p summarize | append_to my_file_to_summarize.md

```
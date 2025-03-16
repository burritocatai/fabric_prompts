# Add Fabric Patterns.

Add the following line to your `.zshrc` file or equivalent configuration file. Run this command in the base directory of your project to create symlinks for the specified patterns, making them accessible for use in Fabric.

```bash

# Function to symlink directories in current directory to fabric patterns folder
add_fabric_patterns() {
  local patterns_dir="$HOME/.config/fabric/patterns"
  
  # Create the patterns directory if it doesn't exist
  if [[ ! -d "$patterns_dir" ]]; then
    mkdir -p "$patterns_dir"
    echo "Created patterns directory: $patterns_dir"
  fi
  
  # Get all directories in the current directory
  local current_dirs=("$PWD"/*)
  
  # Count how many symlinks were created
  local count=0
  
  # Loop through each item
  for item in "${current_dirs[@]}"; do
    # Only process directories
    if [[ -d "$item" && ! -L "$item" ]]; then
      local dir_name=$(basename "$item")
      local target="$patterns_dir/$dir_name"
      
      # Create symlink if it doesn't already exist
      if [[ ! -e "$target" ]]; then
        ln -s "$item" "$target"
        echo "Linked: $item → $target"
        ((count++))
      else
        echo "Skipped: $dir_name (already exists in patterns directory)"
      fi
    fi
  done
  
  echo "Completed: $count directories symlinked to Fabric patterns"
}
```
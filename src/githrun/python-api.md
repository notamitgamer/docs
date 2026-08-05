---
label: Python API
icon: code
order: 660
---

# Python API Usage

Githrun can be used inside your own Python scripts.

```python
import githrun

# 1. Search a repository
results = githrun.search_repository("https://github.com/user/repo", "test")
for item in results:
    print(item['path'], item['raw_url'])

# 2. Download a file
githrun.download_file("https://github.com/user/repo/blob/main/script.py", output_path="script.py")

# 3. Download a full folder
githrun.download_folder("https://github.com/user/repo/tree/main/src")

# 4. Execute code programmatically
exit_code = githrun.execute_remote_code("https://github.com/user/repo/blob/main/script.py", args=["--verbose"])
```

Continue to [VS Code Extension](vscode-extension.md).

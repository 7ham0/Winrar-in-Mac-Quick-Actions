📦 WinRAR Quick Actions for macOS Finder

Easily add RAR/UnRAR commands to Finder’s Quick Actions menu, just like Windows context menu.

⸻

🔹 Step 1. Install WinRAR for macOS
	1.	Download RAR command line from rarlab.com/download.htm.
	2.	Extract the archive — you’ll see rar and unrar.
	3.	Move them to /usr/local/bin:

sudo mv rar unrar /usr/local/bin/
sudo chmod +x /usr/local/bin/rar /usr/local/bin/unrar

4.	Verify installation:

which rar
which unrar


⸻

🔹 Step 2. Create Quick Actions
	1.	Open Automator → New Document → Quick Action.
	2.	At the top:
	•	Workflow receives → files or folders
	•	in → Finder
	3.	Add Run Shell Script.
	•	Shell: /bin/zsh (or /bin/bash)
	•	Pass input: as arguments

⸻

📂 1. Unrar Here

Extract .rar file(s) into the same folder.

```json
for f in "$@"; do
  dir="${f%/*}"
  /usr/local/bin/unrar x -o+ "$f" "$dir"
done
```

💾 Save as Unrar Here.

⸻

📂 2. Unrar to Folder

Extract into a new folder named after the archive.
💾 Save as Unrar to Folder.

⸻

📦 3. Add to RAR

Add selected files/folders to an archive named MyArchive.rar.

```json
dir="${1%/*}"
archive="${dir}/MyArchive.rar"
/usr/local/bin/rar a -ep1 "$archive" "$@"
```
💾 Save as Add to RAR.

⸻

📦 4. Compress to RAR (Custom Name)

Ask for an archive name before compressing.

```json
dir="${1%/*}"
name=$(osascript -e 'Tell application "Finder" to set response to text returned of (display dialog "Enter archive name:" default answer "Archive")')
archive="${dir}/${name}.rar"
/usr/local/bin/rar a -ep1 "$archive" "$@"
```

💾 Save as Compress to RAR.

⸻

🔹 Step 3. Use in Finder
	•	Right-click any file or folder.
	•	Go to Quick Actions → choose:
	•	Unrar Here
	•	Unrar to Folder
	•	Add to RAR
	•	Compress to RAR

🎉 Done!





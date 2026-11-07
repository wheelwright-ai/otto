# Environment (this machine only; never tracked; re-derive on each machine)
Field names match "Fields a later stage needs" in `steering/records.md`. Fill each, or write `unset: ask when needed`.

- os family: <linux | mac | windows | wsl | other>
- os detail and shell: <value>
- agent runtime: <cli | ide | chat_app | local_runner | other>, product <name>
- model: <model id>
- model lanes: <any of frontier, fast, local>
- signed in: <yes | no>
- run kind: <interactive | stand-in run | neither>
- scheduler kind: <none | session_only | os_scheduler | ci | cloud> (what the wheel itself uses to start work; none at stage 0)
- hub location: <absolute path; allowed here only>
- first project location: <absolute path | unset: ask when needed>
- other projects: <name: location, or none>
- launch paths seen on this machine (not created by the hub): <counts per kind; full listings in `.local/before-raw.md`>

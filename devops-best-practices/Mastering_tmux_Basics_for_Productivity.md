🚀 Mastering tmux Basics for Productivity

If you work with terminals daily—whether as a developer, system administrator, or DevOps engineer—you’ve likely struggled with juggling multiple windows, sessions, or processes. tmux (terminal multiplexer) solves this problem elegantly, offering persistence, multitasking, and better organization for your terminal workflows.

This guide is designed as a GitHub-friendly README.md file with theory, best practices, tips, and tricks.

🔎 What is tmux?

tmux is a command-line tool that allows you to:

Run multiple sessions inside one terminal.

Detach and reattach to sessions, keeping processes running.

Split your screen into panes and manage windows.

Improve productivity by organizing work logically.

Think of tmux as tabs + split screen + session persistence for your terminal.

⚡ Installation
On Ubuntu/Debian:
sudo apt update && sudo apt install tmux -y
On CentOS/RHEL:
sudo yum install tmux -y
On macOS (Homebrew):
brew install tmux
📘 Basic Commands

Start a new session:

tmux new -s mysession

Detach from session: Ctrl+b d

List sessions:

tmux ls

Reattach to session:

tmux attach -t mysession

Kill session:

tmux kill-session -t mysession
🛠️ Best Practices

✅ Always name sessions: tmux new -s project1 → prevents confusion.

✅ Organize by projects: One session per project, multiple panes for tasks.

✅ Use consistent keybindings: Default prefix = Ctrl+b. Some prefer remapping to Ctrl+a.

✅ Persist your work: Use tmux-resurrect to restore sessions.

✅ Learn copy mode: Useful for navigating and copying logs.

🎯 Handy Tricks & Shortcuts

✨ Split panes:

Vertical → Ctrl+b %

Horizontal → Ctrl+b "

✨ Switch between panes: Ctrl+b + arrow keys

✨ Rename window: Ctrl+b ,

✨ Create new window: Ctrl+b c

✨ Scroll/copy mode: Ctrl+b [

✨ Close pane/window: exit or Ctrl+b x

📌 Why tmux Improves Productivity

🖥 Persistence: Keep long-running tasks alive after disconnects.

🔍 Focus: Split panes for code, logs, and monitoring.

🚀 Efficiency: Replace messy terminal tabs with one organized session.

💡 Pro Tips

Combine tmux + SSH for seamless remote development.

Use vim/nvim + tmux for an IDE-like experience.

Explore plugins:

tmux-resurrect → Restore sessions.

tmux-continuum → Automatic saving.

✅ Conclusion

Mastering tmux basics can transform your terminal workflow. Start small, build habits with session organization, and explore advanced plugins when comfortable.

📢 Do you have a favorite tmux trick? Feel free to share and contribute to this guide!

#tmux #Linux #DevOps #Productivity #TerminalTools

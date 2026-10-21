# track-to-demo setup

These are the instructions Claude follows when you paste the one-line setup message from the README.
You don't need to read them, but you can: they only install the plugins listed here, in this project only.

## Instructions for Claude

Install the track-to-demo setup in the current folder. Run these commands in the terminal, one at a time.
If one says the marketplace or plugin is already there, that's fine: go on.
If one fails for another reason, go on with the rest and tell the user at the end what failed and why.

```
claude plugin marketplace add sassarini-marco/track-to-demo --scope local
claude plugin install track-to-demo@track-to-demo --scope local
claude plugin install frontend-design@claude-plugins-official --scope local
claude plugin marketplace add pbakaus/impeccable --scope local
claude plugin install impeccable@impeccable --scope local
claude plugin marketplace add anthropics/skills --scope local
claude plugin install document-skills@anthropic-agent-skills --scope local
```

Then, only if this folder is empty or has a components.json (a React app with shadcn/ui), run
`npx skills add shadcn/ui --skill shadcn` with the package runner this project uses (npx, pnpm dlx, yarn dlx or bunx).

Finally, make sure the .gitignore in this folder has the line `.claude/settings.local.json` (create the file if it is
missing): local-scope plugins and personal permissions live there and should not reach the team's repo.

Install nothing else. When you're done, tell the user in plain words what was installed and ask them to type
`/reload-plugins` and then `/reload-skills`.

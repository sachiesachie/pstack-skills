# pstack skills

The pstack agent skills (poteto-mode, architect, the principle-* skills, how, why, swarm, interrogate, and more), packaged so cloud Claude Code sessions can load them.

## Use in a cloud environment

Add this as the environment's setup script:

```bash
git clone --depth 1 https://github.com/sachiesachie/pstack-skills ~/pstack-skills && mkdir -p ~/.claude/skills && cp -R ~/pstack-skills/skills/* ~/.claude/skills/ && cp ~/pstack-skills/CLAUDE.md ~/.claude/CLAUDE.md
```

New sessions in that environment then list the skills as user skills and load `CLAUDE.md` as user-level rules.

## License

MIT. See `LICENSE`.

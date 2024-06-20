Clean Pacman Cache. This command will remove all but the latest version of package files from the Pacman cache. It's a safe way to reclaim disk space used by outdated package files.

```bash
sudo pacman -Sc
```

Clean Paru Cache. Paru, like other AUR helpers, may also keep a cache of downloaded AUR package files. To clean the Paru cache, you can use the -cc option:

```bash
paru -Scc
```

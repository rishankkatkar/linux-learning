# Log: pwd, pwd -L, pwd -P, ln -s, id, id -u, id -g

## pwd

`pwd` = print working directory. Shows where I currently am in the filesystem.

Related to this, there are two variants tied to symbolic links:

- `pwd -L` → prints the **logical** path
- `pwd -P` → prints the **physical** path

## Testing pwd Variants (Using a Symlink)

Used a symbolic link only as a way to test the difference between `pwd`, `pwd -L`, and `pwd -P`. Symlinks themselves weren't the thing being studied here.

I was at: `~/home/kali/Documents/newfolder`

Created a symbolic link using:

```bash
ln -s ~/Downloads ~/home/kali/Documents/newfolder/symboliclinkshortcut
```

Here, `~/Downloads` is the target the link points to, and `symboliclinkshortcut` is the shortcut itself, sitting inside `newfolder`.

Then moved into it and ran pwd variants:

```bash
cd symboliclinkshortcut
pwd
# ~/Documents/newfolder/symboliclinkshortcut

pwd -L
# ~/Documents/newfolder/symboliclinkshortcut

pwd -P
# ~/Downloads
```

### My understanding of logical vs physical

The symbolic link "shortcut" physically sits at `~/Documents/newfolder/symboliclinkshortcut` — but that's called the **logical** path, not physical. The **physical** path is `~/Downloads`, which is what the shortcut actually points to.

My way of remembering it: the shortcut itself isn't a real file/folder — it's just a pointer. So the place where the *pointer* sits is "logical," and the place it *actually leads to* is "physical." Still fuzzy on why the naming is this way around, but this framing makes sense to me for now. Might be wrong — need to revisit.

## id / uid / gid

Ran plain `id` first — got a long output with uid, gid, and groups. Then isolated each:

```bash
id -u   # shows only UID
id -g   # shows only GID
```

### What I understood

- **UID** = unique ID for each user (Linux supports multiple users). Stays the same even if username/password changes.
- UID `0` = root (most powerful user).
- UID `1–999` = reserved for system users — background processes, not real people. Don't know much beyond this yet.
- UID `1000+` = regular/human users.
- **GID** = group ID, useful when multiple users need the same permissions (e.g., working on the same project).
- Noticed UID and GID were the same number for my user — not fully sure why, going in as a guess for now.

## Confidence Check

**Solid on:**

- `pwd`, `pwd -L`, `pwd -P` — comfortable running and reading output
- Creating a symbolic link with `ln -s`
- Running `id`, `id -u`, `id -g` and reading basic output

**Shaky on:**

- *Why* logical path = link location and physical path = target (naming still counterintuitive)
- Full purpose/use-case of GID beyond the basic definition
- Why UID and GID matched for my user — unconfirmed guess

**Next:**

- Revisit logical/physical path naming after some practice
- Dig deeper into GID real-world use cases

# Void Linux Repository

A custom XBPS repository for Void Linux.

---

## Adding the Repository

### 1. Add the repository source

```bash
echo "repository=https://rxelelo.github.io/void-repo" \
  | sudo tee /etc/xbps.d/noctalia.conf
```

### 2. Sync and verify

```bash
sudo xbps-install -S
```

You should see the repository appear in the sync output. If you get a signature error, double check that the key was placed correctly in `/var/db/xbps/keys/`.

---

## Optional Dependencies (Noctalia Shell)

These are not installed automatically but unlock additional features:

| Package | Feature |
|---|---|
| `cliphist` | Clipboard history |
| `cava` | Audio visualizer component |
| `wlsunset` | Night light / color temperature |
| `power-profiles-daemon` | Power profile management |
| `ddcutil` | External display brightness control |

Install any of them with:

```bash
sudo xbps-install cliphist cava wlsunset
```

---

## Updating

```bash
sudo xbps-install -Su
```

This will update all packages including ones from this repository.

---

## Removing the Repository

```bash
sudo rm /etc/xbps.d/noctalia.conf
sudo rm /var/db/xbps/keys/f9:75:69:31:bd:ee:dd:5e:d7:48:97:7f:4b:f1:0f:72.plist
sudo xbps-install -S
```

Note: removing the repo source does not uninstall already-installed packages.

---

## Troubleshooting (Noctalia Shell)

**Signature verification failed**
Make sure the public key is in `/var/db/xbps/keys/` and re-run `sudo xbps-install -S`.

**Package not found after adding repo**
Run `sudo xbps-install -S` to sync the repository index before installing.

**Conflicts with existing quickshell installation**
`noctalia-qs` conflicts with `quickshell` and `quickshell-git`. Remove them first:
```bash
sudo xbps-remove quickshell
# or
sudo xbps-remove quickshell-git
```

Then install `noctalia-qs` or `noctalia-shell` as normal.

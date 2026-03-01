# Noctalia Void Linux Repository

A custom XBPS repository providing `noctalia-qs` and `noctalia-shell` packages for Void Linux.

---

## Adding the Repository

### 1. Add the repository source

```bash
echo "repository=https://rxelelo.github.io/noctalia-void-repo" \
  | sudo tee /etc/xbps.d/noctalia.conf
```

### 2. Add the signing key

Packages in this repository are signed. You need to trust the public key before installing anything:

```bash
sudo mkdir -p /var/db/xbps/keys
curl -fsSL https://rxelelo.github.io/noctalia-void-repo/public.pem \
  | sudo tee /var/db/xbps/keys/noctalia.pem
```

### 3. Sync and verify

```bash
sudo xbps-install -S
```

You should see the repository appear in the sync output. If you get a signature error, double check that the key was placed correctly in `/var/db/xbps/keys/`.

---

## Installing Packages

### Noctalia Shell (recommended)

Installs the full shell along with all required dependencies including `noctalia-qs`:

```bash
sudo xbps-install noctalia-shell
```

### Noctalia QS only

If you only want the Quickshell fork without the shell config:

```bash
sudo xbps-install noctalia-qs
```

---

## Optional Dependencies

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
sudo rm /var/db/xbps/keys/noctalia.pem
sudo xbps-install -S
```

Note: removing the repo source does not uninstall already-installed packages.

---

## Troubleshooting

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

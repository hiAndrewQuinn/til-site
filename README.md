# Today I Learned (TIL) - Website

The 🥩🍖 of this website is already tracked at [my `til` repo](https://github.com/hiAndrewQuinn/til), but I've been on a kick latetly of using [Git submodules](https://github.blog/2016-02-01-working-with-submodules/) and [`systemd` timers](https://wiki.archlinux.org/title/Systemd/Timers) to make my own teensy-tiny local-first automated builds, so here we are!

## Quickstart

Test against Hugo version...

```bash
❯ hugo version
hugo v0.147.9-29bdbde19c288d190e889294a862103c6efb70bf+extended linux/amd64 BuildDate=2025-06-23T08:22:20Z VendorInfo=snap:0.147.9
```

... Yeah, that one. Although this site has been kicking for a few 
years with Hugo already with minimal
changes, so I doubt you'll have much trouble version wise.

Getting this up to speed is easy!

```bash
# Create a temporary directory and schedule its automatic removal on shell exit.
AQDM_TIL_TEMP_DIR=$(mktemp -d "$HOME/til-site-temp.XXXXXX")
trap 'rm -rf "$AQDM_TIL_TEMP_DIR"' EXIT

# Proceed inside the safe, temporary directory.
cd "$AQDM_TIL_TEMP_DIR"
git clone git@github.com:hiAndrewQuinn/til-site.git

cd til-site

# The actual content is stored in a Git submodule, at 
#    https://github.com/hiAndrewQuinn/til
# It's just a big ol' stack of Markdown files.
git submodule update --init --remote

hugo server --renderToMemory
```

That's it! Now just go to `http://localhost:1313/til-site/`  or wherever Hugo points 
you toin your web browser to see the magic happen.

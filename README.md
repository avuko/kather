# rkathe

kathe, but Rust.

# Context

## Docker

I've created a Docker deployment script using ansible (on localhost).

It can be found in [docker-configure.yml](./docker-configure.yml).

Use `ansible-playbook docker-configure.yml --user=<username> --ask-become-pass`to set it up.

After that, running `ansible-playbook docker-container.yml --user=<username> --ask-become-pass`will deploy a currently rather useless container, based on the [docker-container.yml](./docker-container.yml) file.

## Rust environment

Following https://www.rust-lang.org/tools/install I simply ran: `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh`.

### Vim

My vim setup is rather complex, but normally this should work. In `.vimrc`:

```ini
syntax enable
filetype plugin indent on
```

I use pathogen, so:

```bash
git clone --depth=1 https://github.com/rust-lang/rust.vim.git ~/.vim/bundle/rust.vim
```

`sudo snap install --classic rustup`might come in handy too. 